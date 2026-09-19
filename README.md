
# Customer Acquisition KPI Analysis

A data quality audit and 5-KPI analysis of a real-world customer acquisition dataset, built end-to-end in Excel and Power BI from a messy raw export to a self-contained, interactive report.

## Overview

This project analyses a subscription/sign-up dataset from a customer acquisition context, covering a 3-year reporting period (2023–2025). The brief was scoped to 5 specific business questions, not a general exploration of the data, which shaped every decision in the cleaning and analysis process: fix what the KPIs need, defer what they don't.

The dataset arrived genuinely messy: placeholder dropdown text captured as real answers, duplicate form submissions, a non-unique customer identifier, and inconsistent category labels. All of it is documented, not just fixed silently; see the audit trail in reports/customer_subscription_data_log.xlsx.

## Why This Project Matters

A brief with 5 fixed questions is a common real-world constraint, and it changes how a data quality audit should be used. A full audit will always surface more problems than any single task requires; the skill isn't just finding every issue, it's knowing which ones are actually in scope. On this project, roughly half of the logged data-quality issues turned out to be irrelevant to the 5 KPIs and were deliberately left alone; cleaning everything "because it's there" would have wasted effort without changing a single answer.

The project also documents its own reasoning as it went, including two places where an initial finding was later found to be incomplete or inconsistent and corrected; the process log keeps that history rather than quietly overwriting it.

## The 5 KPIs
1. Trend performance of the top 4 channels customers heard about the business through
2. Whether the referral (word-of-mouth) channel is a significant acquisition source
3. Which age range shows low signup counts, broken down by channel
4. Year-on-year percentage change comparing male and female signups
5. Which education levels the business should focus on, and from which countries

## Methodology

1. Data quality audit (Excel). Every column was profiled for structural issues, not just spot-checked: placeholder text sitting in the data as if it were a real answer, blank cells with ambiguous meaning, inconsistent category casing, and a customer-ID field that turned out not to be unique. Every issue was logged with the affected rows, its business impact, and a recommended fix. 20 issues in total.

2. KPI-driven scoping. Once the 5 KPIs were known, every logged issue was mapped to the specific KPI(s) it affects. This cut the active cleanup list roughly in half — most notably, an entire cluster of income-related fields turned out to be irrelevant to any of the 5 questions and were fully deferred, including the most complex problems in the dataset (a coded categorical field with no surviving lookup table, and a free-text numeric field with dozens of inconsistent formats).

3. Cleaning (Excel, Power Query). In-scope fixes were applied as Power Query steps rather than one-off manual edits, so each fix reruns automatically if the source data is refreshed: deduplicating by customer ID, filtering to the correct reporting window, recoding placeholder values, and standardising category labels. Every fix was verified against a row count predicted before running it, not just checked after the fact.

4. KPI calculation (Excel PivotTables). Each of the 5 KPIs was built as a pivot table directly against the cleaned data, so every number in the final report traces back to a formula.

5. Modelling and visualisation (Power BI). The full cleaning pipeline was rebuilt natively inside Power BI's own Power Query editor — importing the raw data directly rather than depending on the Excel working copy staying in its cleaned state, so the .pbix file is fully self-contained. Each KPI has its own report page; a Summary page pulls the headline visual from each, with button-based navigation connecting every page back and forth. Several KPIs go beyond drag-and-drop visuals with custom DAX measures, CALCULATE, FILTER, ALL, and DIVIDE combined to calculate dynamic %-of-total shares across categories, and a manual year-over-year comparison built the same way: the dataset's plain integer Year column doesn't support Power BI's built-in SAMEPERIODLASTYEAR, so each measure looks up its own previous-year value explicitly via a FILTER(ALL()) pattern.

6. Verification and sign-off. One open question surfaced during cleaning: whether repeated customer-ID submissions could ever be legitimate, or should always be treated as accidental resubmissions, was raised with the data owner rather than assumed. Work continued on a working copy in parallel while awaiting a reply, with a clean baseline copy held in reserve. The approach was subsequently confirmed and approved.

## Key Findings (Snapshot)
1. The top 4 acquisition channels are Facebook Ads, Instagram Ads, Friend (referral), and YouTube — but referral actually led every channel in the first year, only     overtaken once paid ad spend scaled up the following year.
2. Referral is a genuinely significant channel overall. The 3rd largest of 10, driving 17.55% of all signups across the 3-year period. A year that looks like a       decline in referral share is actually explained by a surge in paid ad volume, not a weakening of word-of-mouth.
3. The weakest age segment isn't uniform across channels: one bracket is consistently the softest spot for most channels, but the pattern isn't identical for         every channel, a finding only visible by breaking the data down by channel rather than looking at the age distribution alone.
4. The male/female signup split has been remarkably stable across all three years (a roughly 2:1 ratio, drifting by about one percentage point). A year-on-year       view of raw signup counts shows both genders swinging together in near-identical proportion, confirming the swing reflects overall traffic volume, not a real      shift in gender balance, and reinforcing rather than contradicting the share-based finding.
5. Two education levels account for over three-quarters of all signups, and a specific pairing of country and education level, not country alone, is where the        concentration really sits.
   
(Full detail and the reasoning behind each finding are in the Power BI report and the process documentation.)

## Tools Used
- Microsoft Excel — data quality audit, Power Query-based cleaning, and PivotTable KPI calculations
- Microsoft Power BI — self-contained data model, DAX measures, and the full interactive report
- Power Query (M) — used in both Excel and Power BI so every cleaning step is reproducible, not a manual one-off edit

## Reproducing This Project
- To explore the interactive report: open subscription_data_BI.pbix in Power BI Desktop (free). Use the Summary page's navigation buttons to move between each       KPI, or jump directly to any KPI's own page for the underlying detail view.
- To see the KPI calculations and cleaning steps: open customer_subscription_data.xlsx and review its Power Query steps (Data tab → Queries & Connections → Edit),   or the KPI_report sheet for the pivot-table calculations behind each KPI.
- To see the full audit trail: open customer_subscription_data_log.xlsx; it documents every data quality issue found, which were in scope for these 5 KPIs and       which were deferred, and a step-by-step process log of how the analysis was built, including two places where an initial finding was revisited and corrected.
- For a quick overview: subscription_data_presentation.pptx is a 10-minute-format summary deck covering the methodology and all 5 KPIs.

## Limitations & Notes
- This analysis is scoped specifically to the 5 KPIs listed above; several data quality issues in the source dataset are documented but intentionally left           unaddressed because no KPI in this task required fixing them.
- The dataset includes some very small nationality groupings (a handful of countries with only 1–2 signups). Current KPI visuals aggregate at a level where this     isn't exposed, but it's worth keeping in mind if this model is ever extended to country-level detail views.

