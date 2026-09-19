
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
