# System Design – AI-Powered Compliance Test Case Generator

## 1. Architecture Overview
The system follows a **serverless, event-driven AWS architecture** designed for scalability, security, and compliance.

It processes healthcare requirements through document parsing, AI-based reasoning, and retrieval-augmented generation (RAG) to produce compliant and traceable test cases.

---

## 2. High-Level Architecture Components

### 2.1 Frontend
- React-based UI
- Split View Design:
  - Left Panel: Asynchronous document upload
  - Right Panel: Generated test cases
- Natural language input for requirements
- Manual compliance standard selection

---

### 2.2 Authentication & Storage
- **Amazon Cognito**
  - User authentication and authorization
- **Amazon S3**
  - Stores uploaded documents
  - Stores generated and exported test cases

---

### 2.3 Document Processing Layer
- **Amazon Textract**
  - Extracts text from PDF, Word, XML, Markdown
- **Amazon Comprehend**
  - Identifies entities, key phrases, and requirement context

---

### 2.4 AI & RAG Layer
- **Amazon Bedrock**
  - Foundation models (Claude, Llama, Amazon Titan)
  - Generates test cases from processed requirements
- **RAG (Retrieval-Augmented Generation)**
  - Vector database:
    - Amazon OpenSearch Vector Search
    - or Aurora PostgreSQL (pgvector)
  - Stores regulatory standards:
    - FDA
    - IEC
    - ISO
    - GDPR

---

### 2.5 Workflow Orchestration
- **AWS Step Functions**
  - Orchestrates:
    - Upload
    - Parsing
    - Retrieval
    - Test case generation
    - Review
    - Export

---

### 2.6 Human-in-the-Loop Validation
- **Amazon API Gateway + AWS Lambda**
  - Review and edit test cases
  - Capture user feedback
- **Amazon DynamoDB**
  - Store test case versions
  - Store review metadata

---

### 2.7 Compliance & Traceability
- **AWS Audit Manager**
  - Compliance tracking
- **AWS CloudTrail**
  - Full audit logs
- **Amazon Athena**
  - Query traceability data
  - Compliance coverage analysis

---

### 2.8 Eventing & Notifications
- **Amazon EventBridge**
  - Event-driven workflow triggers
- **Amazon SNS / SQS**
  - Notify test case completion
  - Enable async processing

---

### 2.9 Export & Toolchain Integration
- **AWS Lambda**
  - Format conversion (JSON, CSV, XML, XLSX, PDF)
  - Integration adapters
- **AWS Secrets Manager**
  - Secure storage of API tokens
- **External Tools**
  - Jira
  - Polarion
  - Azure DevOps

---

## 3. Process Flow

1. User logs in via Amazon Cognito
2. User uploads documents and enters natural language requirements
3. Documents stored in Amazon S3
4. Textract and Comprehend extract and analyze content
5. RAG retrieves relevant regulatory context
6. Amazon Bedrock generates compliant test cases
7. User reviews and edits test cases
8. Approved test cases stored in DynamoDB / S3
9. Notifications sent via SNS
10. Test cases exported or integrated with ALM tools

---

## 4. Design Principles
- Serverless-first architecture
- Human-in-the-loop AI
- Compliance by design
- Event-driven scalability
- Audit-ready traceability

---

## 5. Future Enhancements
- Risk-based test prioritization
- Automated compliance gap detection
- CI/CD pipeline integration
- Fine-tuned healthcare-specific LLMs
