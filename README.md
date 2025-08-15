# AlxFlux - Personal Lab

**Live Sites:**
- [alxflux.duckdns.org](https://alxflux.duckdns.org) - RSS Reader (Miniflux)
- [alxflux.duckdns.org/home](https://alxflux.duckdns.org/home) - Dashboard

## Stack
- **Frontend**: Astro + Tailwind CSS
- **Hosting**: Oracle Cloud Free Tier VM
- **Proxy**: Caddy Server
- **Deploy**: GitHub Actions + SSH
- **Domain**: DuckDNS

## 🚀 Project Structure

```text
alxflux-site/
├── src/
│   ├── layouts/
│   │   └── Layout.astro          # Main site layout
│   ├── pages/
│   │   ├── index.astro           # Landing page
│   │   └── reader.astro          # RSS Reader (proxied)
│   └── styles/
│       └── global.css            # Tailwind CSS
├── public/
│   └── favicon.svg
├── .github/
│   └── workflows/
│       └── deploy.yml            # CI/CD pipeline
└── dist/                         # Build output
```

## 🧞 Local Development

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Install dependencies                            |
| `npm run dev`             | Start dev server at `localhost:4321`           |
| `npm run build`           | Build production site to `./dist/`             |
| `npm run preview`         | Preview build locally before deploying         |
| `npm run astro add`       | Add Astro integrations                          |

### Development Workflow

1. **Local Development**
   ```bash
   npm run dev
   # Opens http://localhost:4321
   ```

2. **Testing Build**
   ```bash
   npm run build
   npm run preview
   ```

3. **Deploy**
   ```bash
   git add .
   git commit -m "Your changes"
   git push origin main
   # GitHub Actions handles the rest!
   ```

## 🌐 Production Deployment

## URLs
- **/** - RSS Reader (Miniflux)
- **/home** - Dashboard

## Deploy
Push to `main` branch. GitHub Actions builds and deploys automatically.

## Services
- RSS Reader (Miniflux) - Main service at root URL
- Dashboard - Personal lab homepage
