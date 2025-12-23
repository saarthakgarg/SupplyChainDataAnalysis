## Project Overview

This project demonstrates how modern AI-first tools can be used to build a production-style supply chain analytics system.

The solution automates email-based data ingestion, stores data in a cloud PostgreSQL database, and enables prompt-driven analytics using an AI spreadsheet. The goal is to generate actionable supply chain KPIs such as OTIF, Fill Rates, and Delivery Performance across multiple countries.

The project is inspired by a real business scenario involving an FMCG company expanding from India to the USA and facing challenges in inventory availability and order fulfillment.

## Problem statement

Atlart (Atlique Mart) is a Gujarat-based organic food manufacturer that has successfully expanded its operations from India to the USA. Despite handling a limited product portfolio, the company is facing customer dissatisfaction due to poor order fulfillment and immature supply chain processes.

As operations scale across geographies, Atlart lacks: <br>
- Clear visibility into order and delivery performance<br>
- Reliable inventory and fulfillment metrics<br>
- A scalable, automated analytics system<br>

Traditional reporting approaches using Excel or BI tools are slow, manual, and insufficient for leadership’s need for real-time, AI-powered insights.

Leadership wants an AI-powered, scalable analytics solution that can:

- Automatically ingest daily sales data<br>
- Centralize data across geographies<br>
- Calculate critical supply chain KPIs<br>
- Answer business questions using natural-language prompts<br>

### Project Objectives

- Automate CSV ingestion from emails<br>
- Build a cloud-based analytics database<br>
- Enable AI-assisted data cleaning and modeling<br>
- Compute core supply chain performance metrics<br>
- Provide fast, prompt-based business insights<br>

### Architecture Overview

Email → n8n → PostgreSQL (Supabase) → Quadratic (AI Spreadsheet)

1. Daily sales CSV files are received via email
2. n8n monitors inbox and extracts attachments
3. Data is transformed and loaded into PostgreSQL
4. Quadratic connects directly to the database
5. Analytics and KPIs are generated using AI prompts

### Tech Stack

| Layer | Tools |
| ------------- | ------------- |
| Automation | n8n |
| Database | PostgreSQL (Supabase) |
| Analytics | Quadratic (AI Spreadsheet) |
| Languages | Python (Pandas), SQL |
| Data Format | CSV, JSON |
| APIs | OpenExchangeRates (USD ↔ INR) |

### Data Model

Fact Tables
- fact_orders_aggregate – Order-level data
- fact_order_line – Item-level order details

Dimension Tables
- dim_customers
- dim_products
- dim_targets_orders
- dim_date (AI-generated)

Derived Tables
- exchange_rates
- fact_summary (denormalized analytics table)

<p align="center">
    <img src='https://github.com/saarthakgarg/SupplyChainDataAnalysis/blob/main/resources/ETL%20Workflow.png' width="800">
</p>

<p align="center">
    <img src='https://github.com/saarthakgarg/SupplyChainDataAnalysis/blob/main/resources/ETL%20Workflow.png' width="800">
</p>


### ETL Workflow (n8n)

1. Monitors a Gmail inbox for incoming sales emails using a trigger-based workflow
2. Validates incoming attachments to ensure only CSV files are processed
3. Generates a unique hash for each file to prevent duplicate ingestion 
4. Checks file hash against PostgreSQL to detect already processed files 
5. Filters out duplicate files using conditional branching logic 
6. Stores new file hashes in the database for idempotent processing 
7. Merges and cleans incoming JSON data for consistent downstream handling
8. Uses rule-based switching to route aggregate vs line-level datasets
9. Extracts order aggregate & order line CSV attachments (India & USA)
10. Convert CSV → JSON
11. Load data into PostgreSQL tables
12. Support incremental daily loads

<p align="center">
    <img src='https://github.com/saarthakgarg/SupplyChainDataAnalysis/blob/main/resources/ETL%20Workflow.png' width="800">
</p>

### Analytics & KPIs

The following supply chain KPIs are calculated and validated:

- Total Orders
- Total Order Lines
- Line Fill Rate
- Volume Fill Rate
- On-Time Delivery %
- In-Full Delivery %
- OTIF (On-Time In-Full)
- Customer Reliability Metrics
  
All KPI calculations are domain-validated, not blindly trusted from AI output.

## Revenue Dashboard - Overall Analysis View

<p align="center">
    <img src='https://github.com/saarthakgarg/RevenueInsights-HospitalityDomain/blob/main/resources/Revenue%20Dashboard.png' width="600">
</p>


## Business Outcomes 
