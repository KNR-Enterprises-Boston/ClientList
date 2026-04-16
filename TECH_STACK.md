# Tech Stack

## Core Framework & Runtime

| Technology | Version | Role |
|------------|---------|------|
| Next.js | 15.5.15 | React meta-framework with App Router, static export |
| React | 19.2.5 | UI library |
| React DOM | 19.2.5 | DOM rendering |
| TypeScript | 5.9.3 | Static typing (strict mode) |
| Node.js | ^18.18.0 \|\| ^20.9.0 \|\| >=21.1.0 | Runtime requirement |

## Build Configuration

- **Output mode:** Static export (`output: "export"`)
- **Build output directory:** `./out/`
- **TypeScript target:** ES2022
- **Module resolution:** bundler
- **Path aliases:** `@/*` → `src/*`
- **Image optimization:** Disabled (static export)
- **Trailing slashes:** Enabled

## Mapping

| Library | Version | Role |
|---------|---------|------|
| Leaflet | 1.9.4 | Open-source interactive mapping |
| React Leaflet | 5.0.0 | React bindings for Leaflet |
| @types/leaflet | 1.9.21 | Leaflet type definitions |

Leaflet is used to render an interactive delivery radius map (15-mile radius). The map component is dynamically loaded (client-side only) using Next.js `dynamic()` with `ssr: false`.

## Forms & API Integrations

- **Form submission:** External endpoint via `NEXT_PUBLIC_FORM_ENDPOINT` environment variable (Formspree-compatible)
- **Spam protection:** Honeypot field on contact form
- **Fallback behavior:** Simulates success if endpoint is not configured

## Data Management

No database. All data is managed as TypeScript modules in `src/content/`:

| File | Purpose |
|------|---------|
| `products.ts` | Product catalog and pricing tiers |
| `zips.ts` | Zip code–based service area |
| `towns.ts` | Town/municipality data |
| `testimonials.ts` | Customer testimonials |
| `images.ts` | Image asset references |

## Deployment & Hosting

- **Platform:** Cloudflare Workers (static assets via Wrangler)
- **Wrangler config:** `wrangler.toml`
  - Name: `zagwyn`
  - Compatibility date: `2026-04-15`
  - Assets directory: `./out`
- **Architecture:** Fully static — no server runtime required. Compatible with Vercel, Netlify, or any static host.

## SEO & Discoverability

- Next.js Metadata API (per-page meta tags)
- Structured data (JSON-LD)
- `robots.txt`
- `sitemap.xml`

## Code Quality

| Tool | Version | Config |
|------|---------|--------|
| ESLint | 9.39.4 | `.eslintrc.json` (extends `next/core-web-vitals`) |
| eslint-config-next | 15.0.3 | |
| eslint-plugin-react | 7.37.5 | |
| eslint-plugin-react-hooks | 5.2.0 | |
| eslint-plugin-jsx-a11y | 6.10.2 | |
| eslint-plugin-import | 2.32.0 | |

## Type Definitions

| Package | Version |
|---------|---------|
| @types/react | 18.3.12 |
| @types/react-dom | 18.3.1 |
| @types/node | 22.9.0 |
| @types/leaflet | 1.9.21 |

## Project Structure

```
/src
  /app              Next.js App Router pages (about, products, contact, privacy)
  /components       React components (~14 files)
  /lib              Utility functions and site config
  /content          Static data modules
/public             Images, sitemap.xml, robots.txt
```

## NPM Scripts

| Command | Action |
|---------|--------|
| `npm run dev` | Start development server |
| `npm run build` | Build static site |
| `npm start` | Start production server |
| `npm run lint` | Run ESLint |

## Environment Variables

| Variable | Required | Purpose |
|----------|----------|---------|
| `NEXT_PUBLIC_FORM_ENDPOINT` | Yes | Contact form submission URL |

## Testing & CI/CD

- No testing framework configured
- No CI/CD pipeline configured
