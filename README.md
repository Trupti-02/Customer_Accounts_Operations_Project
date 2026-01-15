# AR Master Data Analysis Pipeline

A Python-based data analysis pipeline that consolidates accounts receivable data from multiple sources into a unified dataset for Power BI reporting and analysis.

## Overview

This project integrates customer, invoice, payment, purchase order, and interaction data to create a comprehensive AR master dataset with calculated metrics for aging analysis, collection efficiency tracking, and customer risk assessment.

## Features

- **Multi-source data integration**: Combines 5 separate data sources into a single analytical view
- **Automated calculations**: Pre-calculates critical metrics including days past due, aging buckets, outstanding balances, and payment cycle times
- **Power BI ready**: Exports clean, structured data optimized for business intelligence reporting
- **Comprehensive data coverage**: Handles 20,000 invoices across 10,000 customers

## Data Sources

| Source | Records | Description |
|--------|---------|-------------|
| Customers | 10,000 | Master customer information including industry, location, and account status |
| Invoices | 20,000 | Billing transactions with amounts, dates, and status |
| Payments | 15,000 | Payment history with methods and amounts |
| Purchase Orders | 12,000 | Pre-invoice commitments with approval status |
| Customer Interactions | 18,000 | Communication logs including issue categories |

## Calculated Metrics

The pipeline generates the following derived fields:

- **outstanding_balance**: Invoice amount minus payment amount (with null handling)
- **days_past_due**: Days between due date and current date (0 if not overdue)
- **aging_bucket**: Categorization into 0-30, 31-60, 61-90, 91-120, 120+ day buckets
- **payment_cycle_days**: Time between invoice date and payment date

## Project Structure

.
├── data_analysis.ipynb          # Main analysis notebook
├── documentation/
│   ├── Data_Validation_Checklist.docx
│   └── Process_Improvement_Notes.docx
├── data/
│   ├── customers.csv
│   ├── invoices.csv
│   ├── payments.csv
│   ├── purchase_orders.csv
│   └── customer_interactions.csv
└── output/
    └── ar_master_powerbi.csv    # Final output for Power BI

## Requirements

pandas>=1.5.0
numpy>=1.23.0
jupyter>=1.0.0

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/ar-data-analysis.git
cd ar-data-analysis
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Place your data files in the `data/` directory

## Usage

### Running the Analysis

1. Open the Jupyter notebook:
```bash
jupyter notebook data_analysis.ipynb
```

2. Execute all cells to:
   - Load and validate source data
   - Merge datasets on customer_id and invoice_id
   - Calculate derived metrics
   - Export the AR master dataset

### Output

The pipeline generates `ar_master_powerbi.csv` containing 20,000 records with 18 columns:

- Invoice details: invoice_id, invoice_date, invoice_amount, due_date, invoice_status
- Customer information: customer_id, customer_name, industry, email, phone, city, account_status
- Payment data: payment_amount, payment_date
- Calculated metrics: outstanding_balance, days_past_due, aging_bucket, payment_cycle_days

## Data Validation

Before using the output in production reporting, complete the validation checklist in `documentation/Data_Validation_Checklist.docx` to ensure:

- Data completeness and integrity
- Accurate calculated fields
- Proper business logic implementation
- Output file quality

## Process Improvements

See `documentation/Process_Improvement_Notes.docx` for recommended enhancements including:

- Automation and scheduling
- Enhanced data validation
- Logging and audit trails
- Configuration management
- Performance optimization
- Advanced analytics features

## Key Metrics Enabled

The consolidated dataset supports analysis of:

- **Aging Analysis**: Distribution of receivables across aging buckets
- **Collection Efficiency**: Average payment cycle times by customer/industry
- **Risk Segmentation**: Identification of high-risk accounts based on payment patterns
- **DSO Tracking**: Days Sales Outstanding trends over time
- **Customer Behavior**: Payment velocity and late payment patterns

## Data Quality Standards

The pipeline enforces the following quality standards:

- No null values in critical fields (customer_id, invoice_id, invoice_amount)
- Valid customer_id relationships across all tables
- Unique identifiers for all primary keys
- Consistent date formats (YYYY-MM-DD)
- Non-negative monetary values
- Valid status codes (Open, Paid, Overdue for invoices; Active, On Hold for accounts)


**Last Updated**: January 2026  
**Version**: 1.0.0
