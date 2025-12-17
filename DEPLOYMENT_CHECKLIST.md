# Deployment Checklist for Separate Repo

## Important: Remove pnpm-lock.yaml

Since you're using npm (not pnpm), make sure to **delete `pnpm-lock.yaml`** from your `omniflow-kiosk` repository:

```bash
git rm pnpm-lock.yaml
git commit -m "Remove pnpm-lock.yaml, using npm instead"
git push
```

This will prevent Netlify from trying to use pnpm and causing lockfile errors.

## Verify netlify.toml is at Root

Make sure `netlify.toml` is at the **root** of your `omniflow-kiosk` repository (not in a subdirectory).

## Netlify Configuration

The `netlify.toml` is configured for:
- ✅ Root-level Next.js app (no base directory)
- ✅ Using npm (not pnpm)
- ✅ Next.js plugin for SSR support
- ✅ Publish directory: `.next`

## Environment Variables

Set these in Netlify Dashboard → Site Settings → Environment Variables:
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

## After Removing pnpm-lock.yaml

1. Commit and push the removal
2. Trigger a new deploy in Netlify
3. The build should now use npm and succeed

