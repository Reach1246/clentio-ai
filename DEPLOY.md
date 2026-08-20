# Deploying Clentio.ai with the AI Writer backend

This folder is a static site (`index.html`, `manifest.json`, `sw.js`, `icons/`) plus one
serverless function (`api/generate.js`) that holds your Anthropic API key and powers the
AI LinkedIn Writer. The frontend never touches the key directly.

## Get an API key
1. Go to https://console.anthropic.com
2. Create or open your account, go to API Keys, generate a new key.
3. Note: this is billed separately from any Claude.ai subscription, pay-as-you-go. Content
   generation at solo-founder volume typically costs a few dollars a month at most.

## Deploy on Vercel (recommended, free tier works)

1. Install the CLI once: `npm install -g vercel`
2. From inside this folder, run: `vercel`
3. Follow the prompts (link or create a project). It will deploy immediately.
4. Add your API key as an environment variable:
   - `vercel env add ANTHROPIC_API_KEY`
   - paste your real key when prompted, choose "Production" (and "Preview" if you want)
5. Redeploy so the function picks up the new env var: `vercel --prod`

Your site and the `/api/generate` function are now live on the same domain, so the AI
Writer button will work immediately, no extra CORS setup needed.

### Alternative: deploy via the Vercel dashboard (no CLI)
1. Push this folder to a GitHub repo.
2. Go to vercel.com → Add New Project → import the repo.
3. Before the first deploy, add `ANTHROPIC_API_KEY` under Project Settings → Environment Variables.
4. Deploy.

## Local testing before you deploy
1. Copy `.env.example` to `.env.local` and paste your real key in.
2. Run `vercel dev` from this folder. It serves both the static site and the `/api` function locally.
3. Open the local URL it gives you and test the AI Writer form.

## Installing the app once it's live
Once deployed, visit your live URL on your phone or desktop:
- **Android/Chrome:** tap the in-app "Install" banner or the browser's install prompt.
- **iPhone/Safari:** tap Share → "Add to Home Screen."
- **Desktop Chrome/Edge:** click the install icon in the address bar.

## Notes
- The rate limiter in `api/generate.js` is in-memory and resets whenever the function cold-starts.
  It's a basic safeguard against runaway costs, not a production-grade limiter. If this gets real
  traffic, swap it for a proper store (Vercel KV, Upstash Redis, etc.).
- Lead form submissions (bundle unlock, newsletter, profile audit) still save to each visitor's own
  browser storage, not a shared database. That's a separate piece from the AI Writer, happy to wire
  up a real leads database next if you want centralized visibility.
