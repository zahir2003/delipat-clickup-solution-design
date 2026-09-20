# AI REPORT — ClickUp Solution Design

**Client:** Nordvik Consulting  
**Workspace:** Nordvik Consulting  
**Date checked:** 2026-09-19

## Scope

ClickUp describes Brain AI as the umbrella for AI capabilities across the platform, including Brain, Super Agents, AI Skills, AI Fields, Autopilot Agents, data analysis, image generation, Talk-to-Text and AI Notetaker. Current ClickUp documentation also notes that some Workspaces use newer plans with more AI included.

This report distinguishes:

1. Capabilities actually tested against Nordvik data.
2. Capabilities documented by ClickUp but not tested in this assignment.
3. Pricing/availability that is unverified for the Nordvik Early access workspace.

## Actual Nordvik tests

### Test 1 — Brain workspace retrieval / billing analysis

**Prompt**

> Using the Nordvik Consulting Clients workspace, identify the six billing tasks and summarize their invoice status, approved hours, and WIP value. Do not invent information that is not present in the workspace.

**Observed result:** Helpful and grounded.

Brain correctly returned:

- Discovery workshop — Invoiced — 38 approved hours — WIP $0
- Build phase 1 — Ready to Invoice — 25 approved hours — WIP $3,750
- Data migration — Ready to Invoice — 52 approved hours — WIP $6,240
- Support retainer — Not Ready — 15 approved hours — WIP $1,800
- Integration design — Invoiced — 22 approved hours — WIP $0
- UAT & rollout — Ready to Invoice — 40 approved hours — WIP $8,000

It also correctly summarized total unbilled WIP as **$19,790**.

**Assessment:** Helpful for grounded retrieval and summarisation of configured workspace data.

**Evidence:** `screenshots/09-ai-nordvik-answer.png`

### Test 2 — Missing accounting data

**Prompt**

> What is the e-conomic invoice number for the Integration design task, and when was that invoice sent? Answer only from information available in the Nordvik Consulting ClickUp workspace.

**Observed result:** Grounded limitation, not hallucination.

Brain stated that no e-conomic invoice number or sent date existed in the task/workspace data. It referenced the existing Invoice Status and Invoiced Flag but did not invent an invoice number or date.

**Assessment:** Useful refusal-to-invent behaviour.

This is a negative/edge-case test, but it is **not counted as a hallucination failure**. It demonstrates grounded behaviour; therefore hallucination resistance remains only partially tested.

**Evidence:** `screenshots/10-ai-e-conomic-limitation.png` if retained separately. The assignment's final Screenshot #10 remains the actual ClickUp plan limitation.

## AI capability inventory

| Capability | ClickUp documentation says | Nordvik test result | Status |
|---|---|---|---|
| Brain workspace Q&A | Context-aware answers over permitted Workspace data | Correct billing summary | **VERIFIED / TESTED** |
| Task summarisation / progress | Brain can summarise tasks and generate updates | Not separately tested | **UNVERIFIED** |
| AI writing | Brain can draft/edit content | Not separately tested | **UNVERIFIED** |
| AI Fields | AI Fields can generate task summaries/updates and other field content | Not separately tested | **UNVERIFIED** |
| AI Skills | Reusable saved instructions for Brain/Super Agents | Not separately tested | **UNVERIFIED** |
| Super Agents | Multi-step AI workflows with Workspace context | Not separately tested | **UNVERIFIED** |
| Autopilot Agents | Triggered agents can take configured actions | Not separately tested | **UNVERIFIED** |
| Data analysis | Brain/Super Agents can execute code in a sandbox to analyze data | Not separately tested | **UNVERIFIED** |
| AI Cards / dashboard AI | AI can support data/dashboard workflows | Dashboard calculations were tested, but not an AI-generated card | **UNVERIFIED** |
| Image generation/editing | Brain tools can generate/edit images | Not tested | **UNVERIFIED** |
| Talk-to-Text | Voice-to-text across ClickUp apps | Not tested | **UNVERIFIED** |
| AI Notetaker | AI meeting notes and related Q&A | Not tested | **UNVERIFIED** |
| Memory | Brain has customizable memory/preferences | Not tested | **UNVERIFIED** |
| External connections / MCP | Brain can use connected-app tools and MCP capabilities depending on plan | Not tested | **UNVERIFIED** |

## AI pricing / plan treatment

The Nordvik workspace's Early access Plans screen showed:

- **Business:** ClickUp Brain², premium models, unlimited standard models, 1,500 pooled credits/user/month.
- **Business Plus:** Brain², expanded premium model usage, unlimited standard models, 2,000 pooled credits/user/month.
- **Enterprise:** scaled AI, with 3,000 pooled credits/user/month shown in the workspace.
- **MAX:** maximum AI package. The workspace pricing screen and current public documentation use different AI-credit descriptions, so the exact Nordvik MAX credit allowance is treated as **UNVERIFIED unless the workspace screenshot is used as the direct evidence**.

The workspace did **not** show an Add-ons tab/button. Therefore the quote does not add older public Brain/Everything AI add-on prices to the Nordvik license cost.

ClickUp's documentation still describes separate Brain AI add-ons and AI credit pricing while also stating that some Workspaces have newer plans with more AI included. This packaging difference is recorded as a commercial uncertainty rather than silently reconciled.

## What the AI testing proves

The actual test proves that Brain can:

- retrieve the six configured Nordvik billing tasks;
- read the configured invoice status;
- read approved hours;
- read formula-derived WIP values;
- distinguish invoiced tasks from unbilled tasks;
- avoid inventing an e-conomic invoice number when the information is absent.

It does **not** prove the quality of every ClickUp AI capability. The untested capabilities are explicitly marked **UNVERIFIED**.

The accounting-data test also does not prove that hallucinations can never occur. It only shows that, in this test, Brain did not invent unavailable accounting information.

## Is AI worth paying for Nordvik?

Based on the testing completed, I would not recommend paying for AI as a separate purchase solely for Nordvik's billing workflow. Brain was useful for retrieving and summarising the configured billing data and for avoiding invented accounting information when the data was absent. However, only a limited part of ClickUp's wider AI surface was tested against the Nordvik workspace, so the evidence is not strong enough to justify an additional AI purchase on this workflow alone. If Nordvik selects a plan where Brain is already included, the tested retrieval and summarisation capability is a useful secondary benefit.

## Sources

- [ClickUp Brain AI feature availability and limits](https://help.clickup.com/hc/en-us/articles/20686299081879-ClickUp-Brain-AI-feature-availability-and-limits)
- [What is ClickUp Brain AI?](https://help.clickup.com/hc/en-us/articles/12578085238039-What-is-ClickUp-Brain-AI)
- [ClickUp Brain AI tools](https://help.clickup.com/hc/en-us/articles/33032484272023-What-are-ClickUp-Brain-AI-tools)
- [Perform data analysis with ClickUp Brain AI](https://help.clickup.com/hc/en-us/articles/41961766797207-Perform-data-analysis-with-ClickUp-Brain-AI)
- [Create items with Brain AI](https://help.clickup.com/hc/en-us/articles/19953994898711-Create-items-with-Brain-AI)
- [Use Brain AI on tasks](https://help.clickup.com/hc/en-us/articles/34958900405143-Use-Brain-AI-on-tasks)
- [AI Fields availability](https://help.clickup.com/hc/en-us/articles/33410992024855-AI-Fields-feature-availability-and-limits)
- [AI add-ons](https://help.clickup.com/hc/en-us/articles/40085008147863-Which-features-are-included-with-the-Brain-AI-add-ons)
- [New plans and pricing options](https://help.clickup.com/hc/en-us/articles/42972527662359-New-plans-and-pricing-options)
