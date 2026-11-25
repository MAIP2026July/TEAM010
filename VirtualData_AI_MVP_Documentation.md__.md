# VirtualData AI

## Enterprise Chatbot on Top of a Data Virtualization Layer

**Course:** MBA ZG583 - Management of AI Products  
**Capstone:** Functional MVP  
**Team Name:** VirtualData AI  
**Team Members:** Tapan Kumar Mohapatra, R Subith  
**Working Title:** Enterprise Chatbot on Top of a Data Virtualization Layer

---

## 1. About the Project

VirtualData AI is a functional academic MVP demonstrating how authorized business users can ask questions in natural language and receive answers grounded in a governed data-virtualization layer.

Enterprise information is commonly distributed across ERP systems, CRM platforms, data warehouses, cloud databases, APIs, and departmental applications. Business users may understand the question they want answered but may not know which source, table, report, or technical query is required.

The MVP demonstrates this workflow:

```text
Business Question
      -> Intent Interpretation
      -> Business / Semantic Mapping
      -> Governance Validation
      -> Approved Virtualized View
      -> Controlled Read-Only Query
      -> Validated Result
      -> Explainable Business Response
```

The prototype intentionally uses synthetic data so that it can be demonstrated without enterprise credentials, confidential information, or production-system access.

---

## 2. Product Hypothesis

> If authorized business users can ask questions in natural language and receive responses grounded in governed virtualized data, then an organization can reduce data-discovery effort and repeated analyst dependency while preserving security, traceability, and human oversight.

---

## 3. Problem Being Solved

A typical enterprise data question can require a user to:

1. Identify which system contains the data.
2. Find the correct report, dashboard, table, or data owner.
3. Request support from an analyst or technical team.
4. Translate the business question into SQL or another technical query.
5. Combine information from multiple systems.
6. Validate business definitions, filters, and calculations.
7. Confirm access permissions.
8. Interpret and present the result.

This can make simple business questions slow and dependent on specialists. It may also result in inconsistent definitions, outdated spreadsheet extracts, and difficulty verifying how an answer was produced.

VirtualData AI evaluates whether conversational access combined with governed virtualized data can reduce this friction.

---

## 4. Target Users

### Primary Users

- Business analysts
- Finance users
- Operations users
- Supply-chain users
- Sales users
- Engineering and other enterprise data consumers
- Users familiar with business terminology but not necessarily SQL

### Secondary Users

- Data stewards
- Data engineers
- Data-product owners
- Platform administrators
- Governance teams

The product assists authorized users. It is not designed to bypass security controls, reports, data-owner approvals, or governance processes.

---

## 5. Smallest Credible MVP

The MVP focuses on a narrow synthetic business domain containing:

- Customers
- Invoices
- Orders
- Payments
- Receivables

The purpose is not to support every enterprise question. It is to prove the core product workflow on a small set of representative use cases.

A user can enter a supported natural-language question and receive:

- A concise answer
- Supporting result data
- The virtualized view used
- Applied filters
- Authorization status
- The controlled SQL query
- Safe clarification or rejection where appropriate

---

## 6. Functional Capabilities

The prototype includes:

- Streamlit web interface
- Natural-language business questions
- Intent identification
- Business-term interpretation
- Geographic filter extraction
- Synthetic enterprise datasets
- Governed SQLite virtual views
- Approved data-product mapping
- Role-based authorization
- Controlled parameterized SQL
- Read-only access patterns
- Supporting result tables
- Source/view transparency
- Query transparency
- Ambiguity handling
- Safe unsupported-request handling
- Safe unauthorized-request handling
- Automated tests

---

## 7. Why Synthetic Data?

The repository deliberately contains no production or confidential enterprise information.

Synthetic data makes the MVP:

- Safe to publish to GitHub
- Independent of corporate network connectivity
- Free of real customer or employee information
- Independent of enterprise credentials and secrets
- Easy for faculty or reviewers to run
- Focused on product behavior rather than infrastructure access

The synthetic model represents realistic relationships among customers, invoices, payments, orders, regions, outstanding amounts, and fulfillment statuses.

---

## 8. MVP Architecture

```text
Enterprise User
      |
      v
Streamlit Conversational Interface
      |
      v
Intent Interpreter
      |
      v
Semantic / Policy Mapping
      |
      v
Governance Validator
 - Role check
 - Approved view selection
 - Validated query pattern
      |
      v
Simulated Data Virtualization Layer
 - Governed SQLite views
      |
      v
Synthetic Enterprise Data
 - Customers
 - Invoices
 - Orders
 - Payments
      |
      v
Explainable Response
 - Answer
 - Supporting table
 - View used
 - Filters
 - Authorization
 - Controlled query
```

---

## 9. Simulated Data-Virtualization Layer

SQLite is used to simulate the governed data-virtualization layer for the academic MVP.

The conversational application uses approved business-oriented views rather than treating raw source files as unrestricted chatbot data.

Representative approved views include:

- `vw_customer_receivables`
- `vw_order_status`
- `vw_customer_activity`

These demonstrate capabilities expected from a governed virtualization layer, including source abstraction, reusable joins, business-oriented structures, and controlled access patterns.

A production implementation could replace the SQLite simulation with an enterprise data-virtualization platform while retaining the same product workflow.

---

## 10. Controlled Query Design

A central design principle is that the chatbot does **not execute arbitrary AI-generated SQL**.

The request is first converted into a supported intent. The application then chooses a validated query pattern and supplies controlled parameters.

Example user request:

```text
Show overdue invoices for the Western region.
```

Interpreted request:

```json
{
  "intent": "overdue_invoices",
  "region": "Western"
}
```

Controlled query pattern:

```sql
SELECT *
FROM vw_customer_receivables
WHERE status = 'OVERDUE'
  AND region = ?;
```

The region is passed as a parameter instead of being used to construct unrestricted SQL.

This demonstrates separation between natural-language interpretation and deterministic data access.

---

## 11. Governance Demonstration

The prototype contains three demonstration roles:

- Finance Analyst
- Sales Analyst
- Operations Analyst

Before executing a query, the governance component checks whether the selected role is allowed to access the required virtual data product.

For example, the MVP can block an Operations Analyst from accessing a receivables data product.

An unauthorized request results in an **Access Restricted** message instead of query execution.

This demonstrates the principle that authorization is enforced outside the conversational interpretation layer.

---

## 12. Semantic Definitions and Ambiguity Handling

The repository includes a small business glossary.

### Overdue Invoice

An unpaid invoice with status `OVERDUE`.

### Outstanding Amount

Calculated as:

```text
Invoice Amount - Paid Amount
```

### Revenue

Revenue is intentionally treated as ambiguous because organizations may have multiple valid definitions.

If the user asks:

```text
Show revenue for last month.
```

The MVP requests clarification rather than selecting a definition silently.

This is an important human-in-the-loop behavior because a fluent answer based on the wrong business definition can be misleading even if the underlying query executes correctly.

---

## 13. Demonstration Scenarios

### Scenario 1 - Overdue Invoices

```text
Show overdue invoices for the Western region.
```

Demonstrates intent recognition, region extraction, approved view selection, governance validation, controlled query execution, and explainable results.

### Scenario 2 - Outstanding Amount

```text
What is the total outstanding amount by region?
```

Demonstrates aggregation of governed receivables information.

### Scenario 3 - Cross-Domain Question

```text
Which customers have overdue invoices and pending orders?
```

Demonstrates a reusable virtual view combining invoice and order information.

### Scenario 4 - Delayed Orders

```text
Show delayed orders for the Western region.
```

Demonstrates operational data filtering.

### Scenario 5 - Ambiguity

```text
Show revenue for last month.
```

Expected behavior: ask for clarification rather than assume a revenue definition.

### Scenario 6 - Restricted Request

```text
Show customer credit limits.
```

Expected behavior: controlled rejection according to the MVP governance configuration.

---

## 14. Explainability

A successful request presents both the result and information describing how it was produced.

The interface can display:

- Interpreted intent
- Extracted region or filters
- Approved virtual view
- Authorization result
- Controlled SQL query
- Query parameters
- Supporting records

The objective is to make the answer inspectable rather than presenting generated language as an unexplained authoritative result.

---

## 15. Human-in-the-Loop Design

The MVP does not automatically approve or perform financial, customer, operational, or source-system transactions.

The human user remains responsible for interpreting and acting on the information.

The system is designed to clarify, reject, or escalate when:

- The request is ambiguous
- A supported business definition is unavailable
- The required data product is unauthorized
- The request falls outside validated query patterns
- Sufficient grounding is unavailable

---

## 16. Responsible AI Principles

### Grounded

Structured factual responses are derived from validated query results.

### Explainable

The selected view, request interpretation, and controlled query can be inspected.

### Secure by Design

Authorization is checked before data retrieval.

### Human Controlled

The chatbot assists with information access but does not autonomously perform high-impact actions.

### Privacy Aware

Only synthetic data is included in the academic MVP.

### Fail Safe

Unsupported, ambiguous, and unauthorized requests are clarified or rejected rather than answered using unsupported assumptions.

### Auditable Design

The interpreted intent, selected view, parameters, and query can be examined during the demonstration.

---

## 17. Repository Structure

```text
VirtualData-AI/
|
|-- app.py
|-- README.md
|-- MVP_README.md
|-- requirements.txt
|-- LICENSE
|-- .gitignore
|
|-- virtualdata/
|   |-- __init__.py
|   |-- database.py
|   |-- intent.py
|   |-- governance.py
|   |-- query_builder.py
|   `-- response.py
|
|-- data/
|   |-- customers.csv
|   |-- invoices.csv
|   |-- orders.csv
|   `-- payments.csv
|
|-- config/
|   |-- business_glossary.json
|   |-- approved_views.json
|   `-- roles.json
|
|-- tests/
|   `-- test_mvp.py
|
`-- docs/
    |-- architecture.md
    |-- responsible_ai.md
    `-- test_scenarios.md
```

---

## 18. Technology Stack

| Component | MVP Technology |
| --- | --- |
| Programming language | Python 3.10+ |
| Web interface | Streamlit |
| Data processing | Pandas |
| Virtualization simulation | SQLite |
| Synthetic data | CSV |
| Governance | Python policy logic |
| Query mechanism | Controlled parameterized SQL |
| Testing | pytest |
| Source control | GitHub |

The stack is intentionally lightweight so the evaluator can run the prototype without specialized enterprise infrastructure.

---

## 19. Prerequisites

Install:

- Python 3.10 or later
- Git

The supplied academic MVP does not require a production database, enterprise login, or confidential credentials.

---

## 20. Installation

Clone the GitHub repository:

```bash
git clone <your-repository-url>
cd VirtualData-AI
```

Create a virtual environment:

```bash
python -m venv .venv
```

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

### macOS/Linux

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 21. Run the MVP

Start the Streamlit application:

```bash
streamlit run app.py
```

Streamlit will provide a local URL, normally:

```text
http://localhost:8501
```

Open the URL in a browser.

1. Select a demonstration role.
2. Enter one of the supported questions.
3. Select **Ask VirtualData AI**.
4. Review the result and supporting data.
5. Expand the explanation section to review the selected view, authorization, and query.

---

## 22. Automated Tests

Run:

```bash
pytest -q
```

The included tests validate representative MVP behavior such as:

- Intent and region identification
- Governance restrictions
- Controlled receivables-query execution
- Expected calculation from synthetic data

---

## 23. Synthetic Data Model

### Customers

Representative fields:

- Customer ID
- Customer name
- Region
- Segment
- Credit limit

### Invoices

Representative fields:

- Invoice ID
- Customer ID
- Invoice date
- Due date
- Invoice amount
- Paid amount
- Status

### Orders

Representative fields:

- Order ID
- Customer ID
- Order date
- Expected ship date
- Actual ship date
- Order amount
- Status

### Payments

Representative fields:

- Payment ID
- Invoice ID
- Payment date
- Payment amount
- Payment method

All names, identifiers, transactions, amounts, and records in the repository are synthetic and intended only for academic demonstration.

---

## 24. Success Evidence

The MVP is designed to demonstrate:

1. **Natural-language understanding** - representative business questions can be mapped to supported intents.
2. **Grounded responses** - structured answers are based on query results.
3. **Controlled queries** - queries are selected from approved patterns rather than unconstrained SQL generation.
4. **Security preservation** - role validation occurs before data retrieval.
5. **Explainability** - the view, filters, authorization result, and query can be inspected.
6. **Ambiguity handling** - the system can request clarification instead of guessing.
7. **Reduced technical dependency** - supported questions do not require a user to write SQL.
8. **Safe failure behavior** - unsupported and restricted requests do not execute unrestricted queries.

---

## 25. MVP Non-Goals

The initial MVP does not attempt to:

- Connect to real enterprise datasets
- Replace enterprise dashboards or BI platforms
- Replace a production data-virtualization platform
- Provide unrestricted database access
- Execute arbitrary AI-generated SQL
- Make autonomous financial or operational decisions
- Update source-system records
- Implement full production enterprise authentication
- Support every natural-language question
- Support every enterprise business domain
- Train a foundation model
- Use the language model as the security-enforcement layer

These are deliberately outside the smallest credible MVP.

---

## 26. Main Risks and Controls

| Risk | MVP / Product Control |
| --- | --- |
| Hallucinated factual answers | Ground structured answers in query results |
| Incorrect queries | Use approved query patterns |
| Ambiguous terminology | Clarify rather than guess |
| Unauthorized access | Validate role before query execution |
| Unsafe generated SQL | Do not execute unrestricted model-generated SQL |
| Sensitive information exposure | Use synthetic data in the academic prototype |
| Automation bias | Show view/query/context used |
| Unsupported request | Fail safely |
| Incorrect business interpretation | Display interpreted intent and filters |

---

## 27. Build vs Buy vs API View

### Build

Product-specific components include:

- Business-language interpretation
- Mapping questions to data products
- Clarification workflow
- Governance orchestration
- Query-validation workflow
- Explainability experience
- Feedback workflow

### Reuse / Buy in a Production Architecture

An enterprise solution could reuse existing capabilities for:

- Identity and access management
- Production data virtualization
- Data catalog and business glossary
- Foundation-model services
- Secrets management
- API management
- Monitoring
- Audit logging

### API Integration

APIs can provide controlled interaction among:

- Conversational application
- AI/model service
- Authentication services
- Data-virtualization platform
- Metadata/catalog services
- Monitoring and audit systems

The product value lies mainly in governed enterprise-data grounding, semantic mapping, explainability, and workflow integration rather than training a new foundation model.

---

## 28. Future Production Evolution

Possible future enhancements include:

1. Enterprise identity integration
2. Production data-virtualization integration
3. Enterprise glossary and metadata integration
4. LLM-assisted entity and intent extraction
5. Approved semantic-definition retrieval
6. Row-level and column-level security
7. Audit logging
8. Prompt-injection defenses
9. Query row and cost limits
10. Model and query observability
11. Additional business domains
12. Persistent feedback collection
13. Query-correctness benchmark datasets
14. Escalation to data stewards or analysts
15. Production-scale performance and caching controls

The core architectural principle remains:

> **AI interprets and explains; deterministic governance controls authorization, data access, and execution.**

---

## 29. Key Product Demonstration

The MVP is not intended merely to show that a chatbot can generate SQL.

The important distinction is the separation of responsibilities:

```text
Conversational / AI Layer
      |
      | Understand and explain
      v
Governance Layer
      |
      | Authorize and validate
      v
Data Virtualization Layer
      |
      | Govern and abstract
      v
Enterprise Data Sources
```

This architecture allows conversational interaction without treating the AI model as an unrestricted database interface or security-enforcement mechanism.

---

## 30. Expected Product Outcome

The capstone evaluates whether a governed enterprise chatbot can make distributed enterprise information easier to access without removing the controls provided by the data-virtualization layer.

The MVP demonstrates the core workflow:

> **Business question -> governed data interpretation -> virtualized query -> validated result -> explainable response**

---

## 31. Academic and Data Disclaimer

This project is an academic MVP developed for **MBA ZG583 - Management of AI Products**.

All datasets bundled with the project are synthetic. They do not represent actual customers, employees, invoices, orders, payments, companies, or financial results.

The SQLite layer provides a lightweight simulation of a governed data-virtualization architecture and should not be interpreted as a production deployment.

---

## Team

**Team Name:** VirtualData AI  
**Tapan Kumar Mohapatra(2025MB26161)**  
**R Subith(2025MB26120)**

**Working Title:** Enterprise Chatbot on Top of a Data Virtualization Layer
