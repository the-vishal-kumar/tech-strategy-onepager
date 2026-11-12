# tech-strategy-onepager

[![docs](https://github.com/the-vishal-kumar/tech-strategy-onepager/actions/workflows/docs.yml/badge.svg?branch=main)](https://github.com/the-vishal-kumar/tech-strategy-onepager/actions/workflows/docs.yml)

A template for writing a technology strategy on one page, a worked example for a fictional B2B SaaS company, and the companion templates that produce the evidence each section needs.

**Problem:** technology strategies are usually a 40-slide deck that mixes evidence with opinion and never states the decision it needs. Executives cannot approve what they cannot follow, and nobody checks the plan a quarter later.

**Who it's for:** CTOs, CPTOs, VPs and heads of engineering who need a decision from a CEO, CFO or board on architecture, phasing, cost and headcount, and who want that decision made from one page.

**What you get:** a one-page format that answers the questions executives ask, in the order they ask them; an appendix for the evidence; a fully worked example whose numbers add up; and templates for the operating model, org design, build-vs-buy, cost review and a new leader's first 90 days.

## What's in it

### The strategy

| Document | What it is |
|---|---|
| [One-pager template](template/one-pager.md) | The one-pager, with prompts for each section |
| [Appendix template](template/appendix.md) | Evidence: options, cost model, hiring plan, metric definitions |
| [Example one-pager](example/one-pager.md) | Filled in for **Ledgerlight**, an invented accounts-payable SaaS company |
| [Example appendix](example/appendix.md) | The example's evidence, including the full cost model and sensitivity |

### The toolkit

| Document | Feeds section | What it is |
|---|---|---|
| [First 90 days](toolkit/first-90-days.md) | All | 30/60/90 template for a new engineering leader, ending in the one-pager |
| [Operating model](toolkit/operating-model.md) | 8. Success metrics | Discovery to delivery, roles, OKRs, RICE prioritisation with a worked example, cadence |
| [Org design](toolkit/org-design.md) | 7. Team | Team Topologies types and interaction modes, current/target template, checks, worked example |
| [Build vs buy](toolkit/build-vs-buy.md) | Appendix B | Questions that settle most cases, weighted vendor scorecard, 3-year TCO, worked example |
| [FinOps review](toolkit/finops-review.md) | 6. Cost | Monthly cost review: KPIs, agenda, ordered lever checklist, action log |

Ledgerlight is fictional. Its numbers, people and history are invented for illustration and do not describe any real company. The toolkit's worked examples use the same company, so they agree with the one-pager.

## The structure

The one-pager answers, in order, the questions an executive asks:

1. **Why now:** what business goal this serves and what blocks it.
2. **Current state:** facts and numbers, not complaints.
3. **Target architecture:** one diagram, what changes, and what you are deliberately not doing.
4. **Phased approach:** quarters, with exit criteria someone can check.
5. **Risks:** likelihood, impact, mitigation, owner.
6. **Cost:** today versus each milestone, and cost per unit of business (customer, tenant, transaction).
7. **Team:** shape, hires by quarter, and what happens if hiring slips.
8. **Success metrics:** baseline and target.
9. **Decisions requested:** the specific approvals you need.

Everything that supports a claim but doesn't change the decision goes in the appendix.

## Week 1 with this repository

For a leader who has to produce a strategy, in a new role or an existing one:

1. **Day 1: agree the 90 days.** Fill in the [first 90 days](toolkit/first-90-days.md) template with your manager. Agree that the output is an approved one-pager, and by when.
2. **Day 2: read the example end to end.** The [Ledgerlight one-pager](example/one-pager.md), then its [appendix](example/appendix.md). Note which numbers you do not have for your own company.
3. **Day 3: start the evidence list.** Copy the [appendix template](template/appendix.md) and fill section A (current state) with whatever numbers exist, each with a source and a date. Leave gaps visible.
4. **Day 4: book the inputs.** Schedule the first [FinOps review](toolkit/finops-review.md) to get cost and unit cost, and ask for DORA and availability data for the last quarter.
5. **Day 5: write section 9 first.** Draft the decisions you expect to need. They will change, but every other section exists to justify them.

## How to write it

1. **Start from section 9.** Write the decisions you need before anything else.
2. **Collect the numbers.** Current-state facts need a source and a date. If you can't measure something yet, say so and make measuring it the first deliverable.
3. **Draft the appendix, then cut it down.** The one-pager is a summary of the appendix, not the other way round.
4. **Draw the target, not the present.** One diagram of where you're going. Put the current-state diagram in the appendix if you need one.
5. **Pre-read with the CFO and one skeptic.** The cost section and the risk table get challenged most. Fix them before the meeting.
6. **Revisit each quarter.** Mark exit criteria as met or missed and update the cost table with actuals. A strategy that is never checked becomes a wish list.

## Writing rules

- One page. If it doesn't fit, the strategy isn't clear yet.
- Numbers over adjectives. "p95 latency 850 ms at month-end" beats "slow under load".
- Say what you won't do. Rejected options show judgment and prevent the same debate next quarter.
- Every phase has an exit criterion. Every risk has an owner.
- Show cost per unit of business, not only the total. A growing bill can be healthy; a growing unit cost usually isn't.

## About the cost section

Cost is where engineering strategy meets the CFO, so the example spends the most care on it. The approach is: find the waste from utilisation data, move load before shrinking anything, commit to discounts only after right-sizing, delete what nobody reads, and price engineer time next to cloud spend. The [FinOps review](toolkit/finops-review.md) turns the same order into a monthly routine.

This mirrors work I've done. In my current role I cut monthly cloud spend from about $14K to about $2K by right-sizing over-provisioned resources, self-hosting databases, and removing unused services and data. Ledgerlight's numbers are invented and deliberately different. Its cost model also *declines* to self-host databases for now, because with a 2-person infrastructure group the on-call and recovery burden outweighs the saving. The right lever depends on the team that has to run it.

## Rendering and checks

Diagrams are [Mermaid](https://mermaid.js.org/), which GitHub renders in Markdown. To export the one-pager to PDF, any Markdown-to-PDF tool with Mermaid support works.

`scripts/check-docs.sh` runs the same checks as CI, each in Docker with a pinned image: markdownlint, a link check that also verifies `#section` anchors, and a render of every Mermaid diagram.

## License

[MIT](LICENSE) © 2026 Vishal Kumar
