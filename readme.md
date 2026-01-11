# Tweet + Markdown Publisher

A lightweight, single-page web app for publishing content to Twitter and GitHub simultaneously.

## What it does

- Write a tweet and create a markdown file that gets committed to a GitHub repo in one action
- Opens a Twitter intent URL (one click to post) — no paid API required
- Uploads images to your repo and auto-inserts markdown references
- Works on desktop and mobile

## Modes

**Tweet + Markdown** — Tweet text becomes the headline, opens Twitter intent, commits markdown to GitHub

**Markdown Only** — Commits to GitHub without tweeting

## Markdown format

```markdown
---
headline: "(tweet or headline text)"
tag: "(user-provided)"
date: YYYY-MM-DD
draft: true/false
---

(optional body content and images)
```

Files are saved as `YYYY-MM-DD-slugified-headline.md`

## Setup

### 1. Create a GitHub OAuth App

1. Go to GitHub → Settings → Developer settings → [OAuth Apps](https://github.com/settings/developers) → New OAuth App
2. Fill in:
   - **Application name**: e.g., "My Publisher"
   - **Homepage URL**: Your deployed site URL (e.g., `https://yoursite.netlify.app`)
   - **Authorization callback URL**: Same as homepage URL
3. Click "Register application"
4. Copy the **Client ID**
5. Generate a new **Client Secret** and copy it

### 2. Deploy to Netlify

1. Push this repo to GitHub
2. Go to [Netlify](https://netlify.app) and import your repo
3. In Site settings → Environment variables, add:
   - `GITHUB_CLIENT_ID` — the Client ID from step 1
   - `GITHUB_CLIENT_SECRET` — the Client Secret from step 1
4. In `index.html`, replace `YOUR_CLIENT_ID` with your actual Client ID

### 3. Use the app

1. Open your deployed site
2. Click "Sign in with GitHub"
3. Select a repository from the dropdown
4. Configure folder paths in Settings (e.g., `content/posts`, `static/images`)

Settings are saved in your browser's localStorage.

## Hosting

This app requires Netlify for the OAuth serverless function.

1. Push this repo to GitHub
2. Import at [netlify.app](https://netlify.app)
3. Add environment variables (see Setup above)
4. Deploy

For local development, use `netlify dev` to run the function locally.

## Security note

- OAuth tokens are stored in browser localStorage
- The Client Secret is kept secure on the server (Netlify function)
- Tokens have `repo` scope to commit to your repositories

## Tech

- HTML/CSS/JS frontend — no build step
- Netlify serverless function for OAuth token exchange
- GitHub REST API for commits and repo listing
- GitHub OAuth for authentication

## License

MIT