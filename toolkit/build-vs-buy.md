# Build vs buy: vendor scorecard

Use this before committing to build a capability in-house or to sign with a vendor for anything that holds customer data, sits on the critical path, or costs more than [an agreed amount] a year. It feeds the options table in the strategy [appendix](../template/appendix.md#b-options-considered).

## Step 1: should we build this at all?

Answer these before scoring vendors. They settle most cases.

| Question | Points to build | Points to buy |
|---|---|---|
| Is this capability part of why customers choose us? | Yes: it is differentiating | No: customers expect it to work, nothing more |
| Does a mature market exist? | No, or vendors fit badly | Yes, several vendors with customers like us |
| Do we have the skills to run it for years, including on-call? | Yes, and the team wants to own it | No, or only one person could |
| How fast do we need it? | We can wait for a build | Needed in weeks |
| What happens if the vendor fails, is acquired or triples the price? | Unacceptable risk | We could migrate within a quarter |

If the answers point to "buy", score vendors. If they point to "build", write an RFC with the build cost in engineer-months, including running it. If they are split, score the build option as one more candidate in the table below.

## Step 2: score the options

Score each criterion 1–5. Agree the weights **before** looking at vendors, so the weights do not drift toward a favourite.

| Criterion | Weight | What 5 looks like |
|---|---|---|
| Fit to requirements | 25% | Meets every must-have without custom work |
| Total cost of ownership, 3 years | 20% | Lowest TCO after integration, operation and exit costs |
| Security and compliance | 15% | Current SOC 2 Type II or ISO 27001 report, DPA signed, data residency options we need, SSO |
| Reliability and support | 10% | Published SLA that matches our tier, status history, responsive support in our hours |
| Integration and operability | 10% | Good APIs, webhooks, audit logs, metrics we can export, IaC or API-driven config |
| Lock-in and exit | 10% | Data export in a standard format; contract allows exit; migration estimated in weeks |
| Vendor viability | 5% | Profitable or well funded; customers our size; product actively maintained |
| Team capability and appetite | 5% | Our team can run it and wants to |

Weighted score = sum of (score × weight). Then read the scores: a high total with a 1 in security or lock-in is still a no.

## Total cost of ownership

Compare 3-year costs, not list prices.

| Cost | Build | Vendor A | Vendor B |
|---|---|---|---|
| Licences or subscription | — | | |
| Engineering to build or integrate (engineer-months × loaded monthly cost) | | | |
| Running it: infrastructure, on-call, upgrades (per year × 3) | | | |
| Training and migration | | | |
| Exit cost: migrating off at the end | | | |
| **3-year total** | | | |

Engineer time is the cost most often left out. Price it at the loaded cost per engineer-month, and count opportunity cost: what that team would otherwise ship.

## Worked example (fictional)

Ledgerlight needs SSO (SAML and OIDC) for enterprise customers, from the [example strategy](../example/one-pager.md). SSO is expected, not differentiating, and it is security-critical.

| Criterion | Weight | Build | Auth vendor | Open-source IdP, self-hosted |
|---|---|---|---|---|
| Fit | 25% | 4 | 5 | 4 |
| 3-year TCO | 20% | 2 | 3 | 3 |
| Security and compliance | 15% | 3 | 5 | 3 |
| Reliability and support | 10% | 3 | 4 | 2 |
| Integration and operability | 10% | 4 | 4 | 3 |
| Lock-in and exit | 10% | 5 | 2 | 4 |
| Vendor viability | 5% | 5 | 4 | 4 |
| Team capability | 5% | 2 | 4 | 2 |
| **Weighted score** | | **3.40** | **4.00** | **3.25** |

Decision: buy from the vendor, with an exit plan: user identities stay in Ledgerlight's database, keyed by an internal ID, so the IdP can be replaced. The lock-in score of 2 is the risk the exit plan answers.

## Record the decision

Write the outcome as an ADR: options, weighted scores, TCO, the deciding reason, and the exit plan. Review vendor decisions at each renewal with actual cost and incident data.
