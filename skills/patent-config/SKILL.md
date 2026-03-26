---
name: patent-config
description: "v1.0.0 — Configure the Memoriant Patent Platform — LLM provider, search providers, API keys, and connection mode (API-connected vs standalone)."
---

# Patent Config Skill

> DISCLAIMER: This skill manages platform configuration only and does not constitute legal advice. Never share API keys or config files containing secrets with third parties.

Configure and manage the Memoriant Patent Platform settings, including LLM providers, search providers, API keys, and backend connection.

## Configuration File Location

The platform configuration is stored at:

```
~/.memoriant-patent/config.yaml
```

The directory is created automatically on first run. Sensitive values (API keys) are stored with 600 permissions (owner read/write only).

---

## LLM Provider Options

### Claude (Anthropic) — Default, Recommended

Best quality for claim drafting, § 101 analysis, and nuanced patent language. Requires an Anthropic API key.

```yaml
llm:
  provider: claude
  model: claude-opus-4-6           # Recommended: extended thinking for complex claims
  # model: claude-sonnet-4-6       # Faster, balanced quality
  api_key: ""                      # Leave blank — use ANTHROPIC_API_KEY env var instead
  max_tokens: 16000
  temperature: 0.3                 # Lower = more consistent legal text
  extended_thinking: true          # Enable for patent claim analysis (Opus only)
```

**Setup:**
```bash
export ANTHROPIC_API_KEY="sk-ant-your-key-here"
```

**Why extended thinking:** Patent claim analysis requires multi-step reasoning — evaluating prior art combinations, anticipating rejection angles, and choosing the broadest defensible scope. Extended thinking improves accuracy on all of these.

---

### Ollama — Recommended for Air-Gapped / Local Deployment

Zero-cloud, runs fully on local hardware. Best for compliance-sensitive environments where data cannot leave the premises.

```yaml
llm:
  provider: ollama
  base_url: http://localhost:11434  # Local Ollama instance
  # base_url: http://10.0.4.93:11434  # Remote Ollama (e.g., DGX Spark)
  model: qwen2.5:72b               # Recommended for patent quality
  # model: llama3.1:70b            # Alternative
  temperature: 0.3
  context_window: 32768
```

**Setup:**
```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Pull recommended model
ollama pull qwen2.5:72b

# Verify
ollama list
curl http://localhost:11434/api/tags
```

---

### vLLM — Recommended for High-Throughput GPU Deployment

Fastest option for GPU servers. Suitable for batch processing multiple patent applications.

```yaml
llm:
  provider: vllm
  base_url: http://10.0.4.93:8000   # vLLM server address
  model: Qwen/Qwen2.5-72B-Instruct  # HuggingFace model ID
  max_tokens: 8192
  temperature: 0.3
```

**Setup on a GPU server:**
```bash
pip install vllm
python -m vllm.entrypoints.openai.api_server \
  --model Qwen/Qwen2.5-72B-Instruct \
  --port 8000 \
  --tensor-parallel-size 4
```

---

### LM Studio — Recommended for Desktop / Mac

Easy GUI-based model management with an OpenAI-compatible API. No command line required.

```yaml
llm:
  provider: lm_studio
  base_url: http://localhost:1234   # LM Studio local server
  # base_url: http://10.0.4.93:1234  # Remote LM Studio instance
  model: auto                       # Uses currently loaded model in LM Studio
  temperature: 0.3
```

**Setup:**
1. Download LM Studio from https://lmstudio.ai
2. Load a model (recommended: Qwen2.5-72B-Instruct-GGUF Q4_K_M for best patent quality)
3. Start the local server (Server tab → Start Server)
4. Update `base_url` if running on a remote machine

---

## Search Provider Configuration

The platform is **free by default** using public USPTO APIs. Paid providers offer higher rate limits and additional databases.

### Free Providers (Default — Both Enabled)

```yaml
search:
  providers:
    patentsview:
      enabled: true                 # Default: on
      base_url: https://search.patentsview.org/api/v1/
      rate_limit: 45               # requests per minute (free tier)
      timeout: 30

    uspto_full_text:
      enabled: true                 # Default: on
      base_url: https://efts.uspto.gov/LATEST/search-index
      rate_limit: 10               # conservative for public API
      timeout: 30
```

### Paid Providers (Opt-In)

**SerpAPI — Google Patents + broader web patent coverage:**
```yaml
search:
  providers:
    serpapi:
      enabled: false               # Change to true to enable
      api_key: ""                  # Or set SERPAPI_API_KEY env var
      base_url: https://serpapi.com/search
```

Note: SerpAPI pricing starts at $50/month for 100 searches. See https://serpapi.com/pricing.

**Lens.org — patents and non-patent literature (NPL):**
```yaml
search:
  providers:
    lens:
      enabled: false
      api_key: ""                  # Register at https://www.lens.org/lens/user/subscriptions
      base_url: https://api.lens.org/patent/search
```

---

## API Key Management

### Security Rules
- Never store API keys directly in `config.yaml` if that file may be committed to version control
- Prefer environment variables for all keys
- The config file must be chmod 600 if keys are stored in it — the platform enforces this on write

### Recommended: Environment Variables
```bash
# Add to ~/.zshrc or ~/.bashrc
export ANTHROPIC_API_KEY="sk-ant-..."
export SERPAPI_API_KEY="your-key"
export LENS_API_KEY="your-key"
```

### Checking Key Status
The platform never displays full API key values. It shows only a masked hint (e.g., `sk-ant-...abc1`) to confirm a key is configured.

```bash
# Check which providers are active and keys are present
curl http://localhost:8000/api/config/providers

# Output example:
# {
#   "llm": {"provider": "claude", "model": "claude-opus-4-6", "key_hint": "sk-ant-...abc1", "status": "ok"},
#   "search": {
#     "patentsview": {"enabled": true, "status": "ok"},
#     "serpapi": {"enabled": false, "key_hint": null}
#   }
# }
```

---

## Mode Selection: API-Connected vs Standalone

### API-Connected Mode
Requires the Memoriant Patent Platform backend running locally or on a server.

```yaml
mode: api_connected
api:
  base_url: http://localhost:8000
  timeout: 120
  api_key: ""                      # Leave blank for unauthenticated local instance
```

Features available in API-connected mode:
- Full pipeline orchestration with persistent session state
- Real-time progress tracking
- DOCX and PDF export via backend rendering
- Multi-user support (with auth enabled)
- Session history and audit log

**Start the backend:**
```bash
# Docker (recommended)
docker compose up -d

# Or directly
uvicorn api.main:app --host 0.0.0.0 --port 8000

# Verify
curl http://localhost:8000/health
```

### Standalone Mode
No backend required. All processing runs through Claude Code skills directly.

```yaml
mode: standalone
output:
  output_dir: ~/memoriant-patent-output
  session_dir: ~/.memoriant-patent/sessions
```

Features available in standalone mode:
- All patent skills (search, draft, review, diagrams)
- Prior art search via direct PatentsView API calls (WebFetch)
- Session state saved as local JSON files
- Export via local Pandoc if installed
- No Docker, no database required

**Limitation:** Standalone mode does not support DOCX/PDF rendering without Pandoc. Install with `brew install pandoc` on macOS.

---

## Complete Config Example

```yaml
# ~/.memoriant-patent/config.yaml
# Permissions: chmod 600 ~/.memoriant-patent/config.yaml

mode: standalone                   # api_connected | standalone

api:
  base_url: http://localhost:8000
  timeout: 120
  api_key: ""

llm:
  provider: claude                 # claude | ollama | vllm | lm_studio
  model: claude-opus-4-6
  api_key: ""                      # Use ANTHROPIC_API_KEY env var
  temperature: 0.3
  max_tokens: 16000
  extended_thinking: true

search:
  providers:
    patentsview:
      enabled: true
      rate_limit: 45
      timeout: 30
    uspto_full_text:
      enabled: true
      rate_limit: 10
      timeout: 30
    serpapi:
      enabled: false
      api_key: ""                  # Use SERPAPI_API_KEY env var
    lens:
      enabled: false
      api_key: ""                  # Use LENS_API_KEY env var

output:
  default_format: docx             # docx | pdf | both
  output_dir: ~/memoriant-patent-output
  save_session_state: true
  session_dir: ~/.memoriant-patent/sessions

logging:
  level: INFO                      # DEBUG | INFO | WARNING | ERROR
  log_file: ~/.memoriant-patent/logs/platform.log
```

---

## Initial Setup Walkthrough

```bash
# 1. Create config directory structure
mkdir -p ~/.memoriant-patent/sessions ~/.memoriant-patent/logs

# 2. Create base config (standalone mode, Ollama LLM, free search providers)
cat > ~/.memoriant-patent/config.yaml << 'EOF'
mode: standalone

llm:
  provider: ollama
  base_url: http://localhost:11434
  model: qwen2.5:72b
  temperature: 0.3

search:
  providers:
    patentsview:
      enabled: true
    uspto_full_text:
      enabled: true
EOF

# 3. Lock down permissions
chmod 600 ~/.memoriant-patent/config.yaml

# 4. Test search connectivity
curl "https://search.patentsview.org/api/v1/patent/?q={%22patent_title%22:%22test%22}&f=[%22patent_id%22]&o={%22per_page%22:1}"

# 5. Test Ollama
curl http://localhost:11434/api/tags
```

---

## Usage

To configure the platform, specify:
1. **LLM provider** — which AI backend to use (default: Claude with Opus 4.6 + extended thinking)
2. **Mode** — API-connected (full features) or standalone (no backend required)
3. **API keys** — for Claude or paid search providers (use env vars; never paste full keys here)
4. **Search preferences** — which providers to enable

The skill will generate or update `~/.memoriant-patent/config.yaml`, set correct file permissions, and verify connectivity to each configured provider.

---
## Version History
- **v1.0.0** (2026-03-25) — Initial release
