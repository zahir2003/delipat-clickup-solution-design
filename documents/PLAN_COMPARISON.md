# PLAN COMPARISON — ClickUp Solution Design

**Client:** Nordvik Consulting  
**Workspace:** Nordvik Consulting  
**Date checked:** 2026-09-19

**Evidence standard:** VERIFIED = directly supported by current ClickUp documentation and/or the Nordvik workspace test. DOCUMENTED = supported by ClickUp documentation but packaging/availability needs workspace confirmation. UNVERIFIED = not sufficiently verified for the Nordvik workspace.

## Executive summary

The Nordvik build was successfully tested during the Business trial. The current workspace uses ClickUp's newer **Early access** plan structure, where AI is shown as included in the plan cards.

For the plan comparison, the current documented tier structure is treated as:

- Free Forever
- Core
- Business
- Business Plus
- Enterprise
- Max

The Nordvik workspace pricing screen directly showed Business, Business Plus, Enterprise and MAX. Core pricing was not captured in the Nordvik workspace and is therefore not invented.

The older public AI add-on model still appears in some ClickUp documentation, so workspace-observed pricing is kept separate from legacy/public add-on pricing.

## Plan tier coverage

| Plan | Nordvik workspace evidence | Status |
|---|---|---|
| Free Forever | Workspace initially showed Free Forever, 1 seat, $0/seat | **VERIFIED** |
| Core | Current ClickUp new-plan documentation confirms the tier; exact Nordvik price was not captured | **DOCUMENTED / UNVERIFIED for Nordvik pricing** |
| Business | Workspace showed $24/user/month monthly and $16/user/month billed yearly | **VERIFIED** |
| Business Plus | Workspace showed $36/user/month monthly and $24/user/month billed yearly | **VERIFIED** |
| Enterprise | Workspace showed Custom pricing | **VERIFIED — Custom pricing** |
| Max | Workspace showed $120/user/month monthly and $100/user/month billed yearly | **VERIFIED for Nordvik workspace pricing** |

## Plan comparison matrix

| Area | Claim / evidence | Status | Source / evidence | Date checked |
|---|---|---|---|---|
| Automations | Free: 5 active / 100 actions per month; Unlimited: 500 / 1,000; Business: unlimited / 5,000; Business Plus: unlimited / 25,000; Enterprise: unlimited / 250,000 | **VERIFIED** | ClickUp Help — Automations | 2026-09-19 |
| API rate limit | Free 100 requests/min/token; Unlimited 100; Business 100; Business Plus 1,000; Enterprise 10,000 | **VERIFIED** | ClickUp Developer Docs — Rate Limits | 2026-09-19 |
| Custom Fields | Free: 60 uses; Unlimited+: unlimited. Business can pin fields; Business Plus/Enterprise provide advanced management capabilities | **VERIFIED** | ClickUp Help — Custom Fields | 2026-09-19 |
| Dashboards | Dashboard feature exists across plans with plan-based limits; advanced Dashboard cards are available on Business+; Business trial supported the Calculation cards used for Nordvik | **VERIFIED** | ClickUp Help — Dashboards / workspace test | 2026-09-19 |
| Workload | Free 60 uses; Unlimited 100; Business unlimited; Business Plus/Enterprise add advanced capacity controls such as per-day capacity and no-capacity days | **VERIFIED** | ClickUp Help — Workload | 2026-09-19 |
| Timesheets / time tracking | Free/Unlimited/Business have increasing limits; Business has 100 advanced time-tracking uses and 100 timesheet approvals; Business Plus/Enterprise have unlimited advanced time tracking and approvals plus additional custom-role permissions | **VERIFIED** | ClickUp Help — Time Tracking | 2026-09-19 |
| Guests / permissions | Paid plans support view-only and permission-controlled guests; permission-controlled guests are governed by plan guest-seat ratios and can consume paid seats when allowances are exhausted | **VERIFIED** | ClickUp Help — Guest roles / pricing | 2026-09-19 |
| Custom roles | Not available on Free, Unlimited or Business; available on Business Plus and Enterprise | **VERIFIED** | ClickUp Help — User roles / Nordvik screenshot #10 | 2026-09-19 |
| Forms | Forms available on all plans. Free has one Form; Unlimited+ unlimited. Advanced logic/options/hidden fields start at Business Plus; authenticated Forms are Enterprise | **VERIFIED** | ClickUp Help — Forms | 2026-09-19 |
| Security / SSO | Google SSO available on Business+; Microsoft, Okta and SAML available on Enterprise. Nordvik Business screen also showed Google SSO + SMS 2FA | **VERIFIED** | ClickUp Help — SSO / workspace plan screen | 2026-09-19 |
| Support | 24/7 support is available on all plans; Priority Support is Business Plus and Enterprise | **VERIFIED** | ClickUp Help — Support resources | 2026-09-19 |
| AI packaging | ClickUp documents newer plans with more AI included. Nordvik showed AI included in Business, Business Plus, Enterprise and MAX | **VERIFIED** | ClickUp Help — New plans / Nordvik Plans screen | 2026-09-19 |
| MAX plan | Nordvik workspace showed MAX at $100/user/month billed yearly and $120/user/month billed monthly | **VERIFIED** | Nordvik workspace Plans screen | 2026-09-19 |
| Legacy/public AI add-on pricing | ClickUp documentation still describes separate Brain/Everything AI add-ons, but Nordvik did not expose an Add-ons tab and showed AI bundled into plans | **DOCUMENTED** | ClickUp AI add-on docs + Nordvik workspace | 2026-09-19 |
| Exact Enterprise price | Enterprise price was displayed as Custom in the Nordvik workspace | **VERIFIED** | Nordvik workspace Plans screen | 2026-09-19 |
| Monthly/yearly pricing | Nordvik: Business $24 monthly / $16 yearly; Business Plus $36 monthly / $24 yearly; MAX $120 monthly / $100 yearly; Enterprise Custom | **VERIFIED** | Nordvik workspace Plans screen | 2026-09-19 |

## Pricing observed in the Nordvik workspace

### Monthly billing

- Business — $24/user/month
- Business Plus — $36/user/month
- Enterprise — Custom
- MAX — $120/user/month

### Yearly billing

- Business — $16/user/month billed yearly
- Business Plus — $24/user/month billed yearly
- Enterprise — Custom
- MAX — $100/user/month billed yearly

The workspace billing screen showed Business as the active trial and no payment method was configured.

## 39-user license calculations

| Plan | Monthly billing | Annualised monthly-billing cost | Yearly billing | Annual cost on yearly billing |
|---|---:|---:|---:|---:|
| Business | $24/user/mo | $11,232 | $16/user/mo | **$7,488** |
| Business Plus | $36/user/mo | $16,848 | $24/user/mo | **$11,232** |
| Enterprise | Custom | Custom | Custom | **Custom** |
| MAX | $120/user/mo | $56,160 | $100/user/mo | **$46,800** |

## Yearly-billing savings versus monthly billing

| Plan | Monthly-billing annualised | Yearly-billing annual total | Difference |
|---|---:|---:|---:|
| Business | $11,232 | $7,488 | **$3,744** |
| Business Plus | $16,848 | $11,232 | **$5,616** |
| MAX | $56,160 | $46,800 | **$9,360** |

Enterprise is not calculable without a sales quote.

## Key implications for Nordvik

### Billing build

The tested billing solution requires Formula Fields, Automations and Dashboard Calculation cards. The Free Forever workspace blocked Column Calculations, while the Business trial successfully calculated **23, 132 and 19,790**.

### API / accounting integration

ClickUp's API limits increase materially at Business Plus and Enterprise:

- Business — 100 requests/minute per token
- Business Plus — 1,000
- Enterprise — 10,000

This matters if a custom accounting integration becomes high-volume.

### Resource planning

Business provides unlimited Workload usage, while Business Plus/Enterprise add advanced capacity controls. The R4 test showed that Advanced Work Schedules were unavailable on the tested lower plan, and the requested three-country utilisation model is not directly supported by a single Workspace work schedule.

### Security

Business provides Google SSO according to ClickUp documentation. Enterprise adds Microsoft, Okta and SAML options. Business Plus is not equivalent to Enterprise for identity/security controls.

### Custom roles

The actual Nordvik Screenshot #10 shows that Custom Roles are unavailable on the current plan and that ClickUp prompts an upgrade to Business Plus. This is a direct workspace evidence point.

## UNVERIFIED / boundary notes

1. Exact Enterprise commercial pricing was not available; ClickUp displayed **Custom**.
2. Core pricing was not captured in the Nordvik Early access workspace.
3. The exact set of add-ons exposed to the Nordvik Early access workspace was not independently purchased or priced because no Add-ons tab was visible.
4. The newer Early access packaging is subject to change. The report therefore avoids copying older public AI add-on prices into the Nordvik quote.
5. Any capability not directly tested in the Nordvik workspace is not represented as tested.

## Official sources

- [ClickUp — Automations feature availability and limits](https://help.clickup.com/hc/en-us/articles/23477062949911-Automations-feature-availability-and-limits)
- [ClickUp — API rate limits](https://developer.clickup.com/docs/rate-limits)
- [ClickUp — Intro to Custom Fields](https://help.clickup.com/hc/en-us/articles/6303536766231-Intro-to-Custom-Fields)
- [ClickUp — Dashboards feature availability and limits](https://help.clickup.com/hc/en-us/articles/21257864054167-Dashboards-feature-availability-and-limits)
- [ClickUp — Workload feature availability and limits](https://help.clickup.com/hc/en-us/articles/30657456679703-Workload-view-feature-availability-and-limits)
- [ClickUp — Time Tracking feature availability and limits](https://help.clickup.com/hc/en-us/articles/29754533547415-Time-Tracking-feature-availability-and-limits)
- [ClickUp — Form view feature availability and limits](https://help.clickup.com/hc/en-us/articles/25810829634711-Form-view-feature-availability-and-limits)
- [ClickUp — User role availability and limits](https://help.clickup.com/hc/en-us/articles/26173894257047-User-role-availability-and-limits)
- [ClickUp — Guest-type user roles](https://help.clickup.com/hc/en-us/articles/6310022323991-Guest-type-user-roles)
- [ClickUp — SSO](https://help.clickup.com/hc/en-us/articles/6305043992343-Intro-to-single-sign-on-SSO)
- [ClickUp — Support resources](https://help.clickup.com/hc/en-us/articles/16251448728727-ClickUp-support-resources)
- [ClickUp — Pricing per user role and plan](https://help.clickup.com/hc/en-us/articles/6303244318999-Pricing-per-user-role-and-plan)
- [ClickUp — New plans and pricing options](https://help.clickup.com/hc/en-us/articles/42972527662359-New-plans-and-pricing-options)
