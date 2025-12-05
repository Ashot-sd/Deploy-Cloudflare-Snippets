# Deploy Cloudflare Snippets

Automatically deploys every `snippet.js` file found in a folder as a Cloudflare Workers Snippet.

## Expected structure
```
your-repo/
└── domains/              ← or any folder you choose
    ├── analytics/
    │   └── snippet.js
    ├── security/
    │   └── snippet.js
    └── bot-fight/
        └── snippet.js
```

Each subfolder name becomes the snippet name on Cloudflare.

## Usage
```yaml
name: Deploy Snippets
on:
  push:
    branches: [ main, master ]
    paths:
      - 'domains/**/snippet.js'
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Deploy Cloudflare Snippets
        uses: yourusername/deploy-cloudflare-snippets@v1
        with:
          snippets-path: domains
          zone-id: ${{ secrets.CF_ZONE_ID }}
          api-token: ${{ secrets.CF_API_TOKEN }}
```