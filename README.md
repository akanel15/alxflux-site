# AlxFlux - Personal Services Hub

A modern, self-hosted personal dashboard built with Astro and deployed via GitHub Actions to Oracle Cloud Infrastructure.

**Live Site:** [alxflux.duckdns.org](https://alxflux.duckdns.org)

## 🏗️ Architecture Overview

```
┌─────────────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│   GitHub Actions   │────│  Oracle Cloud VM │────│   Services Layer    │
│   - Build & Test    │    │  - Caddy Proxy   │    │   - Miniflux RSS   │
│   - Deploy via SSH  │    │  - Static Files   │    │   - Future Services │
└─────────────────────┘    └──────────────────┘    └─────────────────────┘
```

### Infrastructure Stack
- **Frontend**: Astro + Tailwind CSS (Static Site Generation)
- **Hosting**: Oracle Cloud Free Tier VM
- **Reverse Proxy**: Caddy Server
- **CI/CD**: GitHub Actions with SSH deployment
- **Domain**: DuckDNS (alxflux.duckdns.org)

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

### Server Configuration

The production server runs on Oracle Cloud with the following setup:

```
/var/www/alxflux-site/current/    # Static site files
/etc/caddy/Caddyfile              # Reverse proxy config
```

### Caddy Configuration

```caddyfile
alxflux.duckdns.org {
    root * /var/www/alxflux-site/current
    file_server
    
    # Proxy RSS reader to Miniflux
    handle /reader* {
        reverse_proxy 127.0.0.1:8080
    }
}
```

### Automated Deployment

Every push to `main` triggers:
1. Build static site with Astro
2. Deploy via rsync over SSH
3. Reload Caddy configuration
4. Zero-downtime deployment

## 🔧 Services

### Active Services
- **📰 RSS Reader**: Miniflux instance proxied at `/reader`
- **🏠 Landing Page**: Service hub and status dashboard

### Planned Services
- **📁 File Storage**: Personal file sharing
- **📊 Analytics Dashboard**: System monitoring
- **📝 Notes/Wiki**: Personal knowledge base

## 🔐 Security & SSH

- Deployment uses SSH key authentication
- Private keys stored in GitHub Secrets
- Read-only deployment user on server
- Automatic SSL via Caddy

## 🚨 Disaster Recovery

### Backup Strategy
- Server configuration backed up to `/home/ubuntu/backups`
- Git repository contains complete site source
- Database backups (when applicable) automated

### Recovery Steps
1. Restore VM from Oracle Cloud backup
2. Deploy from GitHub: `git push origin main`
3. Restore service data from backups

## 📈 Performance

- **Static Site**: Fast loading with pre-built HTML/CSS/JS
- **CDN Ready**: Optimized assets with Astro build
- **Minimal JS**: Only ships necessary JavaScript
- **Responsive**: Mobile-first design with Tailwind

## 🛠️ Adding New Services

1. **Create New Page**
   ```bash
   # Create src/pages/newservice.astro
   ```

2. **Update Navigation**
   ```astro
   # Add to src/layouts/Layout.astro
   ```

3. **Configure Reverse Proxy**
   ```caddyfile
   # Add to Caddy config
   handle /newservice* {
       reverse_proxy 127.0.0.1:PORT
   }
   ```

4. **Deploy**
   ```bash
   git push origin main
   ```

## 🤝 Contributing

This is a personal project, but feel free to:
- Report issues or suggestions
- Fork for your own setup
- Share improvements

## 📄 License

MIT License - Feel free to use this setup for your own projects!
