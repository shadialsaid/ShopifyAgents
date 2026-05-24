# PRD: Marketing Agent

| Field | Value |
| --- | --- |
| **Product** | ShopifyAgents — Marketing Agent |
| **Status** | Draft (v0.1) |
| **Last updated** | 2026-05-24 |
| **Owner** | _TBD_ |
| **Reviewers** | _TBD_ |

> This is a **draft** product requirements document. It captures intended scope
> and is informed by the 2026 competitive landscape (see References). Numbers,
> integrations, and milestones are proposals to be validated, not commitments.

---

## 1. Summary

The **Marketing Agent** is an autonomous AI agent that plans, builds, runs, and
optimizes a Shopify merchant's lifecycle marketing across owned channels —
email, SMS, WhatsApp/RCS, mobile push, and on-site — driven by real-time store
and customer data. It is the "how the store reaches people" half of
ShopifyAgents; the [Content Agent](./content-agent-prd.md) owns "what the store
says."

It learns the brand from the store, stands up the foundational retention flows
(welcome, abandoned checkout, post-purchase, win-back), builds and schedules
campaigns, segments audiences, and continuously optimizes based on revenue —
keeping a human in the loop for approvals and spend.

## 2. Background & problem

Owned-channel lifecycle marketing (email + SMS) is consistently the highest-ROI
retention lever for Shopify brands, but it's operationally heavy: building
flows, segmenting audiences, writing/scheduling campaigns, and reading results.
In 2026 the leading platforms (notably **Klaviyo**) have shipped autonomous
"marketing agent" experiences that learn from a store and build on-brand
campaigns and flows in minutes — raising merchant expectations that marketing
should largely run itself, with humans steering rather than operating.

The opportunity for ShopifyAgents' Marketing Agent: an agent that is
**store-native, revenue-aware, multi-channel, and autonomous by default with
human guardrails** — and that shares brand voice and assets with the Content
Agent so messaging is consistent across the funnel.

## 3. Goals & non-goals

### Goals
- Connect to a store and **auto-build foundational lifecycle flows** + a first
  signup form within minutes of onboarding.
- Plan and execute **campaigns** (email/SMS) on a calendar, on-brand.
- Build and maintain **audience segments** from real-time behavioral + purchase
  data.
- **Optimize** continuously (send time, subject/variant testing, channel mix)
  against revenue/engagement goals.
- Keep humans in control: approval gates, spend caps, clear reporting.

### Non-goals (v1)
- Writing long-form store/product content → owned by the
  [Content Agent](./content-agent-prd.md) (Marketing Agent *requests/consumes*
  copy from it).
- Paid media buying (ads) in v1 — candidate for a later phase.
- Full customer-support automation (a separate "Customer/Support Agent").
- Replacing the merchant's judgment on brand, offers, and budget.

## 4. Target users & personas

- **Solo founder / small team:** wants retention marketing "set up for me" and
  running without a marketer on staff.
- **Retention/lifecycle marketer at a scaling brand:** wants leverage —
  agent drafts flows, segments, and campaigns; they approve and refine.
- **Agency operator:** wants to stand up and optimize many client programs
  consistently and measurably.

## 5. Competitive landscape (2026)

| Tool | Strength | Gap the Marketing Agent addresses |
| --- | --- | --- |
| **Klaviyo (Marketing Agent + Customer Agent)** | Deepest Shopify integration; CDP + real-time signals; autonomous campaign/flow building; email/SMS/WhatsApp/RCS/push | Premium pricing/complexity; opportunity for tighter shared brand voice/assets with a content agent and simpler guided autonomy |
| **Omnisend** | Simpler, affordable for smaller brands | Less advanced segmentation/automation and weaker autonomy |
| **Shopify Magic / Sidekick** | Free, native; can draft email content and surface next steps (Sidekick Pulse) | Not a full multi-channel lifecycle automation engine |
| **Postscript / Attentive (SMS), Triple Whale (analytics)** | Channel/analytics depth | Point solutions; agent should orchestrate across channels and tie to revenue |
| **OpenClaw / operational agents** | Ops execution, SEO, inventory | Not retention-marketing focused; complementary |

**Implication:** differentiate on (a) store-native real-time data, (b) shared
brand voice/assets with the Content Agent for consistent funnel messaging,
(c) guided autonomy with strong guardrails, and (d) clear revenue attribution.
A realistic 2026 posture is **interoperate with Klaviyo where merchants already
use it**, while offering a simpler native path for those who don't.

## 6. Key capabilities (user stories)

1. **One-click onboarding** — _As a merchant, I want the agent to learn my brand
   from my site and stand up core flows + a signup form automatically._
2. **Lifecycle flows** — _… have welcome, abandoned-cart/checkout, browse
   abandonment, post-purchase, replenishment, and win-back flows created and
   kept current._
3. **Campaign planning & execution** — _… get a proposed campaign calendar
   (promos, launches, seasonal) and have the agent draft, schedule, and send
   on approval._
4. **Audience segmentation** — _… auto-build segments (VIPs, lapsing, first-time
   vs. repeat, high-AOV, category affinity) from live data._
5. **Multi-channel orchestration** — _… coordinate email + SMS (and later
   WhatsApp/RCS/push) so customers aren't over-messaged._
6. **Optimization & experimentation** — _… run send-time, subject-line, and
   creative A/B tests and shift toward what drives revenue._
7. **Reporting & insights** — _… see revenue per channel/flow/campaign and
   plain-language "what to do next" recommendations._
8. **Compliance & deliverability** — _… stay compliant (consent, unsubscribe,
   SMS regulations) and protect sender reputation/deliverability._

## 7. Functional requirements

- **FR-1** Connect store + sync real-time data (customers, orders, checkouts,
  browse/cart events, products) for triggers and segmentation.
- **FR-2** Provision foundational **flows** from templates, personalized to the
  brand, with merchant review before activation.
- **FR-3** Generate **campaign drafts** (subject, preview, body, SMS copy)
  using the shared **Brand Voice profile**; request long-form copy/assets from
  the Content Agent.
- **FR-4** Build, save, and auto-refresh **segments** with transparent rules.
- **FR-5** **Schedule/send** with approval gates; enforce send-frequency caps
  and channel coordination to prevent fatigue.
- **FR-6** **Experimentation engine:** define, run, and read A/B tests;
  auto-promote winners (configurable).
- **FR-7** **Attribution & reporting:** revenue and engagement by
  channel/flow/campaign/segment; exportable.
- **FR-8** **Consent & compliance** management (opt-in/opt-out, unsubscribe,
  quiet hours, regional SMS/email rules) and deliverability safeguards.

## 8. Non-functional requirements

- **Human control & spend safety:** approvals before first send of a new
  flow/campaign; configurable autonomy; send-volume/frequency caps; clear undo.
- **Real-time:** behavioral triggers fire promptly (near real-time event
  handling).
- **Deliverability:** warmup, list hygiene, bounce/complaint handling,
  authentication (SPF/DKIM/DMARC) where applicable.
- **Reliability:** scheduled sends are durable and idempotent (no double-sends).
- **Privacy/compliance:** consent-first; GDPR/CCPA/CAN-SPAM/TCPA-aware; respect
  Shopify API terms and marketing-consent data.
- **Observability/cost:** per-run logs, token/$ tracking, audit trail of agent
  actions.

## 9. Agent architecture (proposed, to validate)

- **Inputs:** Shopify Admin API + webhooks (orders, checkouts, customers,
  carts), customer profiles/consent, engagement events, optional CDP.
- **Core:** planner/executor with tools to segment, draft (via shared brand
  voice), build flows, schedule/send, run experiments, and read analytics. A
  policy layer enforces guardrails (frequency caps, consent, spend, approvals).
- **Channels:** email + SMS in v1; WhatsApp/RCS/push later — via an Email/SMS
  Service Provider or platform integration (build-vs-integrate decision below).
- **Shared services with Content Agent:** brand voice store, asset library,
  store connection/auth, analytics layer.

> Tech stack and the **build-your-own-sending-infra vs. integrate an
> ESP/Klaviyo** decision are **open** — see Open questions and repo `CLAUDE.md`.

## 10. Success metrics

- **Owned-channel revenue** and **% of total revenue** attributed to
  email/SMS (retention marketing is widely cited as the highest-ROI channel —
  validate target ROI for our cohort).
- **Flow coverage & activation:** core flows live within onboarding window.
- **Engagement:** open/click/conversion and revenue per send by channel.
- **List growth & health:** subscriber growth, opt-out and complaint rates,
  deliverability/inbox placement.
- **Autonomy adoption:** share of flows/campaigns running with auto-promote /
  reduced manual steps over time.
- **Efficiency:** merchant marketing hours saved; cost per incremental dollar.

## 11. Risks & mitigations

| Risk | Mitigation |
| --- | --- |
| Over-messaging / list fatigue / spam complaints | Frequency caps, channel coordination, consent + quiet hours, deliverability monitoring |
| Sending wrong/off-brand message at scale | Approval gates, brand-voice constraints, staged rollout, idempotent sends |
| Regulatory non-compliance (TCPA/GDPR/CAN-SPAM) | Consent-first design, region-aware rules, auditable opt-in/out |
| Klaviyo's incumbency & deep integration | Interoperate with Klaviyo; differentiate on shared brand voice, guided autonomy, simplicity |
| Attribution disputes | Transparent methodology; holdout/control groups where feasible |

## 12. Milestones (proposed)

- **M0 — Discovery:** confirm stack; channel build-vs-integrate decision;
  Shopify app + auth.
- **M1 — Onboarding + core flows (email):** brand learn, welcome / abandoned
  checkout / post-purchase with review.
- **M2 — Segmentation + campaigns + reporting:** live segments, campaign
  calendar, revenue attribution.
- **M3 — SMS + experimentation engine + frequency governance.**
- **M4 — WhatsApp/RCS/push;** **M5 — advanced autonomy & optimization
  (auto-promote, predictive send time/audiences).**

## 13. Open questions

- **Build vs. integrate:** run our own email/SMS sending infrastructure, or
  integrate an ESP/SMS provider — or sit on top of Klaviyo where merchants
  already use it?
- Model provider(s) and per-merchant budget envelope?
- Default autonomy level before requiring approval (per channel/action)?
- Authoritative attribution model and analytics source of truth?
- v1 channel scope (email-only vs. email+SMS) and target geographies/regulatory
  scope?

## 14. References

- [Klaviyo: AI Email Marketing & SMS](https://www.klaviyo.com/)
- [Klaviyo: Email Marketing & SMS (Shopify App Store)](https://apps.shopify.com/klaviyo-email-marketing)
- [Klaviyo AI for Shopify: Complete Review 2026 (StoreStackAI)](https://storestackai.com/klaviyo-ai-for-shopify-review/)
- [Top Shopify Marketing Apps for Scaling Brands 2026 (Lebesgue)](https://lebesgue.io/growth/shopify-marketing-apps-2026)
- [13 AI Marketing Automation Tools 2026 (Toolworthy)](https://www.toolworthy.ai/blog/best-ai-marketing-automation-tools)
- [OpenClaw vs Klaviyo: Shopify Marketing Automation Stack 2026 (Stormy AI)](https://stormy.ai/blog/openclaw-vs-klaviyo-shopify-marketing-automation-2026)
- [Shopify Magic and Sidekick: AI for Commerce](https://www.shopify.com/magic)
- [Shopify Sidekick 2026: features & agentic commerce (Presta)](https://wearepresta.com/shopify-sidekick-features-2026-the-merchants-guide-to-agentic-commerce/)
- [Top E-commerce AI Agents 2026 (AIMultiple)](https://research.aimultiple.com/ecommerce-ai-agent/)
