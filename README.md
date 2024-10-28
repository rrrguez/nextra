# Nextra

Simple, powerful and flexible site generation framework with everything you love
from Next.js.

## Documentation

https://nextra.site

## Development

### Installation

Worked with node v22.2.0 but not with v23.0.0:

```
➜  nextra-theme-docs git:(casiano) ✗ node --version
v22.2.0
```

The Nextra repository uses [PNPM Workspaces](https://pnpm.io/workspaces) and
[Turborepo](https://github.com/vercel/turborepo). To install dependencies, run
`pnpm install` in the project root directory.

### Build Nextra Core

```bash
cd packages/nextra
pnpm build
```

Watch mode: `pnpm dev`

### Build Nextra Theme

```bash
cd packages/nextra-theme-docs
pnpm build
```

| Command           | Description              |
| ----------------- | ------------------------ |
| pnpm dev          | Watch mode               |
| pnpm dev:layout   | Watch mode (layout only) |
| pnpm dev:tailwind | Watch mode (style only)  |

### Development

1. Set `nvm use v22`. I went to the `packages/nextra` directory and run `pnpm dev`. It uses [tsup](https://tsup.egoist.sh/) to bundle the code.
2. I opened a new terminal; set `nvm use v22` and then went to the `packages/nextra-theme-docs` directory and run `pnpm dev`. It concurrently runs `tsup --watch` and `TAILWIND_MODE=watch pnpm postcss css/styles.css -o dist/style.css --watch`.

  ```bash
  ➜  nextra git:(casiano) ✗ cd packages/nextra-theme-docs 
  ➜  nextra-theme-docs git:(casiano) ✗ jq '.scripts' package.json 
  ```
  ```json 
  {
    "build": "tsup",
    "build:all": "pnpm build && pnpm build:tailwind",
    "build:tailwind": "pnpm postcss css/styles.css -o dist/style.css --verbose",
    "clean": "rimraf ./dist ./style.css",
    "dev": "concurrently \"pnpm dev:layout\" \"pnpm dev:tailwind\"",
    "dev:layout": "tsup --watch",
    "dev:tailwind": "TAILWIND_MODE=watch pnpm postcss css/styles.css -o dist/style.css --watch",
    "prepublishOnly": "pnpm build:all",
    "test": "vitest run",
    "types": "tsup --dts-only",
    "types:check": "tsc --noEmit"
  }
  ```
3. I opened a new terminal; set `nvm use v22` and then went to `examples/docs` and run:

  ```bash
  cd examples/docs
  pnpm dev
  ```

  Any changes to `example/docs` will be re-rendered instantly.

Here we have used the watch mode for both nextra and the theme in separated terminals.
Otherwise, if you update the core or theme packages, a rebuild is required. 


It worked!

```
➜  docs git:(casiano) ✗ pnpm dev

> example-docs@ dev /Users/casianorodriguezleon/campus-virtual/2223/learning/nextjs-learning/nextra-learning/nextra/examples/docs
> next

 ⚠ Port 3000 is in use, trying 3001 instead.
 ⚠ Port 3001 is in use, trying 3002 instead.
 ⚠ Port 3002 is in use, trying 3003 instead.
  ▲ Next.js 15.0.1
  - Local:        http://localhost:3003

 ✓ Starting...
   automatically enabled Fast Refresh for 2 custom loaders
 ✓ Ready in 4.5s
 ```

### Sponsors

<div>
 <a href="https://the-guild.dev/graphql/hive?utm_source=github&utm_campaign=nextra&utm_content=logolink">
   <img src="/docs/pages/showcase/graphql-hive.png" alt="GraphQL Hive preview" width="256">
 </a>
 <a href="https://speakeasyapi.dev/docs?utm_source=github&utm_campaign=nextra&utm_content=logolink">
   <img src="/docs/pages/showcase/speakeasy.png" alt="Speakeasy preview" width="256">
 </a>
 <a href="https://xyflow.com?utm_source=github&utm_campaign=nextra&utm_content=logolink">
   <img src="/docs/pages/showcase/xyflow.jpg" alt="xyflow preview" width="256">
 </a>
</div>
