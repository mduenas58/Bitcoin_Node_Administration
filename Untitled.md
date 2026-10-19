I'll inspect the site directly to fingerprint the stack.

The shell proxy blocked that. Let me use the web tools instead.

Strong fingerprints there. Let me confirm against the repository.

Branch is `master`, not `main` — refetching.

Confirmed. Let me check what's current before recommending versions.

## The stack

**Nextra** — a documentation framework built on Next.js. Confirmed from the repo rather than inferred:

```json
{
  "name": "theroadtonode",
  "version": "4.1.1",
  "dependencies": {
    "next": "^12.3.2",
    "nextra": "^1.1.0",
    "nextra-theme-docs": "^1.2.6",
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  }
}
```

And the i18n wiring in `next.config.js`:

```js
const withNextra = require("nextra")("nextra-theme-docs", "./theme.config.js");

module.exports = withNextra({
  i18n: { locales: ['en', 'nl'], defaultLocale: 'en' }
});
```

So: **Nextra 1.x with `nextra-theme-docs`, bilingual English/Dutch, content as `.mdx` files in `pages/`, hosted from GitHub, MIT licensed.** The fingerprints visible from the browser were `meta-next-head-count` (Next.js Pages Router), the `pages/index.en.mdx` edit link, and the "Edit this page on GitHub" footer.

**Don't copy their versions.** That repo is pinned to Next.js 12 and React 17 — released in 2021, both long out of support. Current is [Nextra 4, which moved to the App Router](https://the-guild.dev/blog/nextra-4). Build fresh on 4.

---

## Why this is the right call for you

Setting aside that it's the obvious reference, Nextra fits your situation unusually well:

- **Content is Markdown in git.** You're a sysadmin. Writing `.mdx` files and pushing commits is more natural to you than any CMS admin panel, and it means no database, no WordPress patching, no attack surface.
- **i18n is built in.** Your whole differentiator is Spanish. Nextra's locale routing (`.es.mdx` / `.en.mdx`) is exactly the mechanism theroadtonode uses for Dutch, and it costs you nothing to set up.
- **It exports to static files.** Which matters more than it sounds — see below.
- **"Edit this page on GitHub"** turns readers into contributors. That's how a solo guide becomes a community project.

### The thing worth noticing

This site is the English/Dutch version of the Spanish-language gap we identified in your roadmap. A bilingual, professional-grade Bitcoin node guide in Spanish does not meaningfully exist. Building it is simultaneously your content marketing, your credibility proof, your lead generation, and your sales collateral — the same artifact doing four jobs.

And one detail you should exploit: **self-host it on your own node.** `next build` with static export gives you plain HTML/CSS/JS that Caddy serves from the hardware in your lab. A Bitcoin sovereignty consultant whose own site runs on Vercel is making an argument he doesn't follow himself. One whose site is served from his own box, over his own connection, with a Tor onion address alongside it, has a demo he can point at in every sales conversation. Keep a Cloudflare Pages mirror for uptime.

---

## Honest alternatives

Nextra isn't the only good answer, and I'd rather you pick deliberately:

|Framework|Stack|Case for it|Case against|
|---|---|---|---|
|**Nextra 4**|Next.js / React|Matches the reference; good i18n; big ecosystem|React/Next.js churn — you'll hit breaking changes between majors|
|**Astro Starlight**|Astro|Excellent i18n, ships almost no JS, fastest builds, very stable|Smaller ecosystem; different from your reference|
|**Docusaurus**|React / Meta|Most mature i18n, versioning, huge community|Heavier, more opinionated, more config|
|**MkDocs Material**|Python|Dead simple, YAML config, you already know Python|Less flexible, more obviously "a docs site"|

If you want to deviate from the reference, **Astro Starlight** is the one I'd actually look at. It produces a lighter site, has first-class i18n, and has far less framework churn than the Next.js world — which matters when you're maintaining this alone for years. For a content site with no app-like interactivity, shipping less JavaScript is a straightforward win.

That said, going with Nextra means your reference implementation is sitting right there in a readable MIT-licensed repo whenever you're stuck. That's worth something real when you're learning.

---

## How to proceed

**1. Get it running locally, today**

```bash
# Node 20+ required
npx create-next-app@latest roadmap-nodo --typescript --app --no-tailwind
cd roadmap-nodo
npm install nextra@latest nextra-theme-docs@latest
```

Then follow the Nextra 4 docs for the App Router setup — `next.config.mjs`, `app/layout.tsx`, and a `content/` directory. Start with their starter rather than hand-assembling it.

**2. Study the reference properly**

```bash
git clone https://github.com/harrybawsac/theroadtonode
```

Read `theme.config.js` and the structure of `pages/`. Note how `_meta.json` controls sidebar ordering and how the `.en` / `.nl` suffixes map to locales. Don't port the code — port the _information architecture_. Their section ordering (hardware → OS → Core → Core extensions → Lightning → Lightning extensions → wallets) is a well-tested teaching sequence and you'd be reinventing it badly.

**3. Decide the language strategy before you write anything**

Spanish-first with English second is the correct order for you, and it's the inverse of how most projects do it. Set `defaultLocale: 'es'`. Changing this later means rewriting every file path.

**4. Write one page end to end**

Pick the single page you know best — installing Bitcoin Core from source with signature verification — and take it all the way to published. You'll hit every problem the project has (code blocks, callouts, images, navigation, deployment) on one page instead of forty.

**5. Deploy early and ugly**

Push to Cloudflare Pages or Vercel in week one, with three pages and rough edges. A live URL you're embarrassed by is worth more than a perfect local build, because it forces the deployment problems to surface while the site is small.

**6. Then self-host it**

Once the build pipeline is stable, add the deploy to your own hardware: `next build` → static output → Caddy with automatic TLS → Tailscale for admin access. Write up _that_ process as a page on the site itself. It's genuinely useful content and it demonstrates the exact skill you're selling.

---

## Two cautions

**Scope.** Theroadtonode covers Pi hardware, Tor, firewalls, Core, Electrs, mempool.space, LND, RTL, Thunderhub, Lightning Terminal, and wallets. That's a multi-year volume of writing. Launch with a narrow, complete spine — hardware, OS hardening, Core, one Electrum server — and expand. A finished small guide beats an abandoned comprehensive one.

**Maintenance is the real cost.** Node software versions move constantly; a guide pinned to Bitcoin Core 28 reads as abandoned by the time 32 ships. Build version-checking into your routine from the start, and put a visible "last verified against Core vX, date Y" line on every technical page. That line is also a trust signal — it tells a reader you actually ran this recently.

---

Want me to scaffold the project structure — `next.config.mjs`, theme config, locale setup, and a Spanish/English page skeleton with the section tree already laid out?

**Sources:** [Nextra 4 x App Router — migration guide](https://the-guild.dev/blog/nextra-4) · [harrybawsac/theroadtonode](https://github.com/harrybawsac/theroadtonode)