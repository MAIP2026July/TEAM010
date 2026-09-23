# MBA ZG583: Management of AI Products

## Capstone: Topic Approval Form

### Team Name

**VirtualData AI**

### Team Members

- **Tapan Kumar Mohapatra**
- **R Subith**

### Working Title

**Enterprise Chatbot on Top of a Data Virtualization Layer**

### Industry / Function

**Enterprise Data and Analytics / Data Management / Generative AI**

The proposed product focuses on enterprise data discovery and conversational analytics. It enables authorized business users to interact with distributed enterprise information through natural-language questions while using a data virtualization layer as the governed access and integration foundation.

The solution is relevant to organizations that maintain information across multiple operational systems, databases, cloud data platforms, applications, and business domains.

### Target User

**Primary users:**

- Business analysts who need information from multiple enterprise data sources
- Finance, operations, supply-chain, sales, and engineering users who require frequent operational insights
- Data consumers who understand business terminology but may not know SQL or the physical location of the required data

**Secondary users:**

- Data stewards responsible for data definitions and access governance
- Data engineers responsible for maintaining reusable data products and virtualized data views
- Platform administrators responsible for monitoring security, usage, performance, and compliance

The product is intended to assist authorized enterprise users. It is not designed to bypass existing reporting systems, security controls, data-owner approvals, or governance processes.

### Current Workflow Problem

Enterprise information is distributed across databases, cloud platforms, ERP systems, data warehouses, APIs, and departmental applications.

When a business user needs an answer, the current workflow frequently involves:

1. Identifying which system contains the required data
2. Finding the appropriate report, dashboard, table, or data owner
3. Raising a request with an analyst or technical team
4. Translating the business question into SQL or another technical query
5. Combining information from multiple systems
6. Validating definitions, filters, calculations, and access permissions
7. Preparing the final response for the business user

This workflow is slow and highly dependent on technical specialists. Different users may also interpret the same business term differently or use data from inconsistent sources.

Even when dashboards are available, users must know which dashboard to open, which filters to apply, and how the displayed metrics are defined.

### Why This Matters

Delayed access to trusted information can slow business decisions and increase dependency on data and analytics teams.

The absence of a unified conversational access layer creates several challenges:

- Business users spend time searching for the correct report or data source
- Analysts repeatedly answer similar data questions
- Different teams may calculate the same metric differently
- Users may rely on downloaded spreadsheets or outdated extracts
- Data access decisions may not have a consistent audit trail
- Direct chatbot-to-database implementations may expose technical schemas or generate unsafe queries
- Answers may be difficult to verify when the source, filters, or calculation logic is not shown

A governed enterprise chatbot could reduce this friction by converting a business question into an approved data request, retrieving information through the data virtualization layer, and presenting an understandable answer with supporting context.

### Proposed AI Role

The AI will perform **natural-language interpretation, query planning, controlled query generation, answer summarization, and clarification**.

For each user question, the proposed system will:

1. Identify the user's business intent
2. Recognize relevant business entities, metrics, filters, and time periods
3. Match the question to approved virtualized views or semantic definitions
4. Generate or select a controlled query against the data virtualization layer
5. Validate the query against security and governance rules
6. Retrieve the permitted data
7. Present the result in business-friendly language
8. Display the source, filters, assumptions, and query context used
9. Ask a clarification question when the original request is ambiguous

The chatbot acts as a **decision-support and data-access copilot**, not as an autonomous decision-maker or an unrestricted database interface.

### Why AI Instead of a Simpler Alternative

A conventional search interface can locate reports or documents, but it cannot reliably interpret varied business questions such as:

- "Show overdue customer invoices by region."
- "Which orders were delayed last month?"
- "Compare sales and shipment performance for the top product categories."
- "Why is this month's revenue lower than the previous month?"

A fixed rule-based chatbot would require a predefined rule or conversation flow for every expected question. This becomes difficult to maintain because business users may express the same request using different terminology, sentence structures, abbreviations, and levels of detail.

Generative AI is appropriate because it can:

- Interpret natural-language questions
- Map business language to governed enterprise data concepts
- Manage follow-up questions within a conversation
- Identify ambiguity and request clarification
- Explain structured query results in understandable language
- Summarize results without requiring the user to understand physical schemas

However, deterministic controls remain essential for authorization, query execution, metric calculation, and data retrieval.

### Role of the Data Virtualization Layer

The data virtualization layer provides a governed abstraction between the enterprise chatbot and the underlying data sources.

Instead of allowing the language model to connect independently to every source system, the chatbot interacts with approved virtualized views and data services.

The virtualization layer is expected to provide:

- A consistent business-oriented view of distributed data
- Reusable joins and transformation logic
- Abstraction from physical database schemas
- Centralized access-control enforcement
- Row-level and column-level security where configured
- Data-source and query traceability
- Standardized definitions for commonly used business entities
- Reduced need to copy data into a separate chatbot-specific repository
- Controlled access to real-time or near-real-time enterprise information

This separation ensures that the AI interprets the question and summarizes the response, while the data virtualization layer remains responsible for governed data access.

### Human-in-the-Loop Design

The chatbot will not automatically approve business decisions, financial actions, customer commitments, operational changes, or updates to source systems.

Human review will be required when:

- The user's question is ambiguous
- Multiple business definitions could apply
- The requested calculation is not mapped to an approved metric
- The generated query falls outside the validated query patterns
- The response contains sensitive or restricted information
- The answer has a low confidence score
- The query returns unusually large or unexpected results
- The user intends to use the answer for a high-impact business decision

Users will be able to:

- Review the interpreted question
- Inspect the selected data product or virtualized view
- See the filters and time period applied
- Validate the source of the answer
- Correct an interpretation
- Provide feedback on answer usefulness
- Escalate the question to a data steward or analyst

The final responsibility for interpreting and acting on the information remains with the authorized human user.

### Smallest Credible MVP

The smallest credible MVP is a web-based conversational application connected to a limited set of approved virtualized enterprise data views.

The initial prototype will support a narrow business domain such as:

- Customer information
- Orders
- Invoices
- Sales transactions
- Payment and receivables status

A user will be able to enter a natural-language question and receive:

- A concise answer
- A supporting table containing the retrieved data
- The virtualized data view used
- The filters and time period applied
- A confidence or validation status
- A clarification request when the question is incomplete
- An option to review the generated query
- A feedback control for reporting incorrect or unhelpful responses

The MVP is intended to prove the product workflow:

> **Business question -> governed data interpretation -> virtualized query -> validated result -> explainable response**

The MVP will not attempt to support every enterprise data source, every business domain, autonomous write-back, or production-scale query volumes.

### Illustrative MVP Architecture

```text
Enterprise User
      |
      v
Conversational Web Interface
      |
      v
Enterprise Authentication and User Context
      |
      v
AI Orchestration Layer
  - Intent identification
  - Business-term mapping
  - Context management
  - Clarification handling
  - Response generation
      |
      v
Governance and Validation Layer
  - Authorization checks
  - Approved-view selection
  - Query validation
  - Sensitive-data controls
  - Query and response logging
      |
      v
Data Virtualization Layer
  - Governed virtual views
  - Reusable data models
  - Business semantics
  - Access policies
  - Source abstraction
      |
      v
Enterprise Data Sources
  - ERP
  - CRM
  - Data warehouse
  - Cloud databases
  - Operational databases
  - Approved APIs
```

### Example User Journey

1. The user signs in using an enterprise identity.
2. The system retrieves the user's authorized role and data-access context.
3. The user asks: **"Show overdue customer invoices for the Western region for the current quarter."**
4. The AI identifies:
   - Business entity: customer invoices
   - Condition: overdue
   - Geographic filter: Western region
   - Time period: current quarter
5. The system maps these concepts to an approved virtualized invoice view.
6. The governance layer validates the user's access and the proposed query.
7. The validated query is executed through the data virtualization layer.
8. The chatbot summarizes the result and displays the supporting data.
9. The answer includes the data source, filters, calculation definition, and retrieval context.
10. The user reviews the result and can refine the question conversationally.

### Build vs Buy vs API View

The initial recommendation is a **hybrid build-and-integrate approach**.

#### Build

Build the product-specific components that provide enterprise differentiation:

- Business-term interpretation
- Mapping between user questions and approved virtualized views
- Query-validation workflow
- Confidence and clarification logic
- Response-grounding logic
- Source and filter presentation
- User-feedback mechanism
- Enterprise-specific governance integration

#### Buy or Reuse

Reuse existing enterprise capabilities where possible:

- Enterprise identity and access management
- Data virtualization platform
- Data catalog and business glossary
- Large language model service
- Monitoring and observability platform
- Secrets-management service
- API gateway
- Audit-logging infrastructure

#### API Usage

Use APIs for controlled interaction between:

- The conversational application and the AI model
- The AI orchestration layer and the data virtualization platform
- The application and enterprise authentication services
- The chatbot and metadata or catalog services
- The platform and monitoring systems

A fully custom language model is not required for the MVP. The product value lies primarily in governed enterprise-data grounding, semantic mapping, explainability, and workflow integration rather than in training a foundation model from scratch.

### Main Risks

#### 1. Hallucinated Answers

The language model may produce a response that is not supported by retrieved enterprise data.

**Mitigation:** Generate factual answers only from validated query results and clearly separate retrieved facts from explanatory text.

#### 2. Incorrect Query Generation

The model may apply the wrong filter, join, aggregation, metric, or time period.

**Mitigation:** Restrict execution to approved views, validate generated queries, display applied filters, and use deterministic templates for sensitive calculations.

#### 3. Ambiguous Business Terminology

Terms such as "revenue," "customer," "active order," or "late delivery" may have multiple business definitions.

**Mitigation:** Integrate approved glossary definitions and ask the user for clarification when multiple valid interpretations exist.

#### 4. Unauthorized Data Exposure

The chatbot may retrieve information that the requesting user is not permitted to access.

**Mitigation:** Enforce authorization within the data virtualization layer and pass the authenticated user context to every request.

#### 5. Prompt Injection and Malicious Input

A user may attempt to override system controls or instruct the chatbot to expose restricted information.

**Mitigation:** Separate system instructions from user content, validate tool calls, allow only approved data operations, and enforce access independently of the language model.

#### 6. Sensitive Information in Prompts or Logs

Enterprise data may be unintentionally included in model prompts, conversation history, or monitoring logs.

**Mitigation:** Minimize prompt data, mask sensitive fields, apply retention controls, and avoid logging unrestricted query results.

#### 7. Automation Bias

Users may trust a fluent chatbot response without reviewing the supporting evidence.

**Mitigation:** Display sources, filters, definitions, validation status, and limitations with every material answer.

#### 8. Data Freshness and Quality

The chatbot may provide technically correct answers from incomplete, delayed, or poor-quality source data.

**Mitigation:** Display data-freshness information where available and communicate known quality limitations.

#### 9. Performance and Cost

Complex virtualized queries or repeated AI requests may create excessive latency or infrastructure cost.

**Mitigation:** Apply query limits, caching, request monitoring, model-routing controls, and usage guardrails.

#### 10. Limited Generalization

An MVP configured around one business domain may not work reliably across other domains.

**Mitigation:** Begin with a narrow scope and introduce additional domains only after their terminology, views, and validation tests are established.

### Responsible AI and Governance Principles

The prototype will follow these product principles:

- **Grounded:** Answers must be based on retrieved and authorized enterprise data.
- **Explainable:** Users should be able to see the source, filters, and interpretation used.
- **Secure:** Access must follow existing enterprise permissions.
- **Auditable:** Questions, validated queries, data products used, and feedback should be traceable.
- **Human-controlled:** The chatbot assists users but does not make or execute high-impact business decisions.
- **Privacy-aware:** Sensitive data should be minimized in prompts and protected in logs.
- **Fail-safe:** The system should decline, clarify, or escalate when it cannot produce a sufficiently reliable answer.
- **Feedback-driven:** User corrections should inform improvements to semantic mappings, query patterns, and product design.

### Success Evidence

The MVP will be considered successful if it demonstrates the following:

1. **Natural-language understanding:** The system correctly interprets representative user questions within the selected business domain.
2. **Grounded responses:** Answers are derived from validated queries executed through approved virtualized views.
3. **Query correctness:** Generated or selected queries use the intended entities, filters, joins, calculations, and time periods.
4. **Security preservation:** Users receive only information permitted by their existing enterprise access rights.
5. **Explainability:** Each response presents enough context for the user to understand how the answer was produced.
6. **Effective ambiguity handling:** The chatbot asks for clarification instead of making unsupported assumptions when a request is incomplete.
7. **Reduced analyst dependency:** Selected recurring business questions can be answered without requiring an analyst to manually prepare every response.
8. **User trust:** Pilot users report that the supporting source, applied filters, and visible data improve their confidence in the answer.
9. **Stakeholder interest:** At least one enterprise business or data team is willing to evaluate the prototype using an approved, controlled dataset.
10. **Safe failure behavior:** The system refuses, clarifies, or escalates requests that are unauthorized, unsupported, or insufficiently grounded.

### MVP Non-Goals

The initial MVP will not:

- Replace enterprise dashboards or reporting platforms
- Provide unrestricted access to underlying databases
- Make autonomous financial or operational decisions
- Update source-system records
- Support every enterprise business domain
- Guarantee that every natural-language request can be converted into a valid query
- Train a new foundation model
- Treat the language model as the security-enforcement layer
- Present generated responses as authoritative when supporting data is unavailable

### Expected Product Outcome

The capstone will demonstrate whether a governed enterprise chatbot can make distributed enterprise information easier to access without removing the controls provided by the data virtualization layer.

The principal product hypothesis is:

> **If authorized business users can ask questions in natural language and receive responses grounded in governed virtualized data, then the organization can reduce data-discovery effort and repeated analyst dependency while preserving security, traceability, and human oversight.**
