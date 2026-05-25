# PRD: Data Agent

| Field | Value |
| --- | --- |
| **Product** | ShopifyAgents — Data Agent |
| **Status** | Draft (v0.1) |
| **Last updated** | 2026-05-24 |
| **Owner** | _TBD_ |
| **Reviewers** | _TBD_ |

> This is a **draft** product requirements document. It captures intended scope
> and is informed by the 2026 competitive landscape (see References). Numbers,
> integrations, and milestones are proposals to be validated, not commitments.

---

## 1. Summary

The **Data Agent** is the analytical brain of ShopifyAgents. It unifies a
merchant's store data — sales, inventory, customer profiles, marketing
performance, and on-site behavior — then continuously **analyzes** it,
proactively **surfaces insights, anomalies, and opportunities**, **forecasts**
(demand, revenue, churn, LTV), and turns each finding into a concrete
**recommendation with a suggested action**.

Crucially, it doesn't stop at dashboards. The Data Agent **closes the loop**:
recommended actions are routed to the agent best suited to execute them —
content changes to the [Content Agent](./content-agent-prd.md), campaigns and
segments to the [Marketing Agent](./marketing-agent-prd.md), or operational
actions (reorder, price change, bundle) executed directly via the Shopify Admin
API — always under merchant-configured guardrails and approval. In effect the
Data Agent is the **orchestrator** of the agent suite: it decides *what should
happen and why*, while the other agents handle *how*.

## 2. Background & problem

Merchants sit on rich data spread across Shopify, ad platforms, email/SMS, and
analytics tools, but turning it into timely decisions is hard: dashboards are
passive, insights require someone to go looking, and acting on a finding means
manual work in yet another tool. The 2026 shift is from **passive
visualization** to **proactive, agentic analytics** — agents that detect
patterns, predict outcomes, and take or trigger action with minimal input.

Industry reporting cites the impact of this shift: AI demand forecasting can cut
forecasting errors substantially and reduce lost sales and excess holdings,
real-time AI segmentation keeps marketing relevant without manual upkeep, and
Gartner projects ~40% of enterprise apps will embed task-specific AI agents by
end of 2026. The Data Agent brings that capability to Shopify merchants in a way
that is **store-native, explainable, and wired directly into the actions** the
other ShopifyAgents can perform.

## 3. Goals & non-goals

### Goals
- **Unify** store data into a single, trustworthy view (sales, inventory,
  customers, marketing, web behavior).
- **Proactively surface** insights, anomalies, and opportunities — without the
  merchant having to ask.
- **Forecast** demand/inventory needs, revenue, customer churn, and LTV.
- **Recommend** specific actions, each with rationale, expected impact, and
  confidence.
- **Act / orchestrate**: execute or hand off recommended actions under
  guardrails, and measure the outcome.
- Answer **ad-hoc natural-language questions** about the business ("why did
  revenue dip last week?") without SQL.

### Non-goals (v1)
- Being a generic BI/SQL replacement or building arbitrary custom dashboards.
- Writing store/marketing copy (→ Content Agent) or sending campaigns
  (→ Marketing Agent) directly — the Data Agent *triggers* those.
- Customer-facing support automation (separate Support/Customer Agent).
- Full financial accounting / bookkeeping.

## 4. Target users & personas

- **Solo founder / small team:** wants a "what should I do today" briefing and
  to never miss a stockout or a sales dip — without learning analytics tools.
- **Operations / merchandising lead at a scaling brand:** wants demand
  forecasts, reorder recommendations, and slow-mover/overstock alerts.
- **Growth / data analyst:** wants anomaly detection, cohort/LTV analysis, and
  the ability to ask deep ad-hoc questions and trust the attribution.

## 5. Competitive landscape (2026)

| Tool | Strength | Gap the Data Agent addresses |
| --- | --- | --- |
| **Triple Whale (Moby AI)** | Shopify-native DTC dashboards, creative/marketing analytics, chat-on-your-data | Strong insight/query; opportunity to tie insights directly to autonomous, multi-domain *actions* across content/marketing/ops |
| **Polar Analytics (Data Analyst, Media Buyer, Inventory Planner + agents)** | Unified cross-channel dataset; proactive anomaly/opportunity surfacing; purpose-built agents | Differentiate via tight execution loop with our Content/Marketing agents and a single orchestration layer |
| **Lebesgue (Henri AI / AI CMO)** | Marketing analytics, attribution, growth insights | Marketing-leaning; the Data Agent spans inventory + ops + customers too |
| **Shopify Analytics + Sidekick Pulse** | Free, native; surfaces next steps | Not a full unified-data forecasting + cross-agent action engine |
| **Klaviyo CDP / real-time signals** | Deep customer data for messaging | Customer/marketing-centric; the Data Agent unifies operational + financial data as well |

**Implication:** differentiate on (a) a **unified** store dataset, (b)
**explainable** insights/forecasts merchants trust, (c) a single
**orchestration layer** that converts findings into executed actions across the
agent suite, and (d) guardrailed autonomy with measurable outcomes.

## 6. Key capabilities (user stories)

1. **Unified data view** — _As a merchant, I want my sales, inventory,
   customer, and marketing data in one trustworthy place so insights reflect
   the whole business._
2. **Proactive insights & anomaly detection** — _… be told when something
   meaningful changes (sales dip/spike, rising CAC, conversion drop, stockout
   risk) with a likely cause — without going looking._
3. **Demand & inventory forecasting** — _… forecast demand per SKU and get
   reorder timing/quantity recommendations and overstock/slow-mover alerts._
4. **Sales & revenue analytics** — _… see revenue drivers, AOV, margin, and
   product/collection performance, and forecasts for the period ahead._
5. **Customer profiling & segments** — _… get cohorts, RFM/VIP segments, churn
   risk, and predicted LTV that the Marketing Agent can act on._
6. **Marketing performance & attribution** — _… understand revenue by channel/
   campaign and where to shift budget or effort._
7. **Recommendations with rationale** — _… receive ranked, explainable actions
   (expected impact, confidence) rather than raw charts._
8. **Action & orchestration** — _… approve a recommendation and have the right
   agent execute it (reorder, price change, content rewrite, campaign/segment),
   then see the result._
9. **Ask-anything (NL queries)** — _… ask questions in plain language and get
   answers with the supporting numbers, no SQL._
10. **Daily/weekly briefing** — _… get a concise "state of the business + top
    actions" digest._

## 7. Functional requirements

- **FR-1** Ingest and unify data: orders, products, inventory levels, customers,
  checkouts/carts, and (where connected) ad-platform and email/SMS performance;
  reconcile into consistent entities and metrics.
- **FR-2** Compute core metrics (revenue, AOV, margin where cost data exists,
  conversion, CAC/ROAS where ad data exists, repeat rate, churn, LTV).
- **FR-3** **Anomaly detection** on key metrics with plain-language explanations
  and probable causes.
- **FR-4** **Forecasting**: per-SKU demand and inventory needs (reorder point /
  quantity), revenue forecast, churn/LTV prediction.
- **FR-5** **Recommendation engine**: produce ranked actions, each with
  rationale, expected impact range, and confidence; group by domain (inventory,
  pricing/merchandising, content, marketing).
- **FR-6** **Action routing & execution**: hand off to Content/Marketing agents
  or execute operational actions via Admin API; respect approval gates and
  autonomy settings.
- **FR-7** **Natural-language query** interface over the unified dataset with
  cited supporting figures.
- **FR-8** **Briefings/alerts**: scheduled digests + real-time alerts for
  high-priority anomalies (e.g., imminent stockout, sharp ROAS drop).
- **FR-9** **Outcome tracking**: record actions taken and measure their effect
  (lift vs. baseline/holdout where feasible).

## 8. Non-functional requirements

- **Explainability & trust:** every insight/forecast/recommendation shows its
  basis and confidence; no opaque "magic numbers." Surface data gaps rather than
  guessing (e.g., margin unavailable without cost data).
- **Accuracy & calibration:** forecasts report uncertainty; models monitored for
  drift; backtested before relied upon.
- **Human control & guardrails:** recommendations require approval by default;
  per-domain autonomy and spend/quantity caps; clear audit trail and undo for
  any executed action.
- **Freshness/latency:** near-real-time for alerting-critical signals; defined
  refresh cadence for heavier analyses.
- **Privacy/compliance:** handle customer/financial data per Shopify API terms
  and data-protection rules; least-privilege access.
- **Observability/cost:** per-run logs, token/$ tracking, lineage from raw data
  to insight.

## 9. Agent architecture (proposed, to validate)

- **Inputs:** Shopify Admin API + webhooks (orders, products, inventory,
  customers, checkouts); optional connectors for ad platforms and email/SMS;
  cost/COGS data where provided.
- **Data layer:** ingestion + a unified store data model (entities + metrics)
  with lineage; this layer is a candidate **shared service** for the whole
  agent suite.
- **Analysis core:** metric computation, anomaly detection, and forecasting
  models, with an LLM planner/reasoner for explanation, NL Q&A, and
  recommendation synthesis (retrieval over the unified data).
- **Orchestration/action layer:** maps recommendations to executors — internal
  Admin API actions, or handoffs to the Content/Marketing agents — gated by a
  policy layer (approvals, caps, autonomy level) and recorded for outcome
  measurement.
- **Surfaces:** insights feed, briefings/alerts, NL chat, recommendation queue.

> Tech stack, model providers, and which connectors ship first are **open** —
> see Open questions and repo `CLAUDE.md`. This describes intent, not a
> committed design.

## 10. Success metrics

- **Decision velocity:** time from a meaningful change to a recommended/executed
  action.
- **Forecast quality:** demand/revenue forecast error (e.g., MAPE) vs. naive
  baseline; reduction in stockouts and overstock.
- **Action impact:** measured lift from acted-on recommendations
  (revenue/margin/retention) vs. baseline or holdout.
- **Adoption:** % of recommendations reviewed/accepted; autonomy adoption over
  time; NL-query usage.
- **Coverage/trust:** share of key metrics monitored; recommendation accept rate
  and reversal/undo rate.
- **Efficiency:** analyst/operator hours saved.

## 11. Risks & mitigations

| Risk | Mitigation |
| --- | --- |
| Wrong or overconfident recommendation drives a costly action | Confidence + impact ranges, approval gates, caps, holdouts, easy undo, outcome tracking |
| Bad/incomplete data → misleading insights | Data validation, surface gaps explicitly, lineage, reconciliation checks |
| Forecast model drift / regime change | Monitoring, backtesting, recalibration, conservative defaults |
| "Another dashboard" perception vs. incumbents | Differentiate via proactive, explainable insights wired to executed actions across the suite |
| Over-automation erodes trust | Conservative default autonomy; merchant-tunable; transparent audit trail |
| Privacy/compliance with customer & financial data | Least-privilege, consent-aware, compliant handling per Shopify terms |

## 12. Milestones (proposed)

- **M0 — Discovery:** confirm stack; unified data model; Shopify app + auth;
  connector priorities.
- **M1 — Unified data + core metrics + NL Q&A:** trustworthy single view and
  ask-anything.
- **M2 — Anomaly detection + briefings/alerts:** proactive insights with causes.
- **M3 — Forecasting (demand/inventory, revenue) + recommendations engine.**
- **M4 — Action/orchestration layer:** handoffs to Content/Marketing agents +
  guardrailed Admin API actions + outcome tracking.
- **M5 — Churn/LTV prediction, dynamic pricing/merchandising recommendations,
  advanced autonomy.**

## 13. Open questions

- Which external connectors ship first (ad platforms, email/SMS, COGS source)?
- Build forecasting/anomaly models in-house vs. leverage existing services?
- Default autonomy per action domain (inventory vs. pricing vs. marketing)
  before requiring approval?
- Authoritative attribution model and how to reconcile with the Marketing
  Agent's reporting?
- Is the unified data layer a standalone shared service for all agents, or owned
  by the Data Agent?
- Model provider(s) and per-merchant cost envelope?

## 14. References

- [Triple Whale vs Polar Analytics (Polar Analytics, 2026)](https://www.polaranalytics.com/vs/triple-whale)
- [Best AI Tools for Ecommerce Data Analysis (PodVector)](https://podvector.ai/articles/ai-analytics/ai-agents/best-ai-tools-for-ecommerce-data-analysis-compared)
- [6 Best Triple Whale Alternatives for Shopify Stores (Lebesgue)](https://lebesgue.io/growth/best-triple-whale-alternatives-for-shopify-stores)
- [How Ecommerce AI is Transforming Business in 2026 (BigCommerce)](https://www.bigcommerce.com/articles/ecommerce/ecommerce-ai/)
- [Predictive AI for Ecommerce (Arctic Leaf)](https://www.arcticleaf.com/blog/learning-center/predictive-ai-ecom/)
- [AI in Ecommerce Analytics: Predictive Analytics & Personalization (Techreviewer)](https://techreviewer.co/blog/ai-in-ecommerce-analytics-the-rise-of-predictive-analytics-and-personalization)
- [Top Agentic Commerce Trends for 2026 (MapMyChannel)](https://www.mapmychannel.com/blog/ai-trends-shaping-agentic-commerce-2026)
- [Shopify Magic and Sidekick: AI for Commerce](https://www.shopify.com/magic)
