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

### 📊 Data Model

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

## Revenue Dashboard - Overall Analysis View

<p align="center">
    <img src='https://github.com/saarthakgarg/RevenueInsights-HospitalityDomain/blob/main/resources/Revenue%20Dashboard.png' width="600">
</p>


## Business Outcomes 
