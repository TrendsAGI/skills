# TrendsAGI Skills

This repository contains Agent Skills for the TrendsAGI API.

## Skills
- `trendsagi`: Real-time market trends, keyword analytics, financial intelligence, and AI insights.

## Structure
Skills live in `skills/<skill-name>/` and each skill includes a `SKILL.md` with instructions, plus optional `scripts/`, `references/`, and supporting files.

## Quick Start
1. Set `TRENDSAGI_API_KEY` in your environment.
2. Run:

```bash
node skills/trendsagi/scripts/get-trends.js --limit 5 --period 24h
```

## Notes
- Default API base URL is `https://api.trendsagi.com` (override with `TRENDSAGI_BASE_URL`).
- Scripts output JSON to stdout and exit non-zero on errors.
- Requires Node.js 18+ for built-in `fetch`.
