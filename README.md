# Raj Oracle — Technical Learning Blog

A public learning blog about Python, AI, data engineering, and DevOps.

## Stack

Astro, TypeScript, Markdown/MDX, and CSS.
Static hosting: Cloudflare Pages.

## Local development

Install dependencies: `npm ci`
Start the background dev server: `npm run astro -- dev --background`
Check server status: `npm run astro -- dev status`
Stop the server: `npm run astro -- dev stop`
Build: `npm run build`
Preview the build: `npm run preview`

## Writing articles

Add Markdown files to `src/content/blog/`.

Required metadata: title, description, pubDate.
Optional metadata: updatedDate, heroImage, tags, draft.

Posts marked `draft: true` are excluded from article routes,
listings, Topics, and RSS. Files committed to a public repository
remain publicly readable.

## Deployment

Production branch: master
Build command: npm run build
Output directory: dist

Set the production URL in astro.config.mjs before the public launch.

## Credits

Created from the official Astro blog starter.
The starter styling includes CSS based on Bear Blog.
