# Cloud cost (FinOps) review

A monthly, 45-minute review that keeps cloud spend tied to business growth. It produces the actuals for the cost section of the [one-pager](../template/one-pager.md) and checks the levers in the [cost model](../template/appendix.md#c-cost-model). Run by the platform or infrastructure lead, with each team's engineering manager and someone from finance.

## Before the meeting

Prepare from the billing export and monitoring, not from memory:

- Spend for the month by service, by team (tags) and by environment, with the previous 3 months.
- The **unit cost**: spend divided by a business unit that finance recognises (active customer, tenant, 1,000 transactions).
- Anomalies: any line that moved more than 10% month on month without a known reason.
- Commitment status: coverage and utilisation of savings plans or reserved capacity.

## Scorecard

| KPI | Definition | This month | Last month | Target |
|---|---|---|---|---|
| Total spend | Cloud bill, all accounts | | | Within budget |
| Unit cost | Spend ÷ [business unit] | | | Flat or falling as you grow |
| Allocated spend | Share of spend with an owning-team tag | | | ≥ 90% |
| Commitment coverage | Share of steady-state compute covered by commitments | | | 60–80% of the right-sized baseline |
| Commitment utilisation | Share of committed spend actually used | | | ≥ 95% |
| Idle and orphaned spend | Unattached volumes, old snapshots, idle load balancers, stopped-but-billed resources | | | Falling |
| Non-production share | Non-production spend ÷ total | | | Agreed per company, often 10–20% |

The unit cost is the headline. Total spend that rises with customers is healthy; unit cost that rises is not.

## Agenda

1. **Scorecard and trend** (10 min). Unit cost first, then total.
2. **Anomalies** (10 min). Each one gets an owner and an explanation, or an action.
3. **Lever review** (15 min). Status of the actions from last month, then the checklist below for new ones.
4. **Decisions** (10 min). Commitments to buy or not, budget changes, items to escalate.

## Lever checklist

Work through these in order. The order matters: commit only after right-sizing, or you lock in waste.

- [ ] **Delete what nobody uses.** Orphaned volumes, snapshots past retention, idle environments, unread buckets and logs. Confirm with the owning team, and keep anything in DR scope.
- [ ] **Turn off what is idle.** Non-production off nights and weekends; preview environments deleted on merge.
- [ ] **Right-size.** Use 2–4 weeks of utilisation data. Change one tier at a time and watch latency and errors before the next step.
- [ ] **Move load before shrinking.** Batch and reporting work off the primary database, to replicas or queues, then resize.
- [ ] **Storage and data transfer.** Lifecycle rules to cheaper storage classes; private endpoints instead of NAT for high-volume internal traffic; a CDN for downloads.
- [ ] **Observability spend.** Drop debug logs in production, sample traces, set retention per log type.
- [ ] **Commit.** Savings plans or reservations on the baseline that remains after the steps above.
- [ ] **Architecture.** Only after the above: managed vs self-hosted, serverless vs always-on. These change operational load, so they need an RFC.

## Action log

| Date | Action | Owner | Expected saving / month | Risk and how we watch it | Status | Actual saving |
|---|---|---|---|---|---|---|
| | | | | | | |

Record actual savings from the bill two months later. Expected savings that never show up are the most common FinOps failure.

## Rules

- **Never trade reliability silently.** Every saving that touches production names the metric that would show harm, and the rollback.
- **Cost is a team metric.** Each team sees its own spend and unit cost. Central teams advise; owning teams act.
- **Price engineer time.** A saving of $500 a month that takes two engineer-weeks and adds on-call work is usually not worth it.

See the Ledgerlight [cost model](../example/appendix.md#c-cost-model) for these levers applied, including one deliberately declined.
