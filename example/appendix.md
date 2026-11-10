# Appendix: Ledgerlight technology strategy 2027

> **Fictional example.** All companies, numbers and people here are invented.

Supporting detail for the [one-pager](one-pager.md).

## A. Current state detail

| Fact | Value | Source |
|---|---|---|
| Paying customers | 410 | Billing system, Oct 2026 |
| Peak traffic | ~1,200 requests/s on the last 3 working days of the month | Load balancer metrics |
| Availability, trailing 12 months | 99.5% (about 44 hours of downtime) | Synthetic checks |
| p95 API latency, month-end vs other days | 850 ms vs 240 ms | APM |
| Database CPU at 02:00–05:00 (nightly jobs) | 85–95% | Database metrics |
| Database CPU, rest of the day | 25–35% | Database metrics |
| App server average CPU | 18% | Cloud monitoring, 30-day average |
| Change failure rate | 22% | Deploy log joined to incident tracker |

Month-end latency and the oversized database have the same cause: reporting and ERP sync run on the primary and compete with user traffic.

## B. Options considered

| Option | Cost | Time | Risk | Decision |
|---|---|---|---|---|
| **Cells + modular monolith** (chosen) | Medium | 3 quarters | Medium: a second stack to run | Delivers residency, isolates load, reuses existing code and skills |
| Rewrite into microservices | High | 6+ quarters | High: long freeze on features | Rejected. Solves an org-scaling problem we don't have at 28 engineers |
| Multi-region single database with row-level residency | High | 4 quarters | High: complex, hard to prove to auditors | Rejected. Residency must be easy to explain to a customer's security team |
| Buy residency through a hosting partner | Medium | 2 quarters | Medium: lock-in, less control over SLOs | Kept as fallback if hiring slips badly |
| Do nothing | Low now | — | High: enterprise and EU plans stall | Rejected |

## C. Cost model

Monthly, in thousands of USD. "End 2027" includes the EU cell and planned growth to 520 customers.

| Line item | Today | End Q2 2027 | End 2027 | Lever and assumption |
|---|---|---|---|---|
| Compute (app + workers) | 17.0 | 10.0 | 13.0 | Right-size to ~50% target CPU; autoscale workers on queue depth; 1-year commitment on the always-on baseline |
| Databases | 11.0 | 7.5 | 10.5 | Reporting moves to a replica, so the primary drops two sizes; replica added; EU primary added |
| Storage and backups | 4.5 | 2.5 | 3.0 | Lifecycle rules move logs and old exports to cold storage; delete orphaned snapshots; retention set by DR tier |
| Data transfer | 3.0 | 2.0 | 2.5 | Private endpoints for storage and queue traffic instead of NAT; CDN for file downloads |
| Observability and tooling | 3.5 | 3.0 | 3.5 | Stop ingesting debug logs in production; sample traces at 10%, keep 100% of errors |
| Non-production | 2.0 | 1.0 | 1.5 | Staging and dev off nights and weekends; preview environments deleted on merge; EU staging added |
| **Total** | **41.0** | **26.0** | **34.0** | |
| Customers | 410 | 440 | 520 | Sales plan |
| **Per customer** | **$100** | **$59** | **$65** | |

### Lever reasoning

1. **Right-sizing first.** Utilisation data shows the waste: 18% average app CPU, and a database sized for a 3-hour nightly peak. Right-sizing is reversible in minutes, so we change one tier at a time and watch p95 latency and error rate for a week before the next step.
2. **Move the load, then shrink the database.** Shrinking the primary before reporting moves would make month-end worse. The order matters more than the size of any single step.
3. **Commit after right-sizing, not before.** A 1-year commitment on today's footprint would lock in the waste for a year. We commit only on the baseline we see after Q1, and leave burst capacity on demand.
4. **Delete what nobody reads.** Storage access logs show which buckets and snapshots have not been read in 180 days. We delete or archive them after the owning team confirms. Retention for anything in DR scope follows the DR tier, not the cost target.
5. **Self-hosting databases: not now.** Running Postgres ourselves on compute would cut the database line by roughly a third. It would also move backups, failover, patching and on-call for our most critical system onto a 2-person infrastructure group. Self-hosting pays off when the team already runs databases well and the managed premium is large next to engineer time. We revisit at the end of 2027, once the platform team is staffed and database spend is known after the EU cell.

### Sensitivity

- **Customer growth at double the plan (630 by end 2027):** cost rises to about $38K/month; per-customer cost falls to about $61.
- **Growth at half the plan (465):** cost about $31K/month; per-customer cost about $67, still above target. The main fix would be to delay EU staging and keep the commitment at the lower baseline.
- **EU cell not built:** end-2027 cost about $27K/month, $52 per customer.

## D. Team and hiring plan

| Role | Why | Quarter | If we cannot hire |
|---|---|---|---|
| Staff platform engineer | Leads cells, tenant router and infrastructure code | Q1 | Internal promotion plus external advisor; EU cell slips one quarter |
| SRE | SLOs, on-call quality, DR tests | Q1 | Platform team shares the work; DR test moves to Q4 |
| Senior backend engineer (integrations) | Queue-based ERP sync | Q2 | Squad with ERP knowledge takes it on; one product feature deferred |
| EU-based SRE | On-call cover in EU working hours; local credibility with EU customers | Q3 | US on-call covers with an extended rotation and higher on-call pay, for at most two quarters |

The platform team is 5 people: 2 from the current infrastructure group, 1 internal move from a product squad, and the first two hires. Headcount grows from 28 to 32. Product squads keep their current size.

## E. Metric definitions

| Metric | Definition | Source | Owner |
|---|---|---|---|
| Availability | Share of 1-minute synthetic checks on login and invoice approval that succeed, per month | Synthetic monitoring | SRE |
| p95 API latency at month-end | p95 server-side latency for all API calls on the last 3 working days of the month | APM | Platform lead |
| Deploy frequency | Production deploys of the core app per week | Deploy pipeline | Eng managers |
| Change failure rate | Share of deploys followed by a rollback, hotfix or incident within 48 hours | Deploy log + incident tracker | Eng managers |
| Cost per active customer | Monthly cloud bill ÷ customers with at least one approval that month | Cloud billing + product analytics | Platform lead |
| Deals lost to platform gaps | Closed-lost enterprise deals where SSO, audit or residency is a recorded loss reason | CRM | CRO |

## F. Open questions

- Which EU region do the first prospects require? Answer from sales by end of Q1.
- Does the audit log need to be exportable to customers' own logging tools in the first release? Decide with the first two pilots.
- Can the tenant router be the existing load balancer with host-based routing, or does it need its own service? Spike in Q2.
