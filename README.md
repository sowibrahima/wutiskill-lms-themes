# WutiSkill LMS Themes

Multi-tenant theming solution for Open edX LMS platform.

## Structure

```
wutiskill-lms-themes/
├── tenants/
│   ├── wutiskill/              # WutiSkill tenant theme
│   │   ├── tokens/src/         # Design tokens (colors, etc.)
│   │   ├── paragon/            # SCSS and generated CSS
│   │   └── comprehensive/      # HTML template overrides
│   │       └── lms/
│   │           └── templates/
│   │
│   └── tenant1/                # Second tenant theme
│       ├── tokens/src/
│       ├── paragon/
│       └── comprehensive/
│
└── dist/                       # Built CSS output
    ├── wutiskill/
    └── tenant1/
```

## Installation

```bash
npm install
```

## Build

Build all tenants:
```bash
make build
```

Build specific tenant:
```bash
make build-wutiskill
make build-tenant1
```

## Output

After building, each tenant will have in `dist/<tenant>/`:
- `core.css` - Core theme CSS
- `light.css` - Light theme CSS with design tokens

## Deployment

### Design Tokens (MFEs)

Upload `dist/<tenant>/` to your CDN and configure via `MFE_CONFIG`:

```json
{
  "MFE_CONFIG": {
    "PARAGON_THEME_URLS": {
      "core": { "url": "https://cdn.example.com/<tenant>/core.css" },
      "defaults": { "light": "https://cdn.example.com/<tenant>/light.css" }
    }
  }
}
```

### Comprehensive Theme (LMS)

Copy `tenants/<tenant>/comprehensive/` to `/openedx/themes/<tenant>/` in your Open edX instance.

Configure via eox-tenant:
```json
{
  "lms_configs": {
    "THEME_NAME": "<tenant>"
  }
}
```

## Adding a New Tenant

1. Copy an existing tenant folder
2. Update `tokens/src/themes/light/global/color.json` with new colors
3. Update logos and assets
4. Add build scripts to `package.json`
5. Run `make build`
