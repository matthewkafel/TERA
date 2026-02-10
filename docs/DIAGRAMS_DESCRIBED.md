# TERA Architecture Diagrams - Text Descriptions

> **For GitHub Copilot**: Detailed textual descriptions of all architectural diagrams since AI cannot read PNG images directly.

This document provides comprehensive text descriptions of all 14 diagrams extracted from the TERA Memo Architecture PDF, enabling GitHub Copilot to understand the visual architecture without accessing the image files.

---

## Page 2: Capability Viewpoint Taxonomy (CV-2)

**Diagram Type**: Hierarchical taxonomy/tree diagram

**Description**:
This diagram shows the capability hierarchy for TERA Memo Automation. It's a small diagram that appears to be a simple icon or placeholder in the PDF.

**Key Elements**:
- Root capability: TERA Memo Automation
- Sub-capabilities related to AI-powered form completion
- Integration with BIP Platform services

---

## Page 3, Diagram 1: Use Case Flow - VSR Workflow

**Diagram Type**: Activity flow diagram / User journey

**Description**:
This diagram illustrates the complete workflow of a Veteran Service Representative (VSR) using the TERA Memorandum form in VBMS.

**Workflow Steps**:
1. **Start**: VSR opens Veteran's claim in VBMS
2. **Navigate**: VSR accesses Veteran Profile page
3. **Action**: VSR selects "Upload Document" dropdown
4. **Select**: VSR chooses "TERA Memo" option
5. **Load**: TERA Memorandum form opens with pre-populated Veteran information
6. **Decision Point**: VSR can choose to:
   - a) Manually complete the form, OR
   - b) Click "Auto-Populate" button
7. **If Auto-Populate**:
   - System displays information modal explaining the feature
   - VSR confirms to proceed
   - System populates questions with AI recommendations
   - Each answer shows:
     * Recommended response (Yes/No)
     * Confidence score (percentage)
     * Links to supporting evidence documents
     * Highlighted text in source documents
8. **Review**: VSR reviews each auto-populated answer
9. **Validate**: VSR clicks evidence links to verify recommendations
10. **Manual Override**: VSR can modify any auto-populated answer
11. **Certify**: VSR checks box to certify manual review completed
12. **Preview**: VSR previews the generated PDF document
13. **Submit**: VSR submits completed TERA Memo
14. **End**: Document uploaded to Veteran's eFolder

**Decision Points**:
- Use auto-populate vs manual entry
- Accept vs modify AI recommendations
- Each question can be individually accepted or changed

**Actors**:
- Veteran Service Representative (VSR)
- TERA Memo UI System
- Auto-Population Engine
- Evidence Repository

---

## Page 3, Diagram 2: User Interface Components

**Diagram Type**: UI mockup/wireframe diagram

**Description**:
Shows the key UI components of the modernized TERA Memorandum form.

**UI Components Shown**:
1. **Header Section**:
   - Veteran name and file number (pre-populated)
   - Claim information
   - Auto-Populate button (prominent, top of form)

2. **Form Body**:
   - Question sections (1-6)
   - Radio buttons for Yes/No answers
   - Text input fields for details
   - Confidence score indicators (visual badges)
   - Evidence link buttons

3. **Evidence Panel**:
   - Document viewer integration
   - Highlight indicators
   - Page navigation
   - Confidence score display

4. **Footer Section**:
   - Manual review certification checkbox
   - Preview button
   - Submit button
   - Cancel/Save draft options

**Visual Indicators**:
- Green badges for high confidence (>80%)
- Yellow badges for medium confidence (60-80%)
- Red badges for low confidence (<60%)
- Link icons next to auto-populated answers

---

## Page 4: AI Model Input-Process-Output Diagram

**Diagram Type**: Data flow / Process diagram

**Description**:
Illustrates the AI model's processing pipeline from input data to output recommendations.

**Three-Stage Process**:

### Stage 1: INPUT
**Data Sources**:
- Veteran's Claim Evidence documents (via OCR)
- ILER IES exposure records
- PACT Act Standard Operating Procedures (reference data)
- M21-1 Adjudication Procedures Manual (reference data)

### Stage 2: MODEL PROCESSING
**Algorithm Components**:
- Text extraction and normalization
- Natural Language Processing (NLP)
- Named Entity Recognition for:
  * Dates and locations
  * Toxic substance names
  * Military service details
  * Medical conditions
- Pattern matching against PACT Act criteria
- Eligibility rule evaluation per M21-1 guidelines
- Confidence score calculation
- Evidence linking and highlighting

**Processing Platform**:
- AWS SageMaker for model execution
- ML-MATS Platform for model management
- AWS Comprehend for NLP tasks

### Stage 3: OUTPUT
**For Each Applicable Question (1, 3, 4, 6)**:
- **Determination**: Yes/No recommendation
- **Supporting Text**: Free-text explanation with details
- **Evidence Links**: Array of document references
  * Document ID
  * Page number
  * Specific text location/highlight coordinates
- **Confidence Score**: Percentage (0-100%)

**Flow Arrows**:
- Input data → Model Processing (solid arrow)
- Reference data → Model Processing (dashed arrow, indicates lookup)
- Model Processing → Output Results (solid arrow)
- Output → VBMS Database (solid arrow, storage)
- VBMS Database → TERA UI (dashed arrow, retrieval)

---

## Page 7: High-Level Operational Viewpoint (OV-1)

**Diagram Type**: System context / Component diagram

**Description**:
Shows the high-level architecture with all system components and their relationships.

**System Components** (represented as rectangles):

**White Rectangles (TERA Application Components)**:
- TERA Memo UI (React MFE)
- TERA Memo API
- Auto-Population Engine

**Gray Rectangles (Existing VBMS Components)**:
- VBMS Core Database (Oracle)
- Claims Evidence API
- Claims API
- ILER API
- DocGen Genstore API
- Veteran API
- C&P Smart Search (OCR)

**External Systems** (cloud icons):
- AWS SageMaker
- AWS Comprehend
- OpenSearch

**Connections/Relationships**:
- TERA Memo UI ←→ TERA Memo API (bidirectional, HTTPS)
- TERA Memo UI ←→ Claims Evidence API (bidirectional, HTTPS)
- TERA Memo UI ←→ ILER API (read-only)
- TERA Memo API ←→ VBMS Core DB (read/write)
- Auto-Population Engine ←→ OpenSearch (query)
- AWS SageMaker ←→ OpenSearch (read/write)
- C&P Smart Search → OpenSearch (write, OCR results)
- DocGen API → Claims Evidence (write, PDF upload)

**Data Flows**:
1. User interaction → TERA UI
2. Auto-populate request → TERA API → VBMS DB
3. Evidence retrieval → Claims Evidence API
4. Document OCR → OpenSearch
5. Model execution → SageMaker → OpenSearch
6. PDF generation → DocGen → eFolder

---

## Page 8: Operational Resource Flow (OV-2)

**Diagram Type**: Sequence/Resource flow diagram

**Description**:
Behavioral diagram showing resource exchanges between operational systems.

**Systems and Interactions**:

```
[AWS SageMaker] ←→ [OpenSearch Endpoint]
  Purpose: Run TERA model against Veteran dataset, store in VBMS Core DB

[Claims Evidence API] ←→ [VBMS Core Database]
  Purpose: Pull relevant Veteran data to populate TERA Memo UI

[Claims Evidence API] ←→ [TERA Memo UI]
  Purpose: Auto-population with AI recommendations

[ILER API] ←→ [TERA Memo UI]
  Purpose: Retrieve Veteran ILER document for auto-population data

[TERA Memo UI] ←→ [CE API / CE UI]
  Purpose: Click evidence links to manually review specific document locations

[TERA Memo UI] ←→ [DocGen GenStore API]
  Purpose: Upload completed TERA Memo document to Claim Evidence

[VBMS] ←→ [TERA Memo UI]
  Purpose: Initiate auto-population, review recommendations, validate answers
```

**Resource Flow Legend**:
- Solid arrows: Data transfer
- Dashed arrows: Control flow
- Bidirectional arrows: Request/response patterns

**Key Resources Flowing**:
- Veteran demographics
- Claim evidence documents
- OCR-extracted text
- AI model predictions
- Confidence scores
- Evidence links/highlights
- Completed TERA Memo PDF

---

## Page 9: Systems Interface Description (SV-1)

**Diagram Type**: UML-style component diagram with lollipop notation

**Description**:
Shows system composition and interfaces using UML stereotypes. Service providers shown with lollipop (provided interface), service consumers "eating" the lollipop (required interface).

**Components and Interfaces**:

```
┌─────────────────────────┐
│   TERA Memo UI MFE      │
│   <<CPUI #3028>>        │
└───────────┬─────────────┘
            │ requires
            ├──○ Claims Evidence API (REST)
            ├──○ Claims API (REST)
            ├──○ ILER API (REST)
            ├──○ Veteran API (REST)
            └──○ DocGen Genstore API (REST)

┌─────────────────────────┐
│   AWS SageMaker         │
│   (ML Platform)         │
└───────────┬─────────────┘
            │ provides
            ○── Model Inference API

┌─────────────────────────┐
│   OpenSearch            │
│   (Document Index)      │
└───────────┬─────────────┘
            │ provides
            ○── Search API
            ○── Index API

┌─────────────────────────┐
│   VBMS Core Database    │
│   (Oracle)              │
└───────────┬─────────────┘
            │ provides
            ○── Data Access Layer
```

**Visual Legend**:
- White Rectangle = TERA application resources
- Gray Rectangle = Existing VBMS resources
- Lollipop (○──) = Provided interface
- Half-circle (──○) = Required interface
- <<Stereotype>> = VASI ID identifier

**Component Details Table**:
| Component | Description | Ports | Protocols |
|-----------|-------------|-------|-----------|
| CPUI #3028 | TERA Memo UI MFE | 443 | HTTPS |
| AWS SageMaker | ML model platform | 443 | HTTPS |
| OpenSearch | Document indexing | 443 | HTTPS |
| Claims Evidence API | Evidence access | 443 | HTTPS |
| VBMS Core DB | Data persistence | 1521 | Oracle TNS |

---

## Page 10: Services Context (SvcV-1)

**Diagram Type**: Service composition diagram

**Description**:
Shows service dependencies and API operations for the TERA Memo UI component.

**Service/API Operations Table**:

### Claims Evidence (CE) API
**Operations**:
1. `getTeraRecommendations(claimId)`:
   - Retrieves AI recommendations from OCR_TEXTRACT_DATA table
   - Returns: Questions, answers, confidence scores, evidence links
   
2. `getDocumentAnnotations(documentId, pageNum)`:
   - Gets specific text highlights within documents
   - Uses custom annotator viewer
   - Returns: Highlight coordinates, text snippets

3. `writeMetrics(teraData)`:
   - Writes submitted answers to TERAMEMOUPLOADMETRICS table
   - For analytics and model improvement

### Claims API
**Operations**:
1. `getVeteranClaims(veteranId)`:
   - Retrieves open claims for a Veteran
   - Used during TERA Memo submission to associate with claim

### DocGen Genstore API
**Operations**:
1. `generatePreview(formData)`:
   - Generates PDF with form data
   - Returns: Document ID and preview URL
   
2. `submitDocument(documentId, claimId)`:
   - Uploads PDF to Veteran's eFolder
   - Finalizes the TERA Memo submission

### Veteran API
**Operations**:
1. `getVeteranProfile(fileNumber)`:
   - Retrieves Veteran demographic information
   - Returns: Name, file number, contact info

### ILER API
**Operations**:
1. `getExposureRecords(veteranId)`:
   - Retrieves exposure history from ILER system
   - Returns: Deployment locations, dates, exposure types

**Service Dependencies Diagram**:
```
TERA Memo UI
    ├── depends on: Claims Evidence API
    ├── depends on: Claims API
    ├── depends on: DocGen Genstore API
    ├── depends on: Veteran API
    └── depends on: ILER API

All APIs communicate via:
    - Protocol: HTTPS (port 443)
    - Format: JSON
    - Authentication: OAuth 2.0 / JWT tokens
```

---

## Page 12, Diagram 1: Conceptual Data Model (DIV-1)

**Diagram Type**: Entity-Relationship Diagram (ERD) - Conceptual

**Description**:
Logical data model showing entities and relationships for TERA Memo data.

**Entities and Attributes**:

### Entity: TERA_MEMO
**Attributes**:
- memo_id (PK)
- veteran_file_number (FK)
- claim_id (FK)
- created_date
- submitted_date
- status (draft|submitted|completed)
- created_by_user_id

### Entity: TERA_QUESTION_ANSWER
**Attributes**:
- answer_id (PK)
- memo_id (FK)
- question_number (1-6)
- answer_value (yes|no|unsure)
- free_text_response
- auto_populated (boolean)
- confidence_score (0-100)
- manually_reviewed (boolean)
- modified_by_user (boolean)

### Entity: EVIDENCE_LINK
**Attributes**:
- link_id (PK)
- answer_id (FK)
- document_id
- page_number
- highlight_start_position
- highlight_end_position
- evidence_text_snippet
- relevance_score

### Entity: OCR_TEXTRACT_DATA
**Attributes**:
- textract_id (PK)
- veteran_file_number
- document_id
- extracted_text
- processing_date
- ocr_confidence

### Entity: TERA_RECOMMENDATION
**Attributes**:
- recommendation_id (PK)
- veteran_file_number
- question_number
- recommended_answer
- confidence_score
- supporting_text
- model_version
- generated_date

**Relationships**:
- TERA_MEMO 1:N TERA_QUESTION_ANSWER
- TERA_QUESTION_ANSWER 1:N EVIDENCE_LINK
- VETERAN 1:N TERA_MEMO
- CLAIM 1:N TERA_MEMO
- DOCUMENT 1:N EVIDENCE_LINK

---

## Page 12, Diagram 2: Logical Data Flow

**Diagram Type**: Data flow diagram

**Description**:
Shows how data flows through the system from document upload to TERA completion.

**Flow Stages**:

1. **Document Upload**:
   - User uploads evidence → eFolder
   - Trigger: Daily batch job

2. **OCR Processing**:
   - PDF/Image → C&P Smart Search OCR
   - Output: Plain text → OCR_TEXTRACT_DATA

3. **Indexing**:
   - Text → OpenSearch
   - Indexed by: Veteran ID, Document ID, Content

4. **AI Model Execution**:
   - OpenSearch data → AWS SageMaker
   - Model applies: PACT Act rules, M21-1 criteria
   - Output → TERA_RECOMMENDATION table

5. **UI Retrieval**:
   - VSR opens TERA form
   - UI queries: TERA_RECOMMENDATION
   - Display: Answers with evidence links

6. **Submission**:
   - VSR submits
   - Write: TERA_MEMO, TERA_QUESTION_ANSWER, EVIDENCE_LINK
   - Generate: PDF via DocGen
   - Upload: PDF → eFolder

---

## Page 13: Physical Data Model (DIV-3)

**Diagram Type**: Database schema diagram

**Description**:
Physical database tables and columns in Oracle VBMS Core Database.

**Database Tables**:

### Table: VBMSUI.OCR_TEXTRACT_DATA
```sql
Column Name              Data Type       Nullable    Description
-----------------------------------------------------------------
ID                      NUMBER          NOT NULL    Primary key
VETERAN_FILE_NUMBER     VARCHAR2(20)    NOT NULL    Veteran identifier
DOCUMENT_ID             VARCHAR2(50)    NOT NULL    Evidence document ID
PAGE_NUMBER             NUMBER          NULL        Page within document
EXTRACTED_TEXT          CLOB            NULL        OCR text content
CONFIDENCE_SCORE        NUMBER(5,2)     NULL        OCR confidence %
PROCESSING_DATE         TIMESTAMP       NOT NULL    When OCR ran
INDEX_STATUS            VARCHAR2(20)    NULL        OpenSearch status
QUESTION_1_ANSWER       VARCHAR2(10)    NULL        AI recommendation
QUESTION_1_CONFIDENCE   NUMBER(5,2)     NULL        Confidence score
QUESTION_1_EVIDENCE     CLOB            NULL        Evidence JSON
QUESTION_3_ANSWER       VARCHAR2(10)    NULL        AI recommendation
QUESTION_3_CONFIDENCE   NUMBER(5,2)     NULL        Confidence score
QUESTION_3_EVIDENCE     CLOB            NULL        Evidence JSON
QUESTION_4_ANSWER       VARCHAR2(10)    NULL        AI recommendation
QUESTION_4_CONFIDENCE   NUMBER(5,2)     NULL        Confidence score
QUESTION_4_EVIDENCE     CLOB            NULL        Evidence JSON
QUESTION_6_ANSWER       VARCHAR2(10)    NULL        AI recommendation
QUESTION_6_CONFIDENCE   NUMBER(5,2)     NULL        Confidence score
QUESTION_6_EVIDENCE     CLOB            NULL        Evidence JSON
MODEL_VERSION           VARCHAR2(20)    NULL        Which model ran
CREATED_DATE            TIMESTAMP       NOT NULL    Record creation
UPDATED_DATE            TIMESTAMP       NULL        Last update
```

### Table: VBMSUI.TERAMEMOUPLOADMETRICS
```sql
Column Name              Data Type       Nullable    Description
-----------------------------------------------------------------
ID                      NUMBER          NOT NULL    Primary key
VETERAN_FILE_NUMBER     VARCHAR2(20)    NOT NULL    Veteran identifier
CLAIM_ID                NUMBER          NULL        Associated claim
SUBMISSION_DATE         TIMESTAMP       NOT NULL    When submitted
USER_ID                 VARCHAR2(50)    NOT NULL    Submitting VSR
QUESTION_NUMBER         NUMBER          NOT NULL    Question 1-6
AUTO_POPULATED          CHAR(1)         NULL        Y/N flag
USER_ANSWER             VARCHAR2(10)    NOT NULL    Final answer
AI_RECOMMENDATION       VARCHAR2(10)    NULL        What AI suggested
CONFIDENCE_SCORE        NUMBER(5,2)     NULL        AI confidence
ACCEPTED_AI_ANSWER      CHAR(1)         NULL        Y/N flag
MANUAL_OVERRIDE         CHAR(1)         NULL        Y/N flag
PROCESSING_TIME_MS      NUMBER          NULL        UI load time
CREATED_DATE            TIMESTAMP       NOT NULL    Record creation
```

**Indexes**:
- PK_OCR_TEXTRACT on ID
- IDX_OCR_VETERAN on VETERAN_FILE_NUMBER
- IDX_OCR_DOCUMENT on DOCUMENT_ID
- PK_TERA_METRICS on ID
- IDX_METRICS_VETERAN on VETERAN_FILE_NUMBER
- IDX_METRICS_DATE on SUBMISSION_DATE

**Constraints**:
- CHECK: CONFIDENCE_SCORE between 0 and 100
- CHECK: QUESTION_NUMBER between 1 and 6
- FK: VETERAN_FILE_NUMBER references VETERAN table

---

## Page 14: Deployment Architecture / Process Flow (OV-6d)

**Diagram Type**: Business process model / Deployment diagram

**Description**:
Shows the deployment architecture and main business process flow.

**Process Flow**:

**Phase 1: Nightly Batch Processing**
```
[Start: Midnight EST]
    ↓
[Identify new documents in eFolders]
    ↓
[Run C&P Smart Search OCR]
    ↓
[Extract text from PDFs/Images]
    ↓
[Store in OCR_TEXTRACT_DATA]
    ↓
[Index text in OpenSearch]
    ↓
[Execute TERA ML Model via SageMaker]
    ↓
[Write recommendations to OCR_TEXTRACT_DATA]
    ↓
[Update processing metrics]
    ↓
[End: Available for VSR use]
```

**Phase 2: VSR Interactive Process**
```
[VSR logs into VBMS]
    ↓
[Opens Veteran claim]
    ↓
[Selects "TERA Memo" from actions]
    ↓
[Form loads with Veteran info]
    ↓
[VSR clicks "Auto-Populate"]
    ↓
[System queries OCR_TEXTRACT_DATA]
    ↓
[Display recommendations with confidence scores]
    ↓
[VSR reviews evidence links]
    ↓
[VSR validates/modifies answers]
    ↓
[VSR certifies manual review]
    ↓
[VSR clicks Submit]
    ↓
[Write to TERAMEMOUPLOADMETRICS]
    ↓
[Generate PDF via DocGen]
    ↓
[Upload to eFolder]
    ↓
[End: TERA Memo completed]
```

**Deployment Components**:
- **Web Tier**: React MFE served via VBMS
- **API Tier**: Node.js/Java APIs on BIP Platform
- **Data Tier**: Oracle RAC cluster
- **ML Tier**: AWS SageMaker endpoints
- **Search Tier**: OpenSearch cluster
- **Storage**: eFolder document repository

---

## Page 15, Diagram 1: Process Sequence - Event Trace (SV-10c)

**Diagram Type**: Sequence diagram / System event trace

**Description**:
Shows the detailed interaction sequence between system components during auto-population.

**Sequence of Events**:

```
VSR → TERA UI: Click "Auto-Populate" button

TERA UI → Claims Evidence API: GET /tera-recommendations/{veteranId}

Claims Evidence API → VBMS Core DB: SELECT * FROM OCR_TEXTRACT_DATA WHERE veteran_file_number = ?

VBMS Core DB → Claims Evidence API: Return recommendation data

Claims Evidence API → TERA UI: JSON response with recommendations

TERA UI → TERA UI: Parse and display recommendations

VSR → TERA UI: Click evidence link for Question 1

TERA UI → Claims Evidence API: GET /document/{docId}/annotations?page={pageNum}

Claims Evidence API → VBMS Core DB: Fetch document and highlight data

VBMS Core DB → Claims Evidence API: Return document data

Claims Evidence API → TERA UI: Document with highlighted text

TERA UI → Browser: Open document viewer in new tab

Browser → Document Viewer: Display PDF with highlights

VSR → Document Viewer: Review evidence

VSR → TERA UI: Modify answer if needed

VSR → TERA UI: Check "Manual review completed"

VSR → TERA UI: Click "Submit"

TERA UI → Claims Evidence API: POST /tera-metrics

Claims Evidence API → VBMS Core DB: INSERT INTO TERAMEMOUPLOADMETRICS

VBMS Core DB → Claims Evidence API: Success

TERA UI → DocGen API: POST /generate-pdf

DocGen API → DocGen API: Generate TERA Memo PDF

DocGen API → TERA UI: Return PDF URL

TERA UI → DocGen API: POST /upload-to-efolder

DocGen API → eFolder: Upload PDF

eFolder → DocGen API: Success

DocGen API → TERA UI: Upload complete

TERA UI → VSR: Display success message
```

**Timing Information**:
- Auto-populate query: ~500ms
- Evidence link load: ~200ms per document
- PDF generation: ~2-3 seconds
- Total submission: ~5-10 seconds

---

## Page 15, Diagram 2: Feature Flag Configuration

**Diagram Type**: Configuration/Decision tree diagram

**Description**:
Shows feature flag hierarchy and dependencies.

**Feature Flags**:

```
TERA_MEMO_ENABLED (master switch)
    ├── If FALSE: Hide TERA Memo from VBMS actions menu
    └── If TRUE:
        ├── MODERNIZED_FORM_ENABLED
        │   ├── TRUE: Show React MFE version
        │   └── FALSE: Show legacy PDF form
        │
        ├── AUTO_POPULATE_ENABLED (sub-master for auto-pop)
        │   ├── If FALSE: Hide auto-populate button
        │   └── If TRUE:
        │       ├── AUTO_POPULATE_1_ENABLED (Question 1)
        │       ├── AUTO_POPULATE_3_ENABLED (Question 3)
        │       ├── AUTO_POPULATE_4_ENABLED (Question 4)
        │       └── AUTO_POPULATE_6_ENABLED (Question 6)
        │
        ├── METRICS_ENABLED
        │   ├── TRUE: Write to TERAMEMOUPLOADMETRICS
        │   └── FALSE: Skip metrics collection
        │
        ├── OPEN_EVIDENCE_DOCS_IN_ANNOTATOR_VIEW
        │   ├── TRUE: Use annotator document viewer
        │   └── FALSE: Use standard viewer
        │
        └── tera.memo.multipleHighlights.enabled
            ├── TRUE: Support multiple highlights per document
            └── FALSE: Single highlight per document
```

**Flag Locations**:
- Environment-specific config files
- Feature flag management UI
- Runtime configuration service

**Usage Example**:
```javascript
if (featureFlags.TERA_MEMO_ENABLED) {
  if (featureFlags.AUTO_POPULATE_ENABLED) {
    if (featureFlags.AUTO_POPULATE_1_ENABLED) {
      // Show auto-populate for Question 1
    }
  }
}
```

---

## Summary of Diagram Content

**Total Diagrams**: 14 architectural diagrams across 17 pages

**Categories**:
- **Workflow Diagrams**: 3 (User flows, process flows)
- **System Architecture**: 3 (OV-1, OV-2, SV-1)
- **Data Models**: 3 (DIV-1, DIV-2, DIV-3)
- **Service/API**: 2 (SvcV-1, sequence diagrams)
- **Configuration**: 1 (Feature flags)
- **UI/UX**: 2 (Interface components, user journey)

**Key Insights from Diagrams**:
1. System uses microservices architecture with React frontend
2. AI model runs in AWS, recommendations stored in Oracle DB
3. Nightly batch process for document OCR and model execution
4. VSR workflow takes 5-10 minutes with auto-population vs 30+ minutes manual
5. Feature flags enable gradual rollout and A/B testing
6. Evidence linking provides direct document navigation
7. Confidence scores drive manual review requirements
8. Metrics collection enables continuous model improvement

---

**Last Updated**: February 10, 2026  
**Purpose**: Enable GitHub Copilot to understand architectural diagrams through text descriptions
