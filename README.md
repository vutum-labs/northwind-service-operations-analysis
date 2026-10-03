# Northwind Service Operations Analysis

**Hack the Hill 2026 · Business / Data Analysis**

A case study of the business-analysis contribution to Northwind's customer-service project: evaluating pilot performance, framing operational costs, and developing a value case for the final pitch. The team's related prototype connected a customer chat widget to a human-agent desk and completed a documented end-to-end rehearsal with real Gemini calls.

**Documented team results:** three bugs fixed, **145 passing tests**, and **18/18 live tests**, as reported in merged [backend PR #47][pr47]. These are historical prototype-validation results, not measured business benefits.

## Problem

Northwind wanted to understand whether its AI/customer-service pilot was improving operational performance and whether further investment was financially justified.

The business question was whether the service actually resolved customer needs at an acceptable cost. A response from the assistant alone would not establish that outcome: the team's domain definitions distinguish customer-confirmed resolution, hand-off to a human, and an unconfirmed answer. Only confirmed auto-resolutions without a subsequent Support Case in the same conversation qualify for handling-cost savings in that definition. [3]

## My contribution: Business / Data Analysis

My role covered financial impact analysis, operational cost modelling, value-case development, interpreting pilot performance, and translating findings into recommendations for the final pitch. I developed the financial analysis/value case. These responsibilities are recorded in the [original project README][original].

This is a self-reported contribution record. This repository currently publishes the case study only; it does not contain the underlying notebooks, datasets, charts, or completed financial model needed to independently reproduce the analysis.

The backend implementation, browser rehearsal, bug fixes, and test results below are **team-project outcomes**. PR #47 was authored by **Theedon**; it does not establish my authorship of that engineering work.

## Analysis and findings

The original README records that complaints rose throughout the pilot period. Without the supporting monthly data or calculations in this repository, that remains a reported analytical finding: its magnitude, month-by-month pattern, and relationship to the pilot cannot be independently checked here. It does not establish that the AI pilot caused the increase.

The financial-analysis contribution addressed the connection between service activity and cost. The engineering evidence addresses a separate question: whether the proposed customer-to-agent workflow worked in the documented rehearsal. Neither substitutes for a measured evaluation of business impact.

## Financial model: framework and limits

The original README specifies the following cost framework:

```text
Activity cost = activity volume × unit cost
Incremental cost = observed cost − baseline cost
```

For a meaningful comparison, both costs need a consistent period, scope, and baseline. A positive incremental cost means higher cost relative to that baseline; a negative value means lower cost. This arithmetic alone does not attribute the difference to the AI pilot.

The published evidence does not supply the inputs or completed calculations needed to state total pilot cost, net savings, ROI, or payback. No financial total is claimed here. The bill amounts in PR #47 are customer-level demonstration values, not project savings or investment returns.

## Team solution and recommendation rationale

The documented team solution combined an AI Assistant for supported self-service requests with a human-agent workflow for cases requiring intervention. A Unified Customer History brought together billing, metering, CRM, and case information; shared triage rules determined urgency, queue, and response date. Plausible meter readings could trigger a bill recalculation by code, while readings requiring review and explicit requests for a person went to a Human Agent. [2][3]

This design connects the business question to observable service outcomes: whether the customer confirms resolution, whether a case is handed off correctly, and whether the customer can follow its progress. The rehearsal demonstrated those paths, including a case-status reply after human resolution. [1]

The repository evidence supports this description of the implemented approach. It does not establish the final pitch's exact investment recommendation, an approved rollout, or a quantified return.

## Verified team outcomes

[PR #47][pr47], merged on **27 September 2026**, documents a Playwright browser rehearsal of the customer widget and agent desk against the backend with real Gemini calls, mock API mode disabled, and a fresh demo database.

| Evidence | Reported result | Scope |
| --- | --- | --- |
| Automated suite | **145 passing tests** via `uv run pytest` | Historical result reported by the PR author; the backend README describes this suite as using faked Gemini calls. |
| Live suite | **18/18 live tests** | Real Gemini calls, including a new hand-off regression test. |
| Integration defects | **Three bugs fixed**, with regression coverage | Bill-breakdown crash; duplicate case after a hand-off; desk transcript/timeline presentation and attribution. |
| Duplicate-case replay | Misclassification changed from **4/5** replays before the fix to **0/5** after | One captured conversation replayed five times per version; not a general accuracy estimate. |
| Customer-to-agent workflow | Billing explanation, reading submission, hand-off, assignment, resolution, and subsequent status lookup completed | End-to-end demonstration, not a production deployment. |
| Queue and reset | Resolving the demo case changed the open count from **297 to 296**; reset restored **1,321 seeded cases** | Demo state changes, not evidence of operational backlog reduction. |

The three fixes addressed concrete service failures:

- **Bill breakdown:** omitted absent optional numeric fields instead of sending null values that crashed the widget.
- **Case continuity:** supplied data-free summaries of prior assistant actions and classified the latest message, preventing the reproduced case-status question from creating another case.
- **Agent desk:** removed literal bold markers from transcripts, made resolution labels readable, and credited changes to the assigned agent.

The backend documentation explicitly describes the desk seed as invented demo data and the legacy-system integrations as mocks. Real backend and model calls therefore demonstrate integration behavior, not live customer-service performance. [2]

## Tools

The original README lists **Python, pandas, Jupyter, Excel / CSV analysis, and Git/GitHub** for the analysis work. [4]

The related team backend uses **FastAPI, LangGraph, Gemini, and pytest**; PR #47 documents **Playwright** for the browser rehearsal. These describe the team implementation and validation stack, not additional individual contribution claims. [1][2]

## Retrospective

The documented rehearsal illustrates why an integrated customer journey matters: it exposed failures that the existing unit tests had missed, including a duplicate case created after a hand-off. Regression tests then captured the corrected behavior.

For the business case, the central lesson is to keep functioning software, confirmed service resolution, and financial benefit as separate claims. A successful demo establishes a narrower result than sustained cost reduction. The next improvement to this portfolio would be to publish shareable analysis artifacts with traceable inputs, baseline definitions, calculations, and assumptions so that the financial conclusions can be reproduced.

## Evidence and limitations

This case study distinguishes self-reported analysis responsibilities from engineering changes visible in the linked PR. Test totals are the author's reported results at that point in time; they have not been rerun for this README update. No production reliability, causal improvement in complaints, realized savings, or personal ownership of team engineering work is asserted.

Sources are pinned where possible to preserve the evidence used:

1. [Backend PR #47: rehearsal, fixes, test results, and authorship][pr47].
2. [Backend README at the PR #47 merge commit][backend].
3. [Domain definitions at the PR #47 merge commit][context].
4. [Original analysis README: role, reported finding, cost framework, and tools][original].

[pr47]: https://github.com/MAT-HTH3/northwind_backend/pull/47
[backend]: https://github.com/MAT-HTH3/northwind_backend/blob/5397cb6548fa15ab219511672618831e3846ff79/README.md
[context]: https://github.com/MAT-HTH3/northwind_backend/blob/5397cb6548fa15ab219511672618831e3846ff79/CONTEXT.md
[original]: https://github.com/vutum-labs/northwind-service-operations-analysis/blob/63979733a1539359c87b88588b1ea9dea11ee6db/README.md
