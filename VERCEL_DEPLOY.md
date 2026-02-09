# Vercel Deployment Guide

Two separate Vercel projects for mainnet (Rhino single-pool) and Bepolia (discovery mode).

## Prerequisites

- Vercel account
- Vercel CLI: `npm i -g vercel`
- This repository pushed to GitHub

## Deploy Mainnet (Rhino)

1. Navigate to project directory:
   ```bash
   cd /Users/camembearbera/src/guides/apps/staking-pools/frontend
   ```

2. Deploy using mainnet config:
   ```bash
   vercel --prod --config vercel.mainnet.json
   ```

3. Follow prompts:
   - Link to existing project or create new
   - Project name: `staking-pools-rhino-mainnet`
   - Framework: Vite (auto-detected)

## Deploy Bepolia

1. From same directory:
   ```bash
   vercel --prod --config vercel.bepolia.json
   ```

2. Follow prompts:
   - Create new project (not the same as mainnet)
   - Project name: `staking-pools-bepolia`
   - Framework: Vite (auto-detected)

## Vercel Dashboard Setup

After CLI deployment, you'll need to configure each project in the Vercel dashboard:

### For Both Projects

1. Go to project settings → Git
2. Connect to your GitHub repository
3. Set Production Branch to your main branch
4. Configure build settings:
   - **Mainnet project**: Override build command with `cp public/config.deploy.rhino-mainnet.json public/config.json && npm run build`
   - **Bepolia project**: Override build command with `cp public/config.deploy.bepolia.json public/config.json && npm run build`

### Custom Domains (Optional)

1. Go to project settings → Domains
2. Add custom domain for each:
   - Mainnet: `rhino.yourdomain.com` or similar
   - Bepolia: `bepolia-pools.yourdomain.com` or similar

## Redeployment

After pushing to GitHub, both projects will auto-deploy on commits to the production branch.

Manual redeploy from CLI:
```bash
# Mainnet
vercel --prod --config vercel.mainnet.json

# Bepolia
vercel --prod --config vercel.bepolia.json
```

## Verification

After deployment, check:
- Site loads at Vercel URL
- Config loads correctly (check browser console)
- Network matches expected (mainnet: 80094, Bepolia: 80069)
- Mode is correct (mainnet: single, Bepolia: discovery)
