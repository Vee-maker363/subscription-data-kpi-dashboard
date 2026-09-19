
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

6. Verification and sign-off. One open question surfaced during cleaning — whether repeated customer-ID submissions could ever be legitimate, or should always be treated as accidental resubmissions was raised with the data owner rather than assumed. Work continued on a working copy in parallel while awaiting a reply, with a clean baseline copy held in reserve. The approach was subsequently confirmed and approved.
