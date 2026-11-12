# Org design: team topologies template

Use this when a strategy changes what teams own, when teams wait on each other more than they build, or when headcount grows by more than about a quarter. It feeds section 7 (Team) of the [one-pager](../template/one-pager.md). The team types and interaction modes come from *[Team Topologies](https://teamtopologies.com/key-concepts)* by Matthew Skelton and Manuel Pais.

## Principles

- **Design teams around the flow of change to customers,** not around technology layers. A "frontend team" and a "backend team" need a handoff for every feature.
- **Respect cognitive load.** A team owns only as much software as it can understand and run well. If on-call means paging someone who has never seen the service, the team owns too much.
- **Teams of 5–9 people,** long-lived, with work brought to the team rather than people moved to the work.
- **Architecture follows the org and the org follows the architecture** (Conway's law). Change both together, or the old shape returns.

## Team types

| Type | Purpose | Typical example |
|---|---|---|
| Stream-aligned | Delivers a product area or customer journey end to end | Invoicing, onboarding, integrations |
| Platform | Provides self-service internal services that make stream-aligned teams faster | Deploy pipeline, cells and tenancy, observability |
| Enabling | Helps other teams adopt a capability, then steps away | Test automation coaching, a security champion group |
| Complicated subsystem | Owns a part that needs rare specialist knowledge | Tax engine, matching algorithm |

Most teams should be stream-aligned. A platform team is justified when several stream-aligned teams repeat the same work; until then, it is overhead.

## Interaction modes

| Mode | When to use | Watch out for |
|---|---|---|
| Collaboration | Two teams discover something new together, for a fixed period | It is expensive. Set an end date |
| X-as-a-service | One team consumes another's stable service with little coordination | The provider must treat it as a product: docs, SLOs, and a published change log |
| Facilitating | An enabling team coaches another | Success is when the coached team no longer needs it |

## Template

### 1. Current state

| Team | Type today | People | Owns (services, journeys) | On-call load (pages / week) | Main dependencies | Pain |
|---|---|---|---|---|---|---|
| | | | | | | |

Measure dependencies with evidence: how many of a team's last 20 tickets waited on another team, and for how long.

### 2. Target state

| Team | Type | People | Owns | Interacts with (mode) | Key metric |
|---|---|---|---|---|---|
| | | | | | |

### 3. Checks before you commit

- [ ] Every service, data store and paging alert has exactly one owning team.
- [ ] No team owns more than it can run on-call without pulling in another team.
- [ ] Each stream-aligned team can ship its most common change without another team's approval.
- [ ] Platform teams have named internal customers and a measure of adoption.
- [ ] Every collaboration has an end date.
- [ ] Manager span is 5–8 direct reports.

### 4. Transition

Move one team at a time. For each move, write who changes team, which services change owner, and when on-call and access change. Keep the old on-call rotation until the new owner has handled at least one incident with support.

## Worked example (fictional)

Ledgerlight, from the [example strategy](../example/one-pager.md): 28 engineers in 4 product squads and a 2-person infrastructure group. Squads wait on the infrastructure group for every environment change, and the infrastructure group carries all paging.

| Team | Type | People | Owns | Interacts with |
|---|---|---|---|---|
| Invoicing | Stream-aligned | 7 | Invoice capture, approval flow | Platform (X-as-a-service) |
| Payments | Stream-aligned | 6 | Payment runs, bank files | Platform (X-as-a-service) |
| Integrations | Stream-aligned | 6 | ERP sync, webhooks | Platform (collaboration, for the queue migration in Q2 only) |
| Reporting | Stream-aligned | 6 | Reports, exports | Platform (X-as-a-service) |
| Platform | Platform | 5 | Cells, tenant router, CI/CD, observability, SSO and audit | All squads |

Before the change the squads were 7, 7, 6 and 6. The internal move to the platform team comes from Integrations, and the senior backend hire joins Integrations in Q2 and brings it back to 7. The EU-based SRE joins the platform team in Q3. Total: 32 engineers by the end of 2027, matching [appendix D](../example/appendix.md#d-team-and-hiring-plan).
