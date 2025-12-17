# Netlify Deployment Guide for OmniFlow Kiosk App

## Current Configuration

The `netlify.toml` file is configured for Next.js deployment with the `@netlify/plugin-nextjs` plugin.

## If Build Fails

### Option 1: Check Build Logs
The build error shows "exit code: 2" but doesn't show the actual error. Check the full build logs in Netlify dashboard to see:
- What command failed
- Any missing dependencies
- TypeScript/compilation errors

### Option 2: Try Without Plugin
If the plugin causes issues, try this alternative `netlify.toml`:

```toml
[build]
  command = "npm run build && npm run export"
  publish = "out"

[build.environment]
  NODE_VERSION = "18"
```

But this requires adding `export` script to package.json and configuring Next.js for static export.

### Option 3: Manual Netlify Configuration
In Netlify Dashboard:
1. Go to Site Settings → Build & Deploy
2. Set **Base directory**: `kiosk-app` (if deploying from monorepo)
3. Set **Build command**: `npm run build`
4. Set **Publish directory**: `.next`
5. Install plugin: Go to Plugins → Add plugin → Search for "@netlify/plugin-nextjs"

### Option 4: Check Environment Variables
Ensure these are set in Netlify:
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

### Common Issues

1. **Plugin not found**: The `@netlify/plugin-nextjs` plugin should auto-install, but if it fails, you can install it manually in Netlify dashboard.

2. **Build directory**: Make sure Netlify is building from the correct directory. If deploying from a separate repo (`omniflow-kiosk`), the `netlify.toml` should be at the root of that repo.

3. **Node version**: Ensure Node.js 18 is available (configured in netlify.toml).

4. **Dependencies**: Make sure `package-lock.json` is committed and up to date.

## Recommended: Use Vercel Instead

For Next.js apps, Vercel is the recommended platform as it's built by the Next.js team and handles everything automatically.

