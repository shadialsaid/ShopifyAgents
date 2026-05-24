# PRD: Content Agent

| Field | Value |
| --- | --- |
| **Product** | ShopifyAgents — Content Agent |
| **Status** | Draft (v0.1) |
| **Last updated** | 2026-05-24 |
| **Owner** | _TBD_ |
| **Reviewers** | _TBD_ |

> This is a **draft** product requirements document. It captures intended scope
> and is informed by the 2026 competitive landscape (see References). Numbers,
> integrations, and milestones are proposals to be validated, not commitments.

---

## 1. Summary

The **Content Agent** is an autonomous AI agent that produces, optimizes, and
maintains on-brand store content for a Shopify merchant: product descriptions,
collection copy, blog posts, landing pages, image alt text, and SEO/metadata.
It is the "what the store says" half of ShopifyAgents (the
[Marketing Agent](./marketing-agent-prd.md) owns "how the store reaches
people").

The agent learns a merchant's brand voice once, then keeps the catalog and
content library fresh — generating new copy, rewriting underperforming pages,
and optimizing for both classic search engines and the emerging class of
AI shopping assistants (Shopify Sidekick, Perplexity, ChatGPT Shopping,
Amazon Rufus) — a discipline now commonly called **Generative Engine
Optimization (GEO)**.

## 2. Background & problem

Merchants spend 15–20 hours/week writing and maintaining content; copy quality
and SEO directly drive organic traffic and conversion. Two shifts make a
dedicated agent valuable in 2026:

1. **Volume & freshness.** Catalogs change constantly (new SKUs, seasonal
   collections, restocks). Manually keeping descriptions, metadata, and blog
   content current does not scale.
2. **Agentic commerce / GEO.** A growing share of discovery happens through AI
   assistants that parse product detail pages to answer complex shopper
   prompts. Content must be structured and explicit enough for machines to
   reason over, not just humans to skim.

Native tools (Shopify Magic, Sidekick) cover point generation well but are
prompt-by-prompt and merchant-driven. Standalone writers (Jasper, Writesonic,
Meetanshi) generate copy but don't autonomously maintain a catalog end-to-end
or close the loop on performance. The Content Agent targets that gap:
**autonomous, brand-consistent, performance-aware content operations.**

## 3. Goals & non-goals

### Goals
- Generate on-brand product descriptions, collection copy, and blog/landing
  content from product data and a learned brand voice.
- Produce SEO + GEO metadata (titles, meta descriptions, structured data,
  alt text) following best practices.
- Detect stale or underperforming content and proactively propose rewrites.
- Keep a human in the loop: draft → review → publish, with bulk approval.
- Be measurable: tie content changes to organic traffic and conversion.

### Non-goals (v1)
- Paid ads, email/SMS campaigns, audience segmentation → owned by the
  [Marketing Agent](./marketing-agent-prd.md).
- Image/video *generation* (may consume merchant assets; generation is a later
  phase).
- Acting as a customer-support chatbot.
- Fully autonomous publishing without any human approval option.

## 4. Target users & personas

- **Solo founder / small team:** wants a full catalog written without hiring a
  copywriter; values speed and "good enough, on-brand" defaults.
- **Marketing/content manager at a scaling brand:** wants leverage and
  consistency across hundreds/thousands of SKUs; values brand controls,
  bulk workflows, and approval gates.
- **SEO/agency operator:** wants GEO-ready structured content and measurable
  organic lift across many client stores.

## 5. Competitive landscape (2026)

| Tool | Strength | Gap the Content Agent addresses |
| --- | --- | --- |
| **Shopify Magic / Sidekick** | Free, native, deep store context; great point generation; meta titles/descriptions, tag suggestions | Prompt-by-prompt and merchant-initiated; not an autonomous, performance-aware operator across the whole catalog |
| **Jasper** | 100+ agents, Brand IQ voice consistency, content pipelines | Not Shopify-native; brand/catalog data must be wired in; no Shopify performance loop |
| **Writesonic** | AI Article Writer, SEO agent, fact-checking | General-purpose; limited Shopify catalog/data integration |
| **Meetanshi AI Content Generator** | Shopify-native bulk descriptions & SEO | Generation-focused; limited autonomy and performance feedback |
| **Stormy AI** | GEO / optimizing PDPs for AI shopping agents | Narrow; the agent should treat GEO as one capability among several |

**Implication:** differentiate on (a) Shopify-native, real-time catalog
awareness, (b) learned-once brand voice applied everywhere, (c) autonomous
detect-rewrite-measure loop, and (d) GEO + classic SEO together.

## 6. Key capabilities (user stories)

1. **Brand voice onboarding** — _As a merchant, I want the agent to learn my
   brand voice from my existing site/content so all output sounds like us._
2. **Product description generation** — _… generate SEO+GEO-optimized
   descriptions from product attributes, in bulk, with variants/options
   reflected._
3. **Collection & landing copy** — _… write collection intros and landing-page
   copy aligned to a campaign or theme._
4. **Blog & editorial** — _… draft on-topic, keyword-targeted blog posts with
   internal links to relevant products/collections._
5. **Metadata & structured data** — _… auto-generate meta titles/descriptions,
   alt text, and product structured data for SEO and AI-assistant parsing._
6. **Content health & rewrites** — _… flag thin, stale, duplicate, or
   underperforming content and propose rewrites ranked by expected impact._
7. **Review & publish workflow** — _… review drafts, edit inline, and bulk
   approve/publish (or schedule), with full change history and rollback._
8. **Localization (later phase)** — _… translate/transcreate content for
   additional markets while keeping voice and SEO intent._

## 7. Functional requirements

- **FR-1** Ingest products, variants, collections, pages, blog articles, and
  existing metadata from the connected store.
- **FR-2** Build and persist a **Brand Voice profile** (tone, vocabulary,
  do/don't lists, reading level, example snippets) editable by the merchant.
- **FR-3** Generate content for a single item, a selected set, or the whole
  catalog (bulk jobs with progress + partial results).
- **FR-4** Produce SEO assets (title, meta description within length limits,
  alt text) and GEO-friendly structured/explicit attributes.
- **FR-5** Maintain a **draft → review → publish** state machine; never
  overwrite live content without an approval step (configurable auto-publish
  per content type once trust is established).
- **FR-6** Track provenance: which model/version/prompt produced each artifact,
  and full version history with rollback.
- **FR-7** Run a scheduled **content audit** that scores items and queues
  rewrite suggestions.
- **FR-8** Surface performance: connect content changes to organic
  traffic/ranking/conversion signals.

## 8. Non-functional requirements

- **Brand safety:** no fabricated claims, specs, or compliance/medical/legal
  assertions; respect a configurable banned-claims list; cite source attributes
  for factual statements where possible.
- **Human control:** approval gates by default; clear undo; audit log.
- **Performance:** bulk generation for large catalogs runs as resumable
  background jobs; per-item generation feels interactive.
- **Cost/observability:** track token/$ per job; expose run logs and metrics.
- **Privacy/compliance:** handle merchant/customer data per Shopify API terms
  and applicable data-protection rules.

## 9. Agent architecture (proposed, to validate)

- **Inputs:** Shopify Admin API (products, collections, pages, blogs,
  metafields), merchant brand assets, analytics/SEO signals.
- **Core:** LLM-driven planner/executor with tools for fetch, generate,
  validate (claims/length/SEO), diff, and publish. Brand Voice profile injected
  as system context; retrieval over existing content for consistency.
- **Outputs:** drafts written back via Admin API / metafields after approval;
  structured data for PDPs.
- **Human-in-the-loop:** review queue UI; bulk approve; scheduling.
- **Shared services with Marketing Agent:** brand voice store, asset library,
  auth/connection to the store, analytics layer.

> Tech stack (language, framework, hosting, model providers) is **not yet
> chosen** — see repo `CLAUDE.md`. This section describes intent, not a
> committed design.

## 10. Success metrics

- **Coverage:** % of catalog with agent-generated, approved descriptions &
  complete metadata.
- **Organic lift:** change in organic sessions / impressions for optimized
  pages over 3–6 months (industry reports cite 30–50% organic traffic lift
  ranges — to be validated for our cohort).
- **Conversion:** PDP conversion rate on optimized vs. control pages.
- **GEO presence:** rate at which products surface in AI-assistant results for
  target prompts.
- **Efficiency:** merchant content hours saved; cost per published artifact.
- **Quality/trust:** edit rate before approval; rollback rate; auto-publish
  adoption over time.

## 11. Risks & mitigations

| Risk | Mitigation |
| --- | --- |
| Hallucinated specs/claims damage trust or compliance | Constrain to known product attributes; banned-claims list; validation pass; human approval |
| Brand voice feels generic / off | Strong onboarding, example-driven voice profile, edit-feedback loop |
| Native Shopify Magic "good enough" for many merchants | Differentiate on autonomy, catalog-wide maintenance, and performance loop |
| Bulk publishing breaks live store / SEO | Staged rollout, approval gates, versioning + rollback |
| GEO is a moving target | Treat as configurable capability; monitor assistant behavior and adapt |

## 12. Milestones (proposed)

- **M0 — Discovery:** confirm stack, Shopify app scaffolding, auth/connection.
- **M1 — Brand voice + single-item generation:** onboarding + PDP copy with
  review.
- **M2 — Bulk + SEO/GEO metadata:** catalog-wide jobs, metadata, structured
  data.
- **M3 — Content audit & rewrites:** scoring, suggestions, performance hookup.
- **M4 — Blog/editorial + scheduling;** **M5 — localization.**

## 13. Open questions

- What model provider(s) and budget envelope per merchant?
- Build as an embedded Shopify app, external dashboard, or both?
- How much autonomy will merchants tolerate before requiring approval?
- Which analytics source is authoritative for the performance loop?
- Scope of localization in v1 vs. later?

## 14. References

- [Shopify Magic and Sidekick: AI for Commerce](https://www.shopify.com/magic)
- [Optimizing Shopify Product Descriptions for AI Shopping Agents: 2026 GEO Guide (Stormy AI)](https://stormy.ai/blog/optimizing-shopify-descriptions-ai-shopping-agents-2026)
- [Shopify AI SEO Content Guide (EasyApps)](https://easyappsecom.com/guides/shopify-ai-seo-content-guide.html)
- [Meetanshi AI Content Generator (Shopify App Store)](https://apps.shopify.com/ai-product-description-articles)
- [Best AI SEO Tools (Shopify Blog)](https://www.shopify.com/blog/ai-seo-tools)
- [Shopify Magic & Sidekick 2026 review (AdsX)](https://www.adsx.com/blog/shopify-magic-sidekick-ai-features-2026)
- [Put AI agents to work for marketing (Jasper)](https://www.jasper.ai/)
- [13 Best AI Agents for Content Creation 2026 (ClickUp)](https://clickup.com/blog/ai-agents-for-content-creation/)
- [Top E-commerce AI Agents 2026 (AIMultiple)](https://research.aimultiple.com/ecommerce-ai-agent/)
