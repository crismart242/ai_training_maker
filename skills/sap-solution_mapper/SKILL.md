---
name: sap-solution-mapper
description: >-
  Helps users navigate the SAP solution portfolio using a reference CSV.
  Works in two directions: given a business challenge, it identifies the most
  relevant SAP product; given a solution name, acronym, or code, it explains
  what it does and where it fits. Activate on any question involving SAP products
  or the mapping between business processes and the SAP portfolio.
allowed-tools: read_file
metadata:
  author: SAP Learning Team
  tags: sap portfolio solutions products
---

# SAP Solution Mapper

This skill uses `references/sap-solutions.csv` as its knowledge base.

## Reference Data

Load `references/sap-solutions.csv` at the start of every interaction.
The CSV contains the following columns:

- `product_name` — Full product name (e.g. SAP S/4HANA)
- `product_code` — Short code or acronym (e.g. S4H, BTP)
- `category` — High-level category (e.g. ERP, Analytics, Integration)
- `business_area` — Business domain covered (e.g. Finance, Supply Chain, HR)
- `description` — Plain-language summary of what the solution does
- `key_processes` — Comma-separated list of supported business processes

## Mode 1 — Business Challenge to Solution

When the user describes a business need, problem, or process:

1. Search the CSV for solutions whose `key_processes` or `business_area` match the user's description.
2. Return the 1–3 most relevant matches.
3. For each match, present: product name, code, and a one-sentence explanation of why it fits.

## Mode 2 — Solution Lookup

When the user mentions a product name, acronym, or code:

1. Look it up in the CSV using `product_name` or `product_code` (partial matches are acceptable).
2. Return: full name, category, business area, and description.
3. If no exact match is found, suggest the closest entry and ask the user to confirm.

## Output Format

Present results in a short Markdown table, followed by a brief paragraph summary.
If no match is found, say so clearly and invite the user to rephrase their need.
