# Goggles

AI-powered meta search engine that aggregates results from multiple search engines with intent-based query classification.

## Features
official instance https://gogglesofficial.netlify.app/
- **Multi-engine search** - Google, DuckDuckGo, SearXNG, Wikipedia, Bing
- **AI intent detection** - Automatically classifies queries as General, Math, Conversion, OSINT, or Code
- **Dynamic SearXNG instances** - Fetches live instances from searx.space, rotates per search
- **Zero API keys** - No sign-up, no tokens, no billing
- **AI summaries** - Get condensed answers from search results
- **Special handlers** - Direct math evaluation, currency/unit conversion
- **OSINT mode** - Reformats queries for intelligence gathering
- **Minimal UI** - Pure black, fast, no bloat

## How It Works

```
User Query → AI Intent Detection → Parallel Search → Deduplicate → Rank → Display
```

### Intent Types

| Intent | Trigger Example | Sources |
|--------|----------------|---------|
| General | "best restaurants NYC" | Google, DDG, SearXNG, Wikipedia |
| Math | "2^16 + sqrt(144)" | Direct eval + DDG, Wikipedia |
| Conversion | "USD to EUR", "5 km to miles" | Direct calc + Google, DDG |
| OSINT | "find info on username X" | Google, DDG, SearXNG, Bing |
| Code | "python async tutorial" | Google, DDG, SearXNG, Wikipedia |

### Search Sources

| Source | Method | Auth |
|--------|--------|------|
| Google | HTML scrape via CORS proxy + SearXNG fallback | None |
| DuckDuckGo | HTML endpoint via CORS proxy | None |
| SearXNG | JSON API from dynamic instances | None |
| Wikipedia | Official API (CORS-friendly) | None |
| Bing | Lite HTML via CORS proxy | None |

### AI Providers (fallback chain)

1. **uncloseai** - Hermes Llama 3.1 8B (primary)
2. **uncloseai** - Qwen Coder 30B
3. **Pollinations AI** - openai-large (GPT-4o-mini class)
4. **Pollinations AI** - Raw GET endpoint

## Usage

Open `index.html` in a browser or serve it locally:

```bash
python -m http.server 8080
```

Then visit `http://localhost:8080`

## File Structure

```
goggles/
└── index.html    # Single file app (~1700 lines)
```

## Tech

- HTML5, CSS, vanilla JavaScript
- No frameworks, no build step, no dependencies
- CORS proxies for cross-origin search requests
- localStorage for search history and engine preferences

## Notes

- CORS proxies may occasionally fail - the app has 4 fallbacks
- SearXNG instances are fetched from searx.space on load with 8 hardcoded fallbacks
- Google scraping may return captchas - falls back to SearXNG Google engine
- Engine preferences persist in localStorage
