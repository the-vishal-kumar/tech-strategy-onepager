# tech-strategy-onepager

A template for writing a technology strategy on one page, plus a worked example for a fictional B2B SaaS company.

**Who it's for:** engineering leaders who need a decision from a CEO, CFO or board on architecture, roadmap, cost and headcount, and who want that decision made from one page instead of a 40-slide deck.

## What's in it

| Path | What it is |
|---|---|
| [`template/one-pager.md`](template/one-pager.md) | The one-pager, with prompts for each section |
| [`template/appendix.md`](template/appendix.md) | Appendix for evidence: options, cost model, hiring plan, metric definitions |
| [`example/one-pager.md`](example/one-pager.md) | Filled-in example for **Ledgerlight**, an invented accounts-payable SaaS company |
| [`example/appendix.md`](example/appendix.md) | The example's appendix, including the full cost model |

Ledgerlight is fictional. Its numbers, people and history are invented for illustration and do not describe any real company.

## The structure

The one-pager answers, in order, the questions an executive asks:

1. **Why now:** what business goal this serves and what blocks it.
2. **Current state:** facts and numbers, not complaints.
3. **Target architecture:** one diagram, what changes, and what you are deliberately not doing.
4. **Roadmap:** quarters, with exit criteria someone can check.
5. **Risks:** likelihood, impact, mitigation, owner.
6. **Cost:** today versus each milestone, and cost per unit of business (customer, tenant, transaction).
7. **Team:** shape, hires by quarter, and what happens if hiring slips.
8. **Success metrics:** baseline and target.
9. **Decisions requested:** the specific approvals you need.

Everything that supports a claim but doesn't change the decision goes in the appendix.

## How to use it

1. **Start from section 9.** Write the decisions you need before anything else. Every other section exists to justify them.
2. **Collect the numbers.** Current-state facts need a source and a date. If you can't measure something yet, say so and make measuring it a Q1 deliverable.
3. **Draft the appendix, then cut it down.** The one-pager is a summary of the appendix, not the other way round.
4. **Draw the target, not the present.** One diagram of where you're going. Put the current-state diagram in the appendix if you need one.
5. **Pre-read with the CFO and one skeptic.** The cost section and the risk table get challenged most. Fix them before the meeting.
6. **Revisit each quarter.** Mark exit criteria as met or missed and update the cost table with actuals. A strategy that is never checked becomes a wish list.

## Writing rules

- One page. If it doesn't fit, the strategy isn't clear yet.
- Numbers over adjectives. "p95 latency 850 ms at month-end" beats "slow under load".
- Say what you won't do. Rejected options show judgment and prevent the same debate next quarter.
- Every roadmap row has an exit criterion. Every risk has an owner.
- Show cost per unit of business, not only the total. A growing bill can be healthy; a growing unit cost usually isn't.

## About the cost section

Cost is where engineering strategy meets the CFO, so the example spends the most care on it. The approach is: find the waste from utilisation data, move load before shrinking anything, commit to discounts only after right-sizing, delete what nobody reads, and price engineer time next to cloud spend.

This mirrors work I've done. In my current role I cut monthly cloud spend from about $14K to about $2K by right-sizing over-provisioned resources, self-hosting databases, and removing unused services and data. Ledgerlight's numbers are invented and deliberately different. Its cost model also *declines* to self-host databases for now, because with a 2-person infrastructure group the on-call and recovery burden outweighs the saving. The right lever depends on the team that has to run it.

## Rendering

The diagram is [Mermaid](https://mermaid.js.org/), which GitHub renders in Markdown. To export the one-pager to PDF, any Markdown-to-PDF tool with Mermaid support works.

## License

[MIT](LICENSE) © 2026 Vishal Kumar
