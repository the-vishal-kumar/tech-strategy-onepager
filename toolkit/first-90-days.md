# First 90 days as an engineering leader: a 30/60/90 template

For a new head of engineering, VP, CTO or CPTO. The first 90 days earn the right to change things: listen first, find the few problems that matter, then commit to a written strategy. The output at day 90 is a strategy [one-pager](../template/one-pager.md) agreed with the CEO.

Copy the template below and fill it in with your manager in week 1. Agreeing what "good" looks like at day 90 is the most useful conversation of the first month.

## Days 1-30: listen and learn

**Goal:** understand the business, the people and the system well enough to describe the current state with numbers.

- [ ] One-to-ones with every direct report, and with every engineer if the organisation is under ~50 people. Same questions each time: what works, what gets in your way, what should I not change, what would you do in my place?
- [ ] Meet peers: CEO, product, sales, customer success, finance. Ask each what engineering does well and badly for them.
- [ ] Talk to at least five customers, or listen to sales and support calls.
- [ ] Read the last 6 months of postmortems, the incident list and the on-call load.
- [ ] Get the numbers: DORA metrics, availability against SLOs, cloud spend and unit cost, headcount and attrition, open roles.
- [ ] Map the architecture at the level of services, data stores and owning teams. Note where ownership is unclear.
- [ ] Ship something small yourself or pair on a deploy, to learn the developer experience first-hand.

**Do not:** reorganise, announce a new process, or rewrite anything. Fix only what is on fire, and say why.

**Output:** a written current-state summary. It becomes section 2 of the one-pager.

## Days 31-60: diagnose and choose

**Goal:** pick the two or three problems that block the business most, and test your diagnosis with the people who will do the work.

- [ ] Write the diagnosis: the few problems, the evidence for each, and what they cost the business.
- [ ] Play it back to your team and peers. Change it where they show you are wrong.
- [ ] Build trust with early, visible fixes that the team asked for in month one: a flaky pipeline, a noisy alert, an unclear decision process.
- [ ] Assess the leadership team against the next 12 months, not the last 12. Decide on any people changes privately, and act on them by day 90.
- [ ] Set a baseline for the metrics you will be judged on.

**Output:** a diagnosis agreed with the CEO and the engineering leadership team, and a short list of early fixes delivered.

## Days 61-90: commit

**Goal:** a written strategy, approved, with the first quarter's work under way.

- [ ] Write the one-pager and appendix: target architecture, phased approach, risks, cost and team.
- [ ] Pre-read it with the CFO and one skeptic, then get the decisions in section 9 approved.
- [ ] Set the operating rhythm: OKRs, delivery reviews, cost review. See the [operating model](operating-model.md) and [FinOps review](finops-review.md).
- [ ] Make the org changes the strategy needs, using the [org design template](org-design.md).
- [ ] Publish the strategy to the whole engineering organisation, with the reasoning and what you chose not to do.

**Output:** an approved strategy, a first quarter of work with exit criteria, and a regular forum to check progress.

## Template

| | Days 1-30 | Days 31-60 | Days 61-90 |
|---|---|---|---|
| Goal | | | |
| Key activities | | | |
| People I must meet | | | |
| Measures of success | | | |
| Output | Current-state summary | Agreed diagnosis | Approved strategy one-pager |
| Agreed with manager on | | | |

## Traps

- **Arriving with the answer.** The strategy that worked at your last company was built for its constraints. Spend the first month finding out which of your assumptions hold.
- **Changing everything.** Pick the few problems that matter. Everything else waits.
- **Only listening upward.** The engineers closest to the code usually know the real problems first.
- **Skipping the numbers.** A diagnosis without a baseline cannot show progress, and the CFO will ask for it.
