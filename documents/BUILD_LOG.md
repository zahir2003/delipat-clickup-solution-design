# BUILD LOG — ClickUp Solution Design

## Project

**Assignment:** Assignment Two — ClickUp Solution Design  
**Client Scenario:** Nordvik Consulting  
**Platform:** ClickUp  
**Workspace:** Nordvik Consulting  
**Purpose:** Build and test a ClickUp-based billing/work-management solution and document what is supported natively, what requires configuration, and what requires custom work.

---

# Day 1 — Workspace and Hierarchy Setup

## Completed

Created the required ClickUp workspace structure for the Nordvik Consulting scenario.

### Required hierarchy

```text
Nordvik Consulting
└── Clients (Space)
    └── Clients (Folder)
        ├── Client Alpha (List)
        ├── Client Beta (List)
        └── Client Gamma (List)
```

The hierarchy matches the assignment requirements.

## Client task structure

Created the six required billing task rows.

### Client Alpha

1. **Discovery workshop**
   - Worked Hours: 40
   - Approved Hours: 38
   - Hourly Rate: 150
   - Invoice Status: Invoiced

2. **Build phase 1**
   - Worked Hours: 25
   - Approved Hours: 25
   - Hourly Rate: 150
   - Invoice Status: Ready to Invoice

### Client Beta

3. **Data migration**
   - Worked Hours: 60
   - Approved Hours: 52
   - Hourly Rate: 120
   - Invoice Status: Ready to Invoice

4. **Support retainer**
   - Worked Hours: 15
   - Approved Hours: 15
   - Hourly Rate: 120
   - Invoice Status: Not Ready

### Client Gamma

5. **Integration design**
   - Worked Hours: 30
   - Approved Hours: 22
   - Hourly Rate: 200
   - Invoice Status: Invoiced

6. **UAT & rollout**
   - Worked Hours: 45
   - Approved Hours: 40
   - Hourly Rate: 200
   - Invoice Status: Ready to Invoice

## Expected calculations

### Hours Variance

```text
Worked Hours - Approved Hours
```

Expected total: **23 hours**

### WIP Hours

```text
Approved Hours for jobs that are not Invoiced
```

Expected total: **132 hours**

### WIP Value

```text
Approved Hours × Hourly Rate
```

for jobs that are not Invoiced.

Expected total: **19,790**

The **Integration design** task is an important test case because it has:

```text
Worked Hours = 30
Approved Hours = 22
Variance = 8
Invoice Status = Invoiced
WIP Hours = 0
WIP Value = 0
```

This verifies that billed work should not remain in WIP even when a variance exists.

## Issue / observation

The initial workspace setup was completed without requiring paid features.

## Screenshot

- Screenshot #1 — Space, Folder and three Client Lists completed.

---

# Day 2 — Custom Fields and Billing Data

## Completed

Created the required billing Custom Fields at the **Clients Folder** level so that the fields are available across the Client Alpha, Client Beta and Client Gamma Lists.

## Custom Fields created

### Input fields

- Worked Hours — Number
- Approved Hours — Number
- Hourly Rate — Number
- Invoice Status — Dropdown

Invoice Status options:

```text
Invoiced
Ready to Invoice
Not Ready
```

### Helper field

- Invoiced Flag — Number

The helper field was required because ClickUp Formula Fields do not directly support text Custom Fields such as the Invoice Status dropdown.

### Calculated fields

- Hours Variance — Formula
- WIP Hours — Formula
- WIP — Formula

## Formula logic

### Hours Variance

```text
Worked Hours - Approved Hours
```

### Invoiced Flag

```text
1 when Invoice Status = Invoiced
0 otherwise
```

### WIP Hours

```text
IF Invoiced Flag = 1
THEN 0
ELSE Approved Hours
```

### WIP

```text
IF(Invoiced Flag = 1, 0, Approved Hours × Hourly Rate)
```

The WIP formula currently used in ClickUp is:

```text
IF(field("Invoiced Flag") = 1, 0, field("Approved Hours") * field("Hourly Rate"))
```

## Important ClickUp limitation discovered

ClickUp Formula Fields do not directly support Custom Fields containing text.

Because `Invoice Status` is a dropdown/text-based Custom Field, the status could not simply be referenced directly inside the Formula Field.

A numeric `Invoiced Flag` helper field was therefore created.

## Configuration workaround

Two ClickUp Automations were created.

### Automation 1

**Trigger:** Invoice Status changes to `Invoiced`  
**Action:** Set `Invoiced Flag` to `1`

### Automation 2

**Trigger:** Invoice Status changes from `Invoiced` to another status  
**Action:** Set `Invoiced Flag` to `0`

## Testing

The automation was tested using the `Build phase 1` task.

Initial state:

```text
Invoice Status = Ready to Invoice
Invoiced Flag = 0
WIP = 3,750
```

Changed status to:

```text
Invoiced
```

Result:

```text
Invoiced Flag = 1
WIP = 0
```

Changed status back to:

```text
Ready to Invoice
```

Result:

```text
Invoiced Flag = 0
WIP = 3,750
```

The dynamic WIP behaviour worked as expected.

The final task state was restored to:

```text
Build phase 1 = Ready to Invoice
```

## Issue encountered

Directly using the Invoice Status text/dropdown field inside the formula was not supported.

## Resolution

Used a numeric helper field plus Automations.

## Screenshots

- Screenshot #2 — Custom Field Manager showing the billing fields and folder-level configuration.
- Screenshot #3 — WIP Formula editor showing the working WIP formula.

---

# Day 3 — Reporting Views and Invoice Status Board

## Completed

Created reporting views to make the billing information easier to inspect.

## View 1 — Hours Variance

Created a List view named:

```text
Hours Variance
```

The view displays the billing information required to inspect the variance calculation.

Relevant columns include:

- Name
- Worked Hours
- Approved Hours
- Hourly Rate
- Hours Variance
- Invoice Status

All six required tasks are visible.

### Individual variance values

| Task | Worked | Approved | Variance |
|---|---:|---:|---:|
| Discovery workshop | 40 | 38 | 2 |
| Build phase 1 | 25 | 25 | 0 |
| Data migration | 60 | 52 | 8 |
| Support retainer | 15 | 15 | 0 |
| Integration design | 30 | 22 | 8 |
| UAT & rollout | 45 | 40 | 5 |

Expected total: **23 hours**

At this stage, the final screenshot still needed the ClickUp column calculation total to be made visible. This was completed during Day 4 after the Business trial was started.

## View 2 — WIP Report

Created a List view named:

```text
WIP Report
```

Applied the filter:

```text
Invoice Status ≠ Invoiced
```

The resulting report contains four tasks.

| Task | Approved Hours | WIP Hours | WIP |
|---|---:|---:|---:|
| Data migration | 52 | 52 | 6,240 |
| Build phase 1 | 25 | 25 | 3,750 |
| Support retainer | 15 | 15 | 1,800 |
| UAT & rollout | 40 | 40 | 8,000 |

Expected totals:

```text
WIP Hours = 132
WIP Value = 19,790
```

The two Invoiced tasks are correctly excluded:

```text
Discovery workshop
Integration design
```

This confirms the required behaviour that invoiced work should have zero WIP.

## View 3 — Invoice Status Board

Created a Board view named:

```text
Invoice Status Board
```

Grouped the board by:

```text
Invoice Status
```

Current groups:

### Invoiced

- Discovery workshop
- Integration design

### Ready to Invoice

- Data migration
- UAT & rollout
- Build phase 1

### Not Ready

- Support retainer

The board correctly reflects the current invoice statuses.

## Dynamic WIP testing

The `Build phase 1` task was temporarily changed:

```text
Ready to Invoice → Invoiced
```

The WIP changed to zero and the task was removed from the filtered WIP Report.

The task was then changed back:

```text
Invoiced → Ready to Invoice
```

The WIP value returned to:

```text
3,750
```

The final state was restored to the required assignment data.

## Issues / observations

The reporting views themselves work correctly.

However, the aggregate column calculation feature is not available on the current Free Forever plan. This limitation was tested further on Day 4.

## Screenshot

- Screenshot #6 — Invoice Status Board completed.

---

# Day 4 — Plan, Billing, Business Trial and Dashboard Testing

## Completed

Tested the current ClickUp plan, the Column Calculations limitation, the available Business trial, and the required billing dashboard calculations.

## Initial Column Calculation limitation

On the Free Forever plan, opened the `Hours Variance` view and attempted to calculate:

```text
Hours Variance → Sum
```

ClickUp displayed:

```text
Column Calculations isn't available on your current plan
```

and:

```text
Upgrade to Business to unlock Column Calculations
```

This confirmed that Column Calculations were restricted on the Free Forever plan.

## Billing / Upgrade investigation

Opened:

```text
Workspace Settings → Billing
```

The workspace initially showed:

```text
Free Forever
1 seat
$0 / seat
```

No payment method was configured.

The Upgrade / Plans page showed:

- Core
- Business
- Business Plus
- Enterprise

The Business plan displayed:

```text
$16/user/month
billed yearly
```

The paid checkout screen showed:

```text
Business Plan (1 seat) = $192/year
Tax (18%) = $34.56
Billed Today = $226.56
```

No payment details were entered and no paid upgrade was completed.

## Business free trial discovered

While adding a Calculation card to the dashboard, ClickUp displayed an explicit Business trial option.

The trial prompt stated:

- 15 day free trial
- No credit card required
- Business features would be available during the trial
- The displayed price to continue after the trial was $16/month

The **Start FREE trial** option was selected.

No credit card or payment method was added.

This provided a controlled way to test the paid features required by the assignment without purchasing a subscription.

## Column Calculations test after starting the trial

After starting the Business trial, created Calculation cards using the `Clients` data source.

The following calculations were successfully tested against the actual Nordvik Consulting task data:

### Total Hours Variance

```text
Measure: Hours Variance
Calculation: Sum
Result: 23
```

### Total WIP Hours

```text
Measure: WIP Hours
Calculation: Sum
Result: 132
```

### Total WIP Value

```text
Measure: WIP
Calculation: Sum
Result: 19,790
```

All three results matched the expected values from the configured Formula Fields and six required tasks.

## Dashboard created

Created the Nordvik billing dashboard with three headline Calculation cards:

```text
Total Hours Variance = 23
Total WIP Hours = 132
Total WIP Value = 19,790
```

The card titles were renamed so that each metric is clearly identifiable.

The dashboard provides a simple management-level view of billing leakage and work in progress.

## Screenshot evidence

- Screenshot #4 — Hours Variance view with the ClickUp calculated total of 23.
- Screenshot #7 — Dashboard showing the three headline numbers: 23, 132 and 19,790.

## Result

The required aggregate calculations were successfully tested during the Business free trial.

The earlier Free Forever limitation remains important evidence for the plan comparison and commercial assessment.

No paid subscription was purchased.

No payment method was added.

---

# Day 5 — R4 Country Holiday Calendars and Utilisation

## Completed

Tested ClickUp's Work Schedule capability against Nordvik Consulting's requirement for separate public-holiday calendars for Denmark, India and Sweden, with staff utilisation respecting each person's country.

## Test performed

Opened:

```text
Nordvik Consulting → Settings → Features → Work Schedule
```

The workspace showed the following restriction:

```text
Advanced Work Schedules isn't available on your current plan
Upgrade to Business Plus to unlock Advanced Work Schedules
```

No paid upgrade was made.

## Important requirement distinction

Nordvik's requirement is not only to display public holidays. The requirement is that each person's utilisation/capacity calculation should respect their own country's holiday calendar.

ClickUp can display national holiday calendars in Calendar view, but the Workspace work schedule used for Workload/utilisation does not provide independent country-specific capacity calendars for Denmark, India and Sweden within one Workspace.

The tested workspace also requires Business Plus for Advanced Work Schedules.

## Result / observation

The test confirmed that the requested per-country utilisation behaviour is not available as a straightforward native setup in the tested workspace.

This should be treated as a limitation rather than represented as a working native feature.

The final feasibility bucket is **CUSTOM BUILD** because separate country calendars driving utilisation would require a workaround, custom logic, or an external solution.

## Evidence

- Screenshot #8 — Country holiday / utilisation limitation showing the Advanced Work Schedules upgrade requirement.
- File: `screenshots/08-country-holidays.png`

## Customer-facing explanation

ClickUp can show the three countries' holidays, but making each employee's utilisation automatically follow their own country's holiday calendar requires a workaround or additional custom solution.

---

# Day 6 — AI Testing and Final Documentation Audit

## Completed

Completed the documented AI testing against the Nordvik workspace and performed the final documentation/evidence audit.

## AI testing

Tested Brain against the actual Nordvik billing data.

### Helpful case

Prompted Brain to identify the six billing tasks and summarise invoice status, approved hours and WIP value.

Observed result:

- All six required tasks were identified.
- Invoice statuses matched the configured workspace.
- Approved hours matched the task data.
- WIP values matched the Formula Fields.
- Total unbilled WIP was correctly summarised as **$19,790**.

### Negative / edge case

Asked Brain for an e-conomic invoice number and sent date for the `Integration design` task.

The workspace did not contain that information.

Brain correctly stated that the information was unavailable rather than inventing an invoice number or date.

This was recorded as a useful grounded limitation, not as a hallucination failure.

## AI limitation identified

The wider ClickUp AI surface was documented, but most capabilities were not independently tested against the Nordvik workspace.

Those capabilities remain explicitly marked **UNVERIFIED** rather than being presented as tested results.

This preserves research integrity and avoids inventing AI failures or successes.

## Final documentation / evidence issues found

### Issue 1 — WIP evidence

The WIP Report evidence needed both headline totals to be visibly supported in the final screenshot section.

Resolution:

- Used the original ClickUp WIP Report evidence.
- Combined it with the original ClickUp dashboard calculation evidence showing **132 WIP hours** and **$19,790 WIP value**.
- No ClickUp values were fabricated or edited.

### Issue 2 — AI conclusion

The AI report initially documented the test results but did not explicitly answer whether AI was worth paying for Nordvik.

Resolution:

Added a customer-facing conclusion based only on the AI testing actually completed. The conclusion states that a separate AI purchase is not justified solely by the tested billing workflow, while Brain is a useful secondary benefit if already included in the selected plan.

### Final feasibility buckets

The final feasibility conclusions were recorded as:

- R1 Hours Variance — **CONFIGURATION**
- R2 WIP Reporting — **CONFIGURATION**
- R3 e-conomic Accounting Sync — **CUSTOM BUILD**
- R4 Country-specific Utilisation — **CUSTOM BUILD**
- R5 Pricing — **NATIVE**

## Result

The final evidence set contains exactly 10 required screenshots.

The documentation explicitly distinguishes:

- what was tested;
- what was documented from official sources;
- what remains unverified;
- what requires configuration;
- what requires custom work.

No unsupported AI results or fabricated product failures were added.

---

# Current Status

## Completed

- Nordvik Consulting workspace
- Clients Space
- Clients Folder
- Client Alpha List
- Client Beta List
- Client Gamma List
- Six required task rows
- Worked Hours field
- Approved Hours field
- Hourly Rate field
- Invoice Status field
- Invoiced Flag helper field
- Hours Variance Formula
- WIP Hours Formula
- WIP Formula
- Invoice Status Automations
- Dynamic WIP testing
- Hours Variance view
- WIP Report view
- Invoice Status Board
- Business / Free plan limitation tested
- Billing / upgrade screen inspected
- No paid upgrade made
- 15-day Business free trial started without a credit card
- Dashboard Calculation cards tested
- Nordvik Billing Dashboard completed
- R4 country holiday / utilisation limitation tested
- Brain AI tested against Nordvik billing data
- Final AI value conclusion added
- Final documentation audit completed

## Screenshot progress

1. Space / Folder / three Lists
2. Custom Fields
3. WIP Formula
4. Hours Variance with total = 23
5. WIP Report with totals = 132 and 19,790
6. Invoice Status Board
7. Dashboard headline numbers
8. Country holiday / utilisation limitation
9. AI answering a Nordvik question
10. Actual error / plan limitation

## Final Documentation Audit

The final screenshot set is complete: all 10 required screenshots are captured.

Final feasibility buckets:

- R1 Hours Variance — CONFIGURATION
- R2 WIP Reporting — CONFIGURATION
- R3 e-conomic Accounting Sync — CUSTOM BUILD
- R4 Country-specific Utilisation — CUSTOM BUILD
- R5 Pricing — NATIVE

The final Screenshot #10 is the actual Custom Roles plan limitation:

> "Custom Roles isn't available on your current plan"

and

> "Upgrade to Business Plus to unlock a Custom Role."

The Free Forever Column Calculations limitation remains documented as historical Day 4 evidence and is not used as final Screenshot #10.
