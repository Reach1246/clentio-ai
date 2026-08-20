# Clentio.ai

> Building Brands Too BIG to Ignore

A personal brand positioning and LinkedIn content platform for B2B founders and CEOs, featuring an AI-powered LinkedIn post writer.

## What's included

- **Static site**: Single-page responsive portfolio with content library, framework guides, and FAQs
- **AI LinkedIn Writer**: Claude-powered agent that generates posts in your voice
- **Lead capture**: Bundle unlock, newsletter signup, and profile audit requests (stored locally)
- **PWA support**: Installable on mobile and desktop with offline-first service worker
- **Serverless backend**: Vercel function holds your Anthropic API key securely

## Quick start

See [DEPLOY.md](./DEPLOY.md) for detailed deployment instructions on Vercel.

### Local development
```bash
npm install -g vercel
vercel dev
```

Then open the URL it gives you (usually `http://localhost:3000`).

## Files

- `index.html` — Main site, all content, forms, and AI writer UI
- `manifest.json` — PWA manifest for app installation
- `sw.js` — Service worker for offline-first caching
- `api/generate.js` — Serverless function that calls Claude API (your key stays here, not exposed to frontend)
- `.env.example` — Template for local environment variables
- `vercel.json` — Vercel function configuration

## Key features

### AI Writer
Give it a topic and choose a content pillar. It generates a LinkedIn post in your voice with:
- Short declarative sentences
- "How I" hooks
- No em dashes, hashtags, or rhetorical questions
- Soft closing

### Lead management
All form submissions (bundle, newsletter, audit) are stored in browser localStorage. No backend database required to get started.

### Content library
Real posts from your LinkedIn account, filterable by content pillar (Broad, Narrow, Niche, Storytell).

## Deployment

1. Push to GitHub
2. Connect to Vercel and deploy
3. Add `ANTHROPIC_API_KEY` environment variable
4. Redeploy with `vercel --prod`

See [DEPLOY.md](./DEPLOY.md) for full walkthrough.
