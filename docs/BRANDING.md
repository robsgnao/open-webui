# Branding & Visual Identity

Open WebUI supports customizing the visual identity of your instance via environment variables. All branding values are set on the server and served to the front-end through the `/api/config` endpoint.

---

## Environment Variables

| Variable | Description | Default | Example |
|----------|-------------|---------|---------|
| `WEBUI_NAME` | Instance name displayed in the title bar and UI | `Open WebUI` | `My Corp AI` |
| `WEBUI_FAVICON_URL` | URL for the browser tab favicon | `https://openwebui.com/favicon.png` | `https://example.com/favicon.ico` |
| `WEBUI_LOGO_URL` | URL for the application logo (light mode) | *(uses favicon)* | `https://example.com/logo.svg` |
| `WEBUI_LOGO_DARK_URL` | URL for the logo in dark mode | *(uses favicon)* | `https://example.com/logo-dark.svg` |
| `WEBUI_DEFAULT_BACKGROUND_IMAGE_URL` | Default background image for pages | *(none)* | `https://example.com/bg.jpg` |
| `WEBUI_PRIMARY_COLOR` | Primary brand color (any valid CSS color) | `oklch(0.5 0.2 250)` | `#2563eb` |
| `WEBUI_ACCENT_COLOR` | Accent brand color (any valid CSS color) | `oklch(0.6 0.2 180)` | `#06b6d4` |

---

## How to Use

Set any of these environment variables when starting the server:

```bash
docker run -d \
  -p 3000:8080 \
  -e WEBUI_NAME="My Custom Instance" \
  -e WEBUI_FAVICON_URL="https://example.com/favicon.ico" \
  -e WEBUI_LOGO_URL="https://example.com/logo.png" \
  -e WEBUI_LOGO_DARK_URL="https://example.com/logo-dark.png" \
  -e WEBUI_PRIMARY_COLOR="#2563eb" \
  -e WEBUI_ACCENT_COLOR="#06b6d4" \
  ghcr.io/open-webui/open-webui:main
```

Or via a `.env` file:

```env
WEBUI_NAME=My Custom Instance
WEBUI_FAVICON_URL=https://example.com/favicon.ico
WEBUI_LOGO_URL=https://example.com/logo.png
WEBUI_LOGO_DARK_URL=https://example.com/logo-dark.png
WEBUI_DEFAULT_BACKGROUND_IMAGE_URL=https://example.com/background.jpg
WEBUI_PRIMARY_COLOR=oklch(0.4 0.15 270)
WEBUI_ACCENT_COLOR=oklch(0.55 0.18 200)
```

---

## Per-User Customization

Users can also customize their own experience:

- **Chat Background Image**: Upload or enter a URL in *Settings > Interface > Chat Background Image*
- **Theme**: Select from *Settings > General > Theme* (system, dark, light, OLED dark)

The chat background resolution order is:
1. Folder-level background (if a chat folder has one set)
2. User-level background (from user settings)
3. Admin-level default (`WEBUI_DEFAULT_BACKGROUND_IMAGE_URL`)
4. No background (default)

---

## Custom CSS

You can inject custom CSS via the `static/static/custom.css` file (loaded on every page). Brand colors are exposed as CSS custom properties:

```css
/* Use brand colors in your custom CSS */
.my-custom-element {
  color: var(--brand-primary, oklch(0.5 0.2 250));
  border-color: var(--brand-accent, oklch(0.6 0.2 180));
}
```

Tailwind utility classes are also available:
- `text-brand-primary`
- `bg-brand-primary`
- `border-brand-accent`
- `text-brand-accent`
- `bg-brand-accent`

---

## Admin Panel

The current branding configuration is displayed in the **Admin Panel > Settings > Branding** tab. This is a read-only view reflecting the server's environment variable configuration.
