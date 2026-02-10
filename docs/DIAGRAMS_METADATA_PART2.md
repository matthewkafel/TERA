# TERA Architecture Diagrams - Structured Metadata (Part 2)

> Continuation of diagram metadata - Diagrams 8.1 through 15.2

---

## Diagram 8.1: Operational Resource Flow (OV-2)

**Type**: Resource Flow / Behavioral Diagram  
**Source**: Page 8 of PDF  
**Image**: `docs/images/page_8_diagram_1.png`

### Metadata

```yaml
diagram_type: resource_flow
diagram_name: "Operational Resource Flow (OV-2)"
page: 8
dimensions:
  width: 1020
  height: 380

description: "Shows resource exchanges between operational performers - what data flows where between systems"

resource_flows:
  - flow_id: 1
    from_system: "AWS SageMaker"
    from_vasi: "N/A"
    to_system: "OpenSearch Endpoint"
    to_vasi: "N/A"
    resource_exchanged: "Model execution results"
    interaction: "Run TERA model against Veteran dataset, store in VBMS Core DB"
    arrow_type: "bidirectional"
    
  - flow_id: 2
    from_system: "Claims Evidence API"
    from_vasi: "TBD"
    to_system: "VBMS Core Database"
    to_vasi: "Core"
    resource_exchanged: "Veteran data queries"
    interaction: "Pull relevant data to populate TERA Memo UI"
    arrow_type: "bidirectional"
    
  - flow_id: 3
    from_system: "Claims Evidence API"
    from_vasi: "TBD"
    to_system: "TERA Memo UI"
    to_vasi: "3028"
    resource_exchanged: "Auto-population recommendations"
    interaction: "Send AI recommendations with confidence scores and evidence links"
    arrow_type: "bidirectional"
    
  - flow_id: 4
    from_system: "ILER API"
    from_vasi: "TBD"
    to_system: "TERA Memo UI"
    to_vasi: "3028"
    resource_exchanged: "Exposure records"
    interaction: "Retrieve Veteran ILER document for auto-population"
    arrow_type: "request_response"
    
  - flow_id: 5
    from_system: "TERA Memo UI"
    from_vasi: "3028"
    to_system: "CE API / CE UI"
    to_vasi: "TBD"
    resource_exchanged: "Evidence link requests"
    interaction: "Click evidence link to open document viewer with highlights"
    arrow_type: "request_response"
    
  - flow_id: 6
    from_system: "TERA Memo UI"
    from_vasi: "3028"
    to_system: "DocGen GenStore API"
    to_vasi: "TBD"
    resource_exchanged: "Completed TERA Memo data"
    interaction: "Upload completed TERA Memorandum PDF to Claim Evidence"
    arrow_type: "request_response"
    
  - flow_id: 7
    from_system: "VBMS (User)"
    from_vasi: "N/A"
    to_system: "TERA Memo UI"
    to_vasi: "3028"
    resource_exchanged: "User interactions"
    interactions:
      - "Initiate auto-population"
      - "Review recommendations"
      - "Validate answers"
    arrow_type: "user_interaction"

resources_detailed:
  veteran_data:
    includes:
      - "Veteran name"
      - "File number"
      - "Claim ID"
      - "Demographics"
    flows_from: "VBMS Core DB"
    flows_to: "TERA Memo UI"
    via: "Claims Evidence API"
    
  ai_recommendations:
    includes:
      - "Question answers (Yes/No)"
      - "Confidence scores (%)"
      - "Supporting text"
      - "Evidence links array"
    flows_from: "OCR_TEXTRACT_DATA table"
    flows_to: "TERA Memo UI"
    via: "Claims Evidence API"
    
  exposure_records:
    includes:
      - "Deployment locations"
      - "Service dates"
      - "Exposure types"
    flows_from: "ILER System"
    flows_to: "TERA Memo UI"
    via: "ILER API"
    
  evidence_documents:
    includes:
      - "PDF documents"
      - "Highlighted text coordinates"
      - "Page numbers"
    flows_from: "eFolder"
    flows_to: "Document Viewer"
    via: "Claims Evidence API"
    
  completed_memo:
    includes:
      - "All question answers"
      - "VSR certifications"
      - "Timestamps"
    flows_from: "TERA Memo UI"
    flows_to: "eFolder"
    via: "DocGen API"
    
  metrics_data:
    includes:
      - "Auto-populate usage"
      - "Answer selections"
      - "Manual overrides"
    flows_from: "TERA Memo UI"
    flows_to: "TERAMEMOUPLOADMETRICS table"
    via: "Claims Evidence API"
```

### JSON Representation

```json
{
  "diagram_id": "page_8_diagram_1",
  "type": "resource_flow",
  "title": "Operational Resource Flow (OV-2)",
  "flows": [
    {
      "id": 1,
      "from": "AWS SageMaker",
      "to": "OpenSearch",
      "resource": "ML model results",
      "direction": "bidirectional"
    },
    {
      "id": 2,
      "from": "Claims Evidence API",
      "to": "VBMS Core DB",
      "resource": "Veteran data queries",
      "direction": "bidirectional"
    },
    {
      "id": 3,
      "from": "Claims Evidence API",
      "to": "TERA Memo UI",
      "resource": "AI recommendations",
      "direction": "bidirectional"
    },
    {
      "id": 4,
      "from": "ILER API",
      "to": "TERA Memo UI",
      "resource": "Exposure records",
      "direction": "request_response"
    },
    {
      "id": 5,
      "from": "TERA Memo UI",
      "to": "CE UI",
      "resource": "Evidence link requests",
      "direction": "request_response"
    },
    {
      "id": 6,
      "from": "TERA Memo UI",
      "to": "DocGen API",
      "resource": "Completed PDF",
      "direction": "request_response"
    }
  ]
}
```

---

## Diagram 9.1: Systems Interface (SV-1)

**Type**: UML Component Diagram with Lollipop Notation  
**Source**: Page 9 of PDF  
**Image**: `docs/images/page_9_diagram_1.png`

### Metadata

```yaml
diagram_type: uml_component_diagram
diagram_name: "Systems Interface Description (SV-1)"
page: 9

notation:
  lollipop_provided: "○── (Service provider has API shown as lollipop)"
  socket_required: "──○ (Service consumer 'eating' the lollipop)"
  white_rectangle: "Internal VBMS resource"
  gray_rectangle: "External VBMS resource"
  stereotype: "<<VASI ID>>"

components:
  - name: "TERA Memo UI MFE"
    vasi_id: "3028"
    stereotype: "<<CPUI #3028>>"
    type: "Micro Frontend"
    tech_stack: "React"
    color: "white"
    port: 443
    protocol: "HTTPS"
    
    required_interfaces:
      - interface: "Claims Evidence API"
        type: "REST"
        operations:
          - "GET /tera-recommendations"
          - "GET /documents"
          - "GET /annotations"
          - "POST /metrics"
        consumes: true
        
      - interface: "Claims API"
        type: "REST"
        operations:
          - "GET /claims/:veteranId"
        consumes: true
        
      - interface: "ILER API"
        type: "REST"
        operations:
          - "GET /exposure-records/:veteranId"
        consumes: true
        
      - interface: "Veteran API"
        type: "REST"
        operations:
          - "GET /veteran/:fileNumber"
        consumes: true
        
      - interface: "DocGen Genstore API"
        type: "REST"
        operations:
          - "POST /generate-pdf"
          - "POST /upload"
        consumes: true
    
  - name: "Claims Evidence API"
    vasi_id: "TBD"
    stereotype: "<<CE API>>"
    type: "REST Service"
    color: "gray"
    port: 443
    protocol: "HTTPS"
    
    provided_interfaces:
      - interface: "Evidence Service"
        type: "REST"
        operations:
          - "GET /tera-recommendations"
          - "GET /documents/:id"
          - "GET /annotations/:docId/:page"
          - "POST /metrics"
        provides: true
        
    required_interfaces:
      - interface: "VBMS Core DB"
        type: "JDBC"
        tables_accessed:
          - "OCR_TEXTRACT_DATA"
          - "TERAMEMOUPLOADMETRICS"
          - "DOCUMENTS"
        consumes: true
  
  - name: "AWS SageMaker"
    vasi_id: "N/A"
    stereotype: "<<ML Platform>>"
    type: "ML Service"
    color: "cloud"
    port: 443
    protocol: "HTTPS"
    
    provided_interfaces:
      - interface: "Model Inference API"
        type: "REST"
        operations:
          - "POST /invoke-endpoint"
        provides: true
        
  - name: "OpenSearch"
    vasi_id: "N/A"
    stereotype: "<<Search Engine>>"
    type: "Search Service"
    color: "cloud"
    port: 443
    protocol: "HTTPS"
    
    provided_interfaces:
      - interface: "Search API"
        type: "REST"
        operations:
          - "POST /_search"
          - "POST /_bulk"
        provides: true
      
      - interface: "Index API"
        type: "REST"
        operations:
          - "PUT /{index}/_doc/{id}"
        provides: true
  
  - name: "VBMS Core Database"
    vasi_id: "Core"
    stereotype: "<<Oracle RAC>>"
    type: "Database"
    color: "gray"
    port: 1521
    protocol: "Oracle TNS"
    
    provided_interfaces:
      - interface: "Data Access Layer"
        type: "JDBC"
        schemas:
          - "VBMSUI"
        tables:
          - "OCR_TEXTRACT_DATA"
          - "TERAMEMOUPLOADMETRICS"
          - "VETERAN"
          - "CLAIM"
        provides: true

component_dependencies:
  tera_memo_ui_dependencies:
    - "Claims Evidence API (required)"
    - "Claims API (required)"
    - "ILER API (required)"
    - "Veteran API (required)"
    - "DocGen Genstore API (required)"
    
  claims_evidence_api_dependencies:
    - "VBMS Core DB (required)"
    
  aws_sagemaker_dependencies:
    - "OpenSearch (required)"
    - "VBMS Core DB (via Claims Evidence API)"

interface_contracts:
  - api: "Claims Evidence API"
    endpoint: "/tera-recommendations/:veteranId"
    method: "GET"
    request:
      path_params:
        veteran_id: "string"
      query_params:
        include_evidence: "boolean (optional)"
    response:
      status: 200
      body:
        type: "application/json"
        schema:
          questions:
            - question_id: "integer"
              recommended_answer: "string"
              confidence_score: "float"
              supporting_text: "string"
              evidence_links:
                - document_id: "string"
                  page_number: "integer"
                  highlight_coordinates: "object"
```

### JSON Representation

```json
{
  "diagram_id": "page_9_diagram_1",
  "type": "component_diagram",
  "title": "Systems Interface Description (SV-1)",
  "notation": "UML lollipop",
  "components": [
    {
      "name": "TERA Memo UI",
      "vasi_id": "3028",
      "type": "frontend",
      "requires": [
        "Claims Evidence API",
        "Claims API",
        "ILER API",
        "Veteran API",
        "DocGen API"
      ],
      "provides": []
    },
    {
      "name": "Claims Evidence API",
      "type": "backend_api",
      "requires": ["VBMS Core DB"],
      "provides": ["Evidence Service"]
    },
    {
      "name": "AWS SageMaker",
      "type": "ml_platform",
      "requires": ["OpenSearch"],
      "provides": ["Model Inference API"]
    },
    {
      "name": "OpenSearch",
      "type": "search_engine",
      "requires": [],
      "provides": ["Search API", "Index API"]
    },
    {
      "name": "VBMS Core DB",
      "type": "database",
      "requires": [],
      "provides": ["Data Access Layer"]
    }
  ],
  "all_communication": "HTTPS port 443 (except DB: Oracle TNS 1521)"
}
```

---

## Diagram 10.1: Services Context (SvcV-1)

**Type**: Service Composition Diagram  
**Source**: Page 10 of PDF  
**Image**: `docs/images/page_10_diagram_1.png`

### Metadata

```yaml
diagram_type: service_context
diagram_name: "Services Context (SvcV-1)"
page: 10

purpose: "Describe and identify service composition and interaction - shows application component, its services, and immediate dependencies"

central_component:
  name: "TERA Memo UI (bip-cpui-tera-memo-ui)"
  vasi_id: "3028"
  type: "React Micro Frontend"
  
service_dependencies:
  - service_name: "Claims Evidence (CE) API"
    service_type: "REST API"
    operations:
      - operation_id: "auto_populate"
        name: "getTeraRecommendations"
        method: "GET"
        endpoint: "/api/tera-recommendations/:veteranId"
        description: "Retrieve AI recommendations from OCR_TEXTRACT_DATA table"
        returns:
          - "Question answers"
          - "Confidence scores"
          - "Evidence links"
        use_case: "On Auto-Population button click"
        
      - operation_id: "get_document"
        name: "getDocumentAnnotations"
        method: "GET"
        endpoint: "/api/documents/:docId/annotations"
        query_params:
          - "page: integer"
        description: "Link to specific evidence locations in documents"
        uses: "Annotator viewer with custom annotations"
        returns:
          - "Document content"
          - "Highlight coordinates"
          - "Text snippets"
        use_case: "On evidence link click"
        
      - operation_id: "write_metrics"
        name: "submitMetrics"
        method: "POST"
        endpoint: "/api/tera-metrics"
        description: "Write submitted answers to TERAMEMOUPLOADMETRICS table"
        request_body:
          - "Veteran ID"
          - "Question answers"
          - "Auto-populate usage"
          - "Manual overrides"
        use_case: "On TERA Memo submission"
    
  - service_name: "Claims API"
    service_type: "REST API"
    operations:
      - operation_id: "get_claims"
        name: "getVeteranClaims"
        method: "GET"
        endpoint: "/api/claims/:veteranId"
        description: "Retrieve Veteran's claim data for association during submission"
        returns:
          - "Open claims list"
          - "Claim IDs"
          - "Claim statuses"
        use_case: "To associate TERA Memo with appropriate claim"
    
  - service_name: "DocGen Genstore API"
    service_type: "REST API"
    operations:
      - operation_id: "generate_preview"
        name: "generatePdf"
        method: "POST"
        endpoint: "/api/docgen/generate"
        description: "Generate PDF document with form data"
        request_body:
          - "Form data"
          - "Veteran info"
          - "All answers"
        returns:
          - "Document ID"
          - "Preview URL"
        processing_time: "2-3 seconds"
        use_case: "On Preview button click"
        
      - operation_id: "submit_document"
        name: "uploadToEfolder"
        method: "POST"
        endpoint: "/api/docgen/upload"
        description: "Upload PDF to Veteran's eFolder in Claim Evidence"
        request_body:
          - "Document ID"
          - "Claim ID"
        use_case: "On Submit button click"
    
  - service_name: "Veteran API"
    service_type: "REST API"
    operations:
      - operation_id: "get_profile"
        name: "getVeteranProfile"
        method: "GET"
        endpoint: "/api/veteran/:fileNumber"
        description: "Retrieve Veteran demographic information"
        returns:
          - "Name"
          - "File number"
          - "Contact info"
          - "EDIPI"
        use_case: "On form load to pre-populate Veteran info"
    
  - service_name: "ILER API"
    service_type: "REST API"
    operations:
      - operation_id: "get_exposure_records"
        name: "getExposureRecords"
        method: "GET"
        endpoint: "/api/iler/:veteranId"
        description: "Retrieve Individual Longitudinal Exposure Record"
        returns:
          - "Deployment locations"
          - "Exposure dates"
          - "Exposure types"
        use_case: "For auto-population data input"

interaction_flows:
  auto_populate_flow:
    - step: 1
      actor: "VSR"
      action: "Clicks Auto-Populate button"
      
    - step: 2
      component: "TERA Memo UI"
      action: "Calls Claims Evidence API"
      endpoint: "GET /tera-recommendations/:veteranId"
      
    - step: 3
      component: "Claims Evidence API"
      action: "Queries OCR_TEXTRACT_DATA table"
      
    - step: 4
      component: "Claims Evidence API"
      action: "Returns JSON response"
      data:
        - "Recommendations for Q1, Q3, Q4, Q6"
        - "Confidence scores"
        - "Evidence links"
      
    - step: 5
      component: "TERA Memo UI"
      action: "Renders recommendations in form"
      displays:
        - "Answer selections"
        - "Confidence badges"
        - "Evidence link buttons"
  
  evidence_review_flow:
    - step: 1
      actor: "VSR"
      action: "Clicks evidence link"
      
    - step: 2
      component: "TERA Memo UI"
      action: "Calls Claims Evidence API"
      endpoint: "GET /documents/:docId/annotations?page=:page"
      
    - step: 3
      component: "Claims Evidence API"
      action: "Retrieves document and highlight data"
      
    - step: 4
      component: "TERA Memo UI"
      action: "Opens annotator viewer in new tab"
      shows:
        - "Document PDF"
        - "Highlighted text"
        - "Page navigation"
  
  submission_flow:
    - step: 1
      actor: "VSR"
      action: "Clicks Submit button"
      
    - step: 2
      component: "TERA Memo UI"
      action: "Calls DocGen API"
      endpoint: "POST /generate"
      
    - step: 3
      component: "DocGen API"
      action: "Generates PDF"
      duration: "2-3 seconds"
      
    - step: 4
      component: "TERA Memo UI"
      action: "Calls DocGen API"
      endpoint: "POST /upload"
      
    - step: 5
      component: "DocGen API"
      action: "Uploads to eFolder"
      
    - step: 6
      component: "TERA Memo UI"
      action: "Calls Claims Evidence API"
      endpoint: "POST /tera-metrics"
      
    - step: 7
      component: "TERA Memo UI"
      action: "Displays success message"
```

### JSON Representation

```json
{
  "diagram_id": "page_10_diagram_1",
  "type": "service_context",
  "title": "Services Context (SvcV-1)",
  "central_component": "TERA Memo UI (CPUI #3028)",
  "service_dependencies": [
    {
      "service": "Claims Evidence API",
      "operations": ["getTeraRecommendations", "getDocumentAnnotations", "submitMetrics"]
    },
    {
      "service": "Claims API",
      "operations": ["getVeteranClaims"]
    },
    {
      "service": "DocGen Genstore API",
      "operations": ["generatePdf", "uploadToEfolder"]
    },
    {
      "service": "Veteran API",
      "operations": ["getVeteranProfile"]
    },
    {
      "service": "ILER API",
      "operations": ["getExposureRecords"]
    }
  ],
  "all_services_use": "REST/HTTPS protocol"
}
```

---

## Diagram 12.1: Conceptual Data Model (DIV-1)

**Type**: Entity-Relationship Diagram  
**Source**: Page 12 of PDF  
**Image**: `docs/images/page_12_diagram_1.png`

### Metadata

```yaml
diagram_type: entity_relationship_diagram
diagram_name: "Conceptual Data Model (DIV-1)"
page: 12

entities:
  - entity_name: "VETERAN"
    entity_type: "master_data"
    primary_key: "file_number"
    attributes:
      - name: "file_number"
        type: "varchar(20)"
        constraints: ["PRIMARY KEY", "NOT NULL"]
      - name: "name"
        type: "varchar(200)"
      - name: "date_of_birth"
        type: "date"
      - name: "ssn"
        type: "varchar(11)"
        sensitive: true
    
  - entity_name: "CLAIM"
    entity_type: "transactional"
    primary_key: "claim_id"
    attributes:
      - name: "claim_id"
        type: "number"
        constraints: ["PRIMARY KEY", "NOT NULL"]
      - name: "veteran_file_number"
        type: "varchar(20)"
        constraints: ["FOREIGN KEY references VETERAN"]
      - name: "claim_date"
        type: "timestamp"
      - name: "status"
        type: "varchar(50)"
    
  - entity_name: "TERA_MEMO"
    entity_type: "transactional"
    primary_key: "memo_id"
    attributes:
      - name: "memo_id"
        type: "number"
        constraints: ["PRIMARY KEY", "NOT NULL", "AUTO_INCREMENT"]
      - name: "veteran_file_number"
        type: "varchar(20)"
        constraints: ["FOREIGN KEY references VETERAN"]
      - name: "claim_id"
        type: "number"
        constraints: ["FOREIGN KEY references CLAIM"]
      - name: "created_date"
        type: "timestamp"
        default: "CURRENT_TIMESTAMP"
      - name: "submitted_date"
        type: "timestamp"
      - name: "status"
        type: "varchar(20)"
        allowed_values: ["draft", "submitted", "completed"]
      - name: "created_by_user_id"
        type: "varchar(50)"
    
  - entity_name: "TERA_QUESTION_ANSWER"
    entity_type: "detail"
    primary_key: "answer_id"
    attributes:
      - name: "answer_id"
        type: "number"
        constraints: ["PRIMARY KEY", "NOT NULL", "AUTO_INCREMENT"]
      - name: "memo_id"
        type: "number"
        constraints: ["FOREIGN KEY references TERA_MEMO"]
      - name: "question_number"
        type: "number"
        constraints: ["CHECK (question_number BETWEEN 1 AND 6)"]
      - name: "answer_value"
        type: "varchar(10)"
        allowed_values: ["yes", "no", "unsure"]
      - name: "free_text_response"
        type: "clob"
        max_length: 4000
      - name: "auto_populated"
        type: "char(1)"
        allowed_values: ["Y", "N"]
      - name: "confidence_score"
        type: "number(5,2)"
        constraints: ["CHECK (confidence_score BETWEEN 0 AND 100)"]
      - name: "manually_reviewed"
        type: "char(1)"
        allowed_values: ["Y", "N"]
      - name: "modified_by_user"
        type: "char(1)"
        allowed_values: ["Y", "N"]
        description: "Did VSR override AI recommendation"
    
  - entity_name: "EVIDENCE_LINK"
    entity_type: "detail"
    primary_key: "link_id"
    attributes:
      - name: "link_id"
        type: "number"
        constraints: ["PRIMARY KEY", "NOT NULL", "AUTO_INCREMENT"]
      - name: "answer_id"
        type: "number"
        constraints: ["FOREIGN KEY references TERA_QUESTION_ANSWER"]
      - name: "document_id"
        type: "varchar(50)"
      - name: "page_number"
        type: "number"
      - name: "highlight_start_position"
        type: "number"
        description: "Character position in document"
      - name: "highlight_end_position"
        type: "number"
      - name: "evidence_text_snippet"
        type: "varchar(500)"
      - name: "relevance_score"
        type: "number(3,2)"
        constraints: ["CHECK (relevance_score BETWEEN 0 AND 1)"]
    
  - entity_name: "OCR_TEXTRACT_DATA"
    entity_type: "ai_generated"
    primary_key: "textract_id"
    attributes:
      - name: "textract_id"
        type: "number"
        constraints: ["PRIMARY KEY", "NOT NULL", "AUTO_INCREMENT"]
      - name: "veteran_file_number"
        type: "varchar(20)"
        constraints: ["FOREIGN KEY references VETERAN"]
      - name: "document_id"
        type: "varchar(50)"
      - name: "extracted_text"
        type: "clob"
      - name: "processing_date"
        type: "timestamp"
      - name: "ocr_confidence"
        type: "number(5,2)"
    
  - entity_name: "TERA_RECOMMENDATION"
    entity_type: "ai_generated"
    primary_key: "recommendation_id"
    attributes:
      - name: "recommendation_id"
        type: "number"
        constraints: ["PRIMARY KEY", "NOT NULL", "AUTO_INCREMENT"]
      - name: "veteran_file_number"
        type: "varchar(20)"
        constraints: ["FOREIGN KEY references VETERAN"]
      - name: "question_number"
        type: "number"
        constraints: ["CHECK (question_number IN (1,3,4,6))"]
      - name: "recommended_answer"
        type: "varchar(10)"
        allowed_values: ["yes", "no"]
      - name: "confidence_score"
        type: "number(5,2)"
      - name: "supporting_text"
        type: "clob"
      - name: "model_version"
        type: "varchar(20)"
      - name: "generated_date"
        type: "timestamp"

relationships:
  - relationship: "VETERAN has many CLAIMs"
    from_entity: "VETERAN"
    to_entity: "CLAIM"
    cardinality: "1:N"
    foreign_key: "veteran_file_number"
    
  - relationship: "VETERAN has many TERA_MEMOs"
    from_entity: "VETERAN"
    to_entity: "TERA_MEMO"
    cardinality: "1:N"
    foreign_key: "veteran_file_number"
    
  - relationship: "CLAIM has many TERA_MEMOs"
    from_entity: "CLAIM"
    to_entity: "TERA_MEMO"
    cardinality: "1:N"
    foreign_key: "claim_id"
    
  - relationship: "TERA_MEMO has many TERA_QUESTION_ANSWERs"
    from_entity: "TERA_MEMO"
    to_entity: "TERA_QUESTION_ANSWER"
    cardinality: "1:N"
    foreign_key: "memo_id"
    description: "One memo contains 6 questions (1-6)"
    
  - relationship: "TERA_QUESTION_ANSWER has many EVIDENCE_LINKs"
    from_entity: "TERA_QUESTION_ANSWER"
    to_entity: "EVIDENCE_LINK"
    cardinality: "1:N"
    foreign_key: "answer_id"
    description: "One answer can have multiple supporting evidence links"
    
  - relationship: "VETERAN has many OCR_TEXTRACT_DATAs"
    from_entity: "VETERAN"
    to_entity: "OCR_TEXTRACT_DATA"
    cardinality: "1:N"
    foreign_key: "veteran_file_number"
    
  - relationship: "VETERAN has many TERA_RECOMMENDATIONs"
    from_entity: "VETERAN"
    to_entity: "TERA_RECOMMENDATION"
    cardinality: "1:N"
    foreign_key: "veteran_file_number"
    
  - relationship: "DOCUMENT referenced by EVIDENCE_LINKs"
    from_entity: "DOCUMENT (external)"
    to_entity: "EVIDENCE_LINK"
    cardinality: "1:N"
    foreign_key: "document_id"
    note: "DOCUMENT is external entity in eFolder system"

entity_groups:
  master_data:
    - "VETERAN"
  
  transactional_data:
    - "CLAIM"
    - "TERA_MEMO"
    - "TERA_QUESTION_ANSWER"
    - "EVIDENCE_LINK"
  
  ai_generated_data:
    - "OCR_TEXTRACT_DATA"
    - "TERA_RECOMMENDATION"
```

### JSON Representation

```json
{
  "diagram_id": "page_12_diagram_1",
  "type": "erd",
  "title": "Conceptual Data Model (DIV-1)",
  "entities": [
    {
      "name": "VETERAN",
      "pk": "file_number",
      "type": "master"
    },
    {
      "name": "CLAIM",
      "pk": "claim_id",
      "fk": ["veteran_file_number"],
      "type": "transactional"
    },
    {
      "name": "TERA_MEMO",
      "pk": "memo_id",
      "fk": ["veteran_file_number", "claim_id"],
      "type": "transactional"
    },
    {
      "name": "TERA_QUESTION_ANSWER",
      "pk": "answer_id",
      "fk": ["memo_id"],
      "type": "detail",
      "key_fields": ["question_number", "answer_value", "confidence_score", "auto_populated", "modified_by_user"]
    },
    {
      "name": "EVIDENCE_LINK",
      "pk": "link_id",
      "fk": ["answer_id"],
      "type": "detail",
      "key_fields": ["document_id", "page_number", "highlight_coordinates", "relevance_score"]
    },
    {
      "name": "OCR_TEXTRACT_DATA",
      "pk": "textract_id",
      "fk": ["veteran_file_number"],
      "type": "ai_generated"
    },
    {
      "name": "TERA_RECOMMENDATION",
      "pk": "recommendation_id",
      "fk": ["veteran_file_number"],
      "type": "ai_generated",
      "key_fields": ["question_number", "recommended_answer", "confidence_score"]
    }
  ],
  "relationships": [
    {"from": "VETERAN", "to": "CLAIM", "type": "1:N"},
    {"from": "VETERAN", "to": "TERA_MEMO", "type": "1:N"},
    {"from": "CLAIM", "to": "TERA_MEMO", "type": "1:N"},
    {"from": "TERA_MEMO", "to": "TERA_QUESTION_ANSWER", "type": "1:N"},
    {"from": "TERA_QUESTION_ANSWER", "to": "EVIDENCE_LINK", "type": "1:N"}
  ]
}
```

---

*File continues with remaining diagrams 12.2, 13.1, 14.1, 15.1, and 15.2...*

[Due to length, I'll create a separate file for the remaining diagrams]
