<!-- Copilot instructions for contributors/AI agents. Keep short, actionable, and specific to this repo. -->
# Repository orientation — astro-blog-lu

This is an Astro-based static blog scaffold configured for Cloudflare Workers. Use these notes to be productive quickly when editing, adding content, or changing site behavior.

Key facts (big picture)
- Framework: Astro (v5.x). Pages/components live under `src/pages`, `src/components`, `src/layouts`.
- Content: Markdown/MDX blog posts live in `src/content/blog/` and are surfaced with `astro:content` (`getCollection`, `render`). See `src/content.config.ts` for the collection schema (title, description, pubDate, updatedDate, heroImage).
- Deployment target: Cloudflare Workers via `@astrojs/cloudflare` adapter and `wrangler`.

Useful scripts (run from repo root)
- npm install — install deps
- npm run dev — local dev server (Astro) at :4321
- npm run build — production build (outputs `./dist/`)
- npm run preview — build + run wrangler dev to preview on Workers runtime
- npm run check — builds + tsc + `wrangler deploy --dry-run` (fast health check for type/schema mismatches)

Files you’ll use often
- `package.json` — scripts and important deps (astro, wrangler, mdx, sitemap, rss)
- `astro.config.mjs` — site, integrations, and Cloudflare adapter options
- `src/content.config.ts` — collection definitions and zod schema for frontmatter validation
- `src/pages/blog/[...slug].astro` — shows how posts are routed and rendered using `render(post)` and `BlogPost` layout
- `src/layouts/BlogPost.astro` — canonical blog layout; consumes frontmatter fields like `pubDate`, `heroImage`
- `src/pages/blog/index.astro` — example listing page; sorts posts by `pubDate` and uses `post.id` for links
- `src/pages/rss.xml.js` — RSS generation using `@astrojs/rss` and `getCollection('blog')`
- `src/components/BaseHead.astro` — canonical head/meta patterns (uses `Astro.site` and `Astro.url`) — update carefully.

Project-specific conventions and patterns
- Content schema: frontmatter is validated by `src/content.config.ts` using `z.coerce.date()` for `pubDate` and `updatedDate`. When adding posts, use parsable date strings (ISO or YYYY/MM/DD used in examples).
- Permalinks: pages use `post.id` returned by `getCollection('blog')`. Link to posts as `/blog/${post.id}/`.
- Hero images: frontmatter uses `heroImage` with a path under `public/` (example: `/1111.png`).
- Locale: some pages/layouts use `lang="zh-cn"` for output; content may be Chinese — keep encoding and meta consistent.

Integration notes / gotchas
- `wrangler` is a dev dependency; wrangler commands require Cloudflare account config to deploy. Use `npm run preview` or `npm run deploy` only when you intend to test on Workers. `npm run check` uses `wrangler deploy --dry-run` for validation without publishing.
- `astro build` produces static assets in `./dist/` for static hosting; with the Cloudflare adapter the build targets Workers runtime and may use `wrangler dev` to emulate.
- If changing frontmatter schema in `src/content.config.ts`, expect TypeScript and content collection errors; run `npm run check` to validate.

Examples (copyable patterns)
- Get and sort posts in a page:

  const posts = (await getCollection('blog')).sort((a,b) =&gt; b.data.pubDate.valueOf() - a.data.pubDate.valueOf());

- Render a blog post page (from `src/pages/blog/[...slug].astro`):

  const { Content } = await render(post);
  <BlogPost {...post.data}>
    <Content />
  </BlogPost>

Editing guidance for AI agents
- When editing layout or head components, preserve use of `Astro.site` and `Astro.url` in `BaseHead.astro` to keep canonical URLs correct.
- When adding new content fields, update `src/content.config.ts` first and run `npm run check`.
- Avoid changing routing conventions: post routes rely on `post.id` and the dynamic `[...slug].astro` page. If you add a custom slug, update the `getStaticPaths` mapping.

Where to look next
- `src/components/*` for UI primitives, `src/layouts/*` for structure, `src/pages/*` for routes.
- `public/` for static assets (images referenced by frontmatter).

If anything above is unclear or incomplete, tell me which area you want expanded (build, deploy, content schema, routing examples) and I’ll iterate.
