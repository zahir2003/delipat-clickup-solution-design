# FEASIBILITY — ClickUp Solution Design

**Client:** Nordvik Consulting  
**Date:** 2026-09-19

## Executive result

| Requirement | Verdict | Evidence |
|---|---|---|
| R1 — Hours Variance | **CONFIGURATION** | Number Custom Fields + Formula Field; Dashboard Calculation used for total. Free plan blocked aggregate Column Calculations; Business trial enabled the required calculation/reporting capability. |
| R2 — WIP reporting | **CONFIGURATION** | Formula Fields + Invoice Status helper automation + filtered WIP view + Dashboard Calculation. |
| R3 — Accounting integration with e-conomic | **CUSTOM BUILD** | No native e-conomic billing flow was identified in ClickUp's native integration catalogue. ClickUp provides API/webhooks; a third-party integration platform or custom API service can implement the required flow. |
| R4 — Per-country holiday calendars and utilisation | **CUSTOM BUILD** | Calendar can display national holidays, but Workspace Work Schedule drives capacity and does not provide independent Denmark/India/Sweden utilisation calendars in one Workspace. Advanced Work Schedules were also locked behind Business Plus in the test. |
| R5 — Pricing | **NATIVE** | ClickUp provides plan pricing and billing-cycle choices. Implementation, custom integration and support are separate commercial estimates rather than ClickUp license fees. |

## R1 — Hours Variance

**Requirement:** Worked Hours minus Approved Hours, with a report total.

**Observed implementation**

- Worked Hours — Number
- Approved Hours — Number
- Hours Variance — Formula: `Worked Hours - Approved Hours`
- Dashboard Calculation card: Sum of Hours Variance = **23**

**Verdict: CONFIGURATION**

The calculation itself is native to ClickUp Formula Fields, but the customer must configure the Custom Fields, formula and reporting view/card. The Free Forever plan did not expose Column Calculations; the Business trial did.

**Customer-facing sentence**

> ClickUp can calculate hours variance natively once the billing fields and formula are configured; the management total requires a plan with the required calculation/reporting capability.

## R2 — WIP reporting

**Requirement:** Approved hours × hourly rate for jobs not yet invoiced; invoiced jobs must show zero WIP.

**Observed implementation**

- Invoice Status — Dropdown
- Invoiced Flag — Number helper
- WIP Hours — Formula
- WIP — Formula
- Two Automations keep Invoiced Flag aligned with Invoice Status
- WIP Report filters out Invoiced tasks
- Dashboard Calculation cards return **132 WIP hours** and **19,790 WIP value**

**Verdict: CONFIGURATION**

The formula and views are native, but the status-to-formula link required a helper field and Automations because ClickUp Formula Fields do not directly support text Custom Fields.

**Customer-facing sentence**

> ClickUp can run the WIP calculation, but the billing workflow needs a small configuration layer using a numeric helper field and Automations.

## R3 — e-conomic accounting integration

**Requirement:** Push invoice data from ClickUp to e-conomic and write the returned invoice number back into ClickUp.

**Research**

- ClickUp's native integrations catalogue was reviewed; no native e-conomic connector was identified.
- ClickUp provides API/webhook capabilities suitable for custom integrations.
- e-conomic provides OpenAPI/REST APIs for invoice operations.
- Make provides a ClickUp + e-conomic integration path.

**Verdict: CUSTOM BUILD**

A third-party/no-code integration or custom API service appears technically feasible, but the workflow is not a native ClickUp accounting feature and was not executed against a live e-conomic account in this assignment.

**Customer-facing sentence**

> ClickUp does not provide the required e-conomic accounting flow as a native billing feature; the integration should be implemented through a supported integration platform or a custom API service, with controlled write-back of the e-conomic invoice number.

## R4 — Country holiday calendars and utilisation

**Requirement:** Denmark, India and Sweden have different public holidays, and utilisation should respect each employee's country calendar.

**Observed / researched**

- ClickUp Calendar can display national holiday calendars.
- Workload availability/capacity uses the Workspace work schedule.
- Workspace holidays/custom non-working days create zero-capacity days.
- ClickUp's Work Schedule does not provide independent country-specific capacity calendars for three employee groups inside one Workspace.
- The Nordvik test showed Advanced Work Schedules unavailable on the tested plan and indicated Business Plus as the upgrade boundary.

**Verdict: CUSTOM BUILD**

The exact business requirement is not satisfied natively by one Workspace work schedule.

**Customer-facing sentence**

> ClickUp can display country holidays, but automatic utilisation based on three different country calendars requires a workaround or custom capacity/integration layer.

## R5 — Pricing

**Requirement:** Cost for 39 people, plan, one-time costs and recurring costs beyond licenses.

**Verdict: NATIVE**

ClickUp supplies the license pricing and billing-cycle choices. The implementation, custom integration and ongoing support are separate delivery estimates and are not ClickUp fees.

## Overall implementation boundary

The ClickUp platform can run the demonstrated billing calculations and reporting once configured.

The two material gaps are:

1. e-conomic accounting synchronisation is not a native ClickUp billing flow.
2. Independent country-specific utilisation calendars are not provided by a single Workspace work schedule.

The build therefore demonstrates a workable ClickUp billing layer, but not a completely native end-to-end accounting and multinational utilisation system.

## Key evidence

- Total Hours Variance: **23**
- Total WIP Hours: **132**
- Total WIP Value: **19,790**
- Integration design variance: **8 hours**, but WIP **0** because it is already invoiced.
- Dynamic status test: Build phase 1 changed Ready to Invoice → Invoiced → WIP 0, then restored to Ready to Invoice → WIP $3,750.

## Sources

- [ClickUp integrations](https://clickup.com/integrations)
- [ClickUp API](https://developer.clickup.com/docs/Getting%20Started)
- [ClickUp API rate limits](https://developer.clickup.com/docs/rate-limits)
- [e-conomic developer documentation](https://www.e-conomic.com/developer/documentation)
- [e-conomic REST invoice documentation](https://restdocs.e-conomic.com/)
- [Make ClickUp + e-conomic integration](https://www.make.com/en/integrations/e-conomic/clickup)
- [ClickUp Work Schedule](https://help.clickup.com/hc/en-us/articles/33032722352279-Set-a-work-schedule-for-your-Workspace)
- [ClickUp Workload capacity](https://help.clickup.com/hc/en-us/articles/30799838221335-Measure-availability-or-capacity-in-Workload-view)
- [ClickUp Workload limits](https://help.clickup.com/hc/en-us/articles/30657456679703-Workload-view-feature-availability-and-limits)
