# How to make full-stack frameworks work on a platform like Netlify

Slides for Philippe Serhal's talk at [ZurichJS Conf 2026](https://conf.zurichjs.org), September 11, 2026.

The talk builds a fictional hosting platform, ZurichCloud, from static files to full-stack framework support, then explores deployment adapters, the Next.js collaboration, and shared integration APIs in Vite.

Built with [Slidev](https://sli.dev/) and the Seriph theme.

## Run locally

```sh
pnpm install
pnpm dev
```

Open <http://localhost:3030>. The pnpm version is pinned in `package.json`.

## Editing

- [slides.md](./slides.md) configures the deck and imports sections.
- [pages/](./pages/) contains the numbered sections and speaker notes.
- [components/](./components/) contains diagrams and animations.
- [public/](./public/) contains locally embedded images, logos, and GIFs.
- [styles/index.css](./styles/index.css) defines shared styling.

## Commands

```sh
pnpm build         # Build the presentation into dist/
pnpm export        # Export the deck to PDF
pnpm format        # Format with Prettier and its Slidev plugin
pnpm format:check  # Check formatting
```
