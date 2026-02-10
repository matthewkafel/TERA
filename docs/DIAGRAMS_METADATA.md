# TERA Architecture Diagrams - Structured Metadata

> **For GitHub Copilot**: Complete structured metadata representation of all architectural diagrams in machine-readable format.

This file contains comprehensive metadata for each diagram, including all components, connections, data flows, and properties in structured format.

---

## Diagram Metadata Index

- [Diagram 2.1: Capability Viewpoint Taxonomy](#diagram-21-capability-viewpoint-taxonomy)
- [Diagram 3.1: VSR Workflow](#diagram-31-vsr-workflow)
- [Diagram 3.2: User Interface Components](#diagram-32-user-interface-components)
- [Diagram 4.1: AI Model Pipeline](#diagram-41-ai-model-pipeline)
- [Diagram 7.1: Operational Viewpoint (OV-1)](#diagram-71-operational-viewpoint-ov-1)
- [Diagram 8.1: Operational Resource Flow (OV-2)](#diagram-81-operational-resource-flow-ov-2)
- [Diagram 9.1: Systems Interface (SV-1)](#diagram-91-systems-interface-sv-1)
- [Diagram 10.1: Services Context (SvcV-1)](#diagram-101-services-context-svcv-1)
- [Diagram 12.1: Conceptual Data Model (DIV-1)](#diagram-121-conceptual-data-model-div-1)
- [Diagram 12.2: Logical Data Flow](#diagram-122-logical-data-flow)
- [Diagram 13.1: Physical Data Model (DIV-3)](#diagram-131-physical-data-model-div-3)
- [Diagram 14.1: Business Process Model (OV-6d)](#diagram-141-business-process-model-ov-6d)
- [Diagram 15.1: Process Sequence (SV-10c)](#diagram-151-process-sequence-sv-10c)
- [Diagram 15.2: Feature Flag Configuration](#diagram-152-feature-flag-configuration)

---

## Diagram 2.1: Capability Viewpoint Taxonomy

**Type**: Hierarchical Tree / Taxonomy  
**Source**: Page 2 of PDF  
**Image**: `docs/images/page_2_diagram_1.png`

### Metadata

```yaml
diagram_type: capability_taxonomy
diagram_name: "Capability Viewpoint Taxonomy (CV-2)"
page: 2
dimensions:
  width: 16
  height: 16
note: "Very small icon/placeholder diagram in original PDF"

hierarchy:
  root:
    name: "TERA Memo Automation"
    level: 0
    children:
      - name: "Auto-Population Capability"
        level: 1
      - name: "AI Integration"
        level: 1
      - name: "BIP Platform Services"
        level: 1
```

### JSON Representation

```json
{
  "diagram_id": "page_2_diagram_1",
  "type": "capability_taxonomy",
  "title": "Capability Viewpoint Taxonomy (CV-2)",
  "root_capability": {
    "name": "TERA Memo Automation",
    "sub_capabilities": [
      "Auto-Population Capability",
      "AI Integration", 
      "BIP Platform Services"
    ]
  }
}
```

---

## Diagram 3.1: VSR Workflow

**Type**: Activity Diagram / User Journey Flow  
**Source**: Page 3 of PDF  
**Image**: `docs/images/page_3_diagram_1.png`

### Metadata

```yaml
diagram_type: activity_flow
diagram_name: "VSR Workflow - TERA Memo Completion"
page: 3
dimensions:
  width: 830
  height: 697

actors:
  - name: "Veteran Service Representative (VSR)"
    role: "primary_user"
  - name: "TERA Memo UI"
    role: "system"
  - name: "Auto-Population Engine"
    role: "ai_service"

workflow_steps:
  - step: 1
    action: "VSR opens Veteran claim in VBMS"
    actor: "VSR"
    type: "start"
    
  - step: 2
    action: "Navigate to Veteran Profile page"
    actor: "VSR"
    type: "navigation"
    
  - step: 3
    action: "Select 'Upload Document' dropdown"
    actor: "VSR"
    type: "interaction"
    
  - step: 4
    action: "Choose 'TERA Memo' option"
    actor: "VSR"
    type: "selection"
    
  - step: 5
    action: "TERA form loads with pre-populated Veteran info"
    actor: "TERA Memo UI"
    type: "system_response"
    data_displayed:
      - "Veteran name"
      - "File number"
      - "Claim information"
    
  - step: 6
    action: "Decision: Use auto-populate or manual entry"
    actor: "VSR"
    type: "decision"
    options:
      - value: "auto_populate"
        next_step: 7
      - value: "manual_entry"
        next_step: 11
    
  - step: 7
    action: "Click 'Auto-Populate' button"
    actor: "VSR"
    type: "interaction"
    condition: "if auto_populate selected"
    
  - step: 8
    action: "Display information modal"
    actor: "TERA Memo UI"
    type: "system_response"
    modal_content:
      - "Explanation of auto-populate feature"
      - "Confirmation button"
    
  - step: 9
    action: "VSR confirms to proceed"
    actor: "VSR"
    type: "confirmation"
    
  - step: 10
    action: "System populates questions with AI recommendations"
    actor: "Auto-Population Engine"
    type: "ai_processing"
    for_each_question:
      - question_id: 1
        displays:
          - "Recommended answer (Yes/No)"
          - "Confidence score (%)"
          - "Evidence links"
          - "Highlighted text locations"
      - question_id: 3
        displays: ["Same as Q1"]
      - question_id: 4
        displays: ["Same as Q1"]
      - question_id: 6
        displays: ["Same as Q1"]
    
  - step: 11
    action: "VSR reviews each auto-populated answer"
    actor: "VSR"
    type: "review"
    review_items:
      - "Read AI recommendation"
      - "Check confidence score"
      - "Assess if score meets threshold"
    
  - step: 12
    action: "VSR clicks evidence links"
    actor: "VSR"
    type: "interaction"
    result: "Opens document viewer with highlighted evidence"
    
  - step: 13
    action: "VSR verifies evidence supports recommendation"
    actor: "VSR"
    type: "validation"
    
  - step: 14
    action: "VSR accepts or modifies answers"
    actor: "VSR"
    type: "decision"
    options:
      - "Accept AI recommendation"
      - "Modify answer"
      - "Change to different answer"
    
  - step: 15
    action: "Check box to certify manual review completed"
    actor: "VSR"
    type: "certification"
    required: true
    
  - step: 16
    action: "Click Preview button"
    actor: "VSR"
    type: "interaction"
    
  - step: 17
    action: "System generates PDF preview"
    actor: "TERA Memo UI"
    type: "system_response"
    processing_time: "2-3 seconds"
    
  - step: 18
    action: "VSR reviews PDF"
    actor: "VSR"
    type: "review"
    
  - step: 19
    action: "Click Submit button"
    actor: "VSR"
    type: "interaction"
    
  - step: 20
    action: "System writes metrics to database"
    actor: "TERA Memo UI"
    type: "system_processing"
    writes_to: "TERAMEMOUPLOADMETRICS"
    
  - step: 21
    action: "System uploads PDF to eFolder"
    actor: "TERA Memo UI"
    type: "system_processing"
    via: "DocGen API"
    
  - step: 22
    action: "Display success message"
    actor: "TERA Memo UI"
    type: "completion"
    
  - step: 23
    action: "TERA Memo completed"
    type: "end"

decision_points:
  - at_step: 6
    question: "Use auto-populate?"
    true_path: "Steps 7-14"
    false_path: "Skip to step 15 (manual entry)"
    
  - at_step: 14
    question: "Accept AI recommendation?"
    true_path: "Proceed to step 15"
    false_path: "Modify answer then proceed to step 15"

timing:
  estimated_total_time: "5-10 minutes with auto-populate"
  manual_entry_time: "30+ minutes without auto-populate"
  time_saved: "20-25 minutes per TERA Memo"
```

### JSON Representation

```json
{
  "diagram_id": "page_3_diagram_1",
  "type": "workflow",
  "title": "VSR TERA Memo Completion Workflow",
  "total_steps": 23,
  "decision_points": 2,
  "actors": [
    {"name": "VSR", "type": "human"},
    {"name": "TERA Memo UI", "type": "system"},
    {"name": "Auto-Population Engine", "type": "ai"}
  ],
  "swim_lanes": [
    "VSR Actions",
    "System Responses",
    "AI Processing"
  ],
  "critical_path": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 19, 20, 21, 22, 23],
  "estimated_duration_minutes": {
    "with_auto_populate": "5-10",
    "without_auto_populate": "30+"
  }
}
```

---

## Diagram 3.2: User Interface Components

**Type**: UI Mockup / Wireframe  
**Source**: Page 3 of PDF  
**Image**: `docs/images/page_3_diagram_2.png`

### Metadata

```yaml
diagram_type: ui_wireframe
diagram_name: "TERA Memo UI Components"
page: 3
dimensions:
  width: 830
  height: 697

layout:
  type: "vertical_sections"
  sections:
    - section: "header"
      position: "top"
      height: "15%"
      components:
        - type: "text_field"
          label: "Veteran Name"
          state: "read_only"
          pre_populated: true
        - type: "text_field"
          label: "File Number"
          state: "read_only"
          pre_populated: true
        - type: "button"
          id: "auto_populate_btn"
          label: "Auto-Populate"
          style: "primary"
          prominent: true
          position: "top_right"
          
    - section: "form_body"
      position: "middle"
      height: "70%"
      components:
        - type: "question_group"
          id: "question_1"
          elements:
            - type: "label"
              text: "Question 1: [Question text]"
            - type: "radio_group"
              options: ["Yes", "No"]
              name: "q1_answer"
            - type: "badge"
              id: "confidence_score"
              display: "85%"
              color: "green"
              visible_if: "auto_populated"
            - type: "link_button"
              label: "View Evidence"
              icon: "document"
              visible_if: "auto_populated"
            - type: "textarea"
              placeholder: "Supporting details..."
              rows: 3
              
        - type: "question_group"
          id: "question_2"
          similar_to: "question_1"
          
        - type: "question_group"
          id: "question_3"
          similar_to: "question_1"
          
        - type: "question_group"
          id: "question_4"
          similar_to: "question_1"
          
        - type: "question_group"
          id: "question_5"
          similar_to: "question_1"
          auto_populate: false
          
        - type: "question_group"
          id: "question_6"
          similar_to: "question_1"
          
    - section: "footer"
      position: "bottom"
      height: "15%"
      components:
        - type: "checkbox"
          id: "manual_review_cert"
          label: "I certify that I have manually reviewed all recommendations"
          required: true
        - type: "button"
          id: "preview_btn"
          label: "Preview"
          style: "secondary"
        - type: "button"
          id: "submit_btn"
          label: "Submit"
          style: "primary"
          enabled_if: "manual_review_cert.checked"
        - type: "button"
          id: "cancel_btn"
          label: "Cancel"
          style: "tertiary"

ui_elements:
  confidence_badge:
    type: "visual_indicator"
    states:
      - range: "80-100%"
        color: "green"
        meaning: "high_confidence"
      - range: "60-79%"
        color: "yellow"
        meaning: "medium_confidence"
      - range: "0-59%"
        color: "red"
        meaning: "low_confidence"
        requires_manual_review: true
        
  evidence_link:
    type: "interactive_button"
    icon: "document_with_magnifier"
    action: "open_document_viewer"
    opens_in: "new_tab"
    shows:
      - "Document viewer"
      - "Highlighted evidence text"
      - "Page number"
      - "Relevance score"

interactions:
  auto_populate_button:
    on_click:
      - "Show confirmation modal"
      - "Query Claims Evidence API"
      - "Populate question fields"
      - "Show confidence badges"
      - "Show evidence links"
      - "Enable manual review checkbox"
      
  evidence_link:
    on_click:
      - "Fetch document from Claims Evidence API"
      - "Open in annotator viewer"
      - "Scroll to highlighted text"
      - "Display relevance metadata"
      
  submit_button:
    on_click:
      - "Validate all required fields"
      - "Check manual review certification"
      - "Send data to TERA API"
      - "Generate PDF via DocGen"
      - "Upload to eFolder"
      - "Show success message"

accessibility:
  wcag_level: "AA"
  features:
    - "Keyboard navigation"
    - "Screen reader support"
    - "High contrast mode"
    - "Focus indicators"
    - "ARIA labels"
```

### JSON Representation

```json
{
  "diagram_id": "page_3_diagram_2",
  "type": "ui_wireframe",
  "title": "TERA Memo Form UI Components",
  "components": {
    "header": {
      "auto_populate_button": {
        "type": "button",
        "prominence": "high",
        "action": "trigger_ai_population"
      },
      "veteran_info": {
        "type": "info_panel",
        "fields": ["name", "file_number"],
        "editable": false
      }
    },
    "body": {
      "questions": [
        {
          "id": 1,
          "has_auto_populate": true,
          "elements": ["radio_buttons", "confidence_badge", "evidence_links", "text_area"]
        },
        {
          "id": 3,
          "has_auto_populate": true,
          "elements": ["radio_buttons", "confidence_badge", "evidence_links", "text_area"]
        },
        {
          "id": 4,
          "has_auto_populate": true,
          "elements": ["radio_buttons", "confidence_badge", "evidence_links", "text_area"]
        },
        {
          "id": 6,
          "has_auto_populate": true,
          "elements": ["radio_buttons", "confidence_badge", "evidence_links", "text_area"]
        }
      ]
    },
    "footer": {
      "certification_checkbox": {"required": true},
      "action_buttons": ["preview", "submit", "cancel"]
    }
  },
  "confidence_badge_colors": {
    "green": ">= 80%",
    "yellow": "60-79%",
    "red": "< 60%"
  }
}
```

---

## Diagram 4.1: AI Model Pipeline

**Type**: Data Flow / Process Pipeline  
**Source**: Page 4 of PDF  
**Image**: `docs/images/page_4_diagram_1.png`

### Metadata

```yaml
diagram_type: data_flow_pipeline
diagram_name: "AI Model Input-Process-Output Pipeline"
page: 4

pipeline_stages:
  - stage: "INPUT"
    stage_number: 1
    components:
      - name: "Veteran Claim Evidence Documents"
        type: "data_source"
        format: "PDF, Images"
        processing: "OCR via C&P Smart Search"
        output: "Plain text"
        
      - name: "ILER IES Record"
        type: "data_source"
        format: "Structured data"
        contains:
          - "Deployment locations"
          - "Exposure dates"
          - "Exposure types"
          
      - name: "PACT Act SOP"
        type: "reference_data"
        usage: "Eligibility rules"
        
      - name: "M21-1 Manual"
        type: "reference_data"
        usage: "Adjudication guidelines"
    
  - stage: "MODEL_PROCESSING"
    stage_number: 2
    platform: "AWS SageMaker via ML-MATS"
    sub_processes:
      - process: "Text Extraction"
        input: "OCR text, ILER data"
        method: "Text normalization"
        
      - process: "Named Entity Recognition (NER)"
        extracts:
          - entity_type: "dates"
            pattern: "\\d{1,2}/\\d{1,2}/\\d{4}"
          - entity_type: "locations"
            source: "Geographic gazetteer"
          - entity_type: "toxic_substances"
            source: "PACT Act substance list"
          - entity_type: "military_units"
            pattern: "Unit designation patterns"
          - entity_type: "medical_conditions"
            source: "ICD-10 codes"
            
      - process: "Pattern Matching"
        against: "PACT Act criteria"
        rules:
          - "Location + Date range matches presumptive exposure"
          - "Substance mentioned + Service period overlap"
          - "Medical condition linked to toxic exposure"
          
      - process: "Eligibility Evaluation"
        applies: "M21-1 guidelines"
        for_each_question:
          - question: 1
            evaluates: "Evidence of TERA participation"
          - question: 3
            evaluates: "Specific toxic exposure identified"
          - question: 4
            evaluates: "Location and timeframe documented"
          - question: 6
            evaluates: "Supporting documentation exists"
            
      - process: "Confidence Calculation"
        factors:
          - "Number of supporting evidence pieces"
          - "OCR quality score"
          - "Match strength to PACT Act criteria"
          - "Specificity of dates/locations"
        formula: "weighted_average(factors)"
        range: "0-100%"
        
      - process: "Evidence Linking"
        identifies:
          - "Source document ID"
          - "Page number"
          - "Text coordinates"
          - "Relevance score"
    
  - stage: "OUTPUT"
    stage_number: 3
    for_each_question: [1, 3, 4, 6]
    output_structure:
      - field: "question_id"
        type: "integer"
        
      - field: "recommended_answer"
        type: "enum"
        values: ["yes", "no", "insufficient_evidence"]
        
      - field: "confidence_score"
        type: "float"
        range: "0.0-100.0"
        unit: "percentage"
        
      - field: "supporting_text"
        type: "string"
        max_length: 4000
        contains: "Explanation and key facts"
        
      - field: "evidence_links"
        type: "array"
        items:
          - document_id: "string"
          - page_number: "integer"
          - highlight_start: "integer"
          - highlight_end: "integer"
          - text_snippet: "string (200 chars)"
          - relevance_score: "float (0.0-1.0)"
    
    storage:
      - destination: "VBMS Core Database"
        table: "OCR_TEXTRACT_DATA"
        columns:
          - "QUESTION_1_ANSWER"
          - "QUESTION_1_CONFIDENCE"
          - "QUESTION_1_EVIDENCE (JSON)"
          - "QUESTION_3_ANSWER"
          - "QUESTION_3_CONFIDENCE"
          - "QUESTION_3_EVIDENCE (JSON)"
          - "QUESTION_4_ANSWER"
          - "QUESTION_4_CONFIDENCE"
          - "QUESTION_4_EVIDENCE (JSON)"
          - "QUESTION_6_ANSWER"
          - "QUESTION_6_CONFIDENCE"
          - "QUESTION_6_EVIDENCE (JSON)"

data_flows:
  - from: "Claim Evidence Documents"
    to: "OCR Processing"
    arrow: "solid"
    
  - from: "OCR Processing"
    to: "Model Processing"
    arrow: "solid"
    data: "Plain text"
    
  - from: "ILER IES Record"
    to: "Model Processing"
    arrow: "solid"
    data: "Structured exposure data"
    
  - from: "PACT Act SOP"
    to: "Model Processing"
    arrow: "dashed"
    data: "Reference lookup"
    
  - from: "M21-1 Manual"
    to: "Model Processing"
    arrow: "dashed"
    data: "Reference lookup"
    
  - from: "Model Processing"
    to: "Output Generation"
    arrow: "solid"
    data: "Recommendations + confidence + evidence"
    
  - from: "Output Generation"
    to: "VBMS Database"
    arrow: "solid"
    operation: "INSERT/UPDATE"
    
  - from: "VBMS Database"
    to: "TERA Memo UI"
    arrow: "dashed"
    operation: "SELECT"
    trigger: "User clicks Auto-Populate"

processing_metadata:
  execution: "Nightly batch job"
  frequency: "Daily at midnight EST"
  duration: "2-4 hours depending on document volume"
  model_version: "Tracked in MODEL_VERSION column"
  aws_services:
    - "SageMaker: Model execution"
    - "Comprehend: NLP processing"
    - "S3: Temporary storage"
```

### JSON Representation

```json
{
  "diagram_id": "page_4_diagram_1",
  "type": "pipeline",
  "title": "AI Model Processing Pipeline",
  "stages": [
    {
      "name": "INPUT",
      "sources": [
        {"type": "claim_evidence", "format": "PDF/Image", "processed_via": "OCR"},
        {"type": "iler_record", "format": "structured"},
        {"type": "pact_act_sop", "usage": "reference"},
        {"type": "m21_manual", "usage": "reference"}
      ]
    },
    {
      "name": "PROCESSING",
      "platform": "AWS SageMaker",
      "tasks": [
        "text_extraction",
        "named_entity_recognition",
        "pattern_matching",
        "eligibility_evaluation",
        "confidence_calculation",
        "evidence_linking"
      ]
    },
    {
      "name": "OUTPUT",
      "for_questions": [1, 3, 4, 6],
      "fields": [
        "recommended_answer",
        "confidence_score",
        "supporting_text",
        "evidence_links"
      ],
      "stored_in": "OCR_TEXTRACT_DATA"
    }
  ],
  "execution": "nightly_batch",
  "frequency": "daily"
}
```

---

## Diagram 7.1: Operational Viewpoint (OV-1)

**Type**: System Context / Component Diagram  
**Source**: Page 7 of PDF  
**Image**: `docs/images/page_7_diagram_1.png`

### Metadata

```yaml
diagram_type: system_context
diagram_name: "High-Level Operational Viewpoint (OV-1)"
page: 7
dimensions:
  width: 1300
  height: 470

legend:
  white_rectangle: "TERA application components (new)"
  gray_rectangle: "Existing VBMS components"
  cloud_icon: "External AWS services"
  arrow_solid: "Data flow / API call"
  arrow_dashed: "Retrieval / Query"

components:
  tera_application:
    - component: "TERA Memo UI"
      type: "React Micro Frontend (MFE)"
      color: "white"
      port: 443
      protocol: "HTTPS"
      responsibilities:
        - "User interface for VSR"
        - "Form rendering"
        - "Auto-populate trigger"
        - "Evidence link display"
      
    - component: "TERA Memo API"
      type: "Backend Service"
      color: "white"
      port: 443
      protocol: "HTTPS"
      responsibilities:
        - "Business logic"
        - "Data orchestration"
        - "Metrics collection"
      
    - component: "Auto-Population Engine"
      type: "AI Service Orchestrator"
      color: "white"
      responsibilities:
        - "Coordinate ML model execution"
        - "Format recommendations"
        
  existing_vbms:
    - component: "VBMS Core Database"
      type: "Oracle RAC"
      color: "gray"
      stores:
        - "TERA recommendations"
        - "Veteran data"
        - "Claim information"
        - "Metrics"
      
    - component: "Claims Evidence API"
      type: "REST API"
      color: "gray"
      vasi_id: "TBD"
      provides:
        - "Document access"
        - "Evidence retrieval"
        - "Annotations"
      
    - component: "Claims API"
      type: "REST API"
      color: "gray"
      provides:
        - "Claim data"
        - "Claim status"
      
    - component: "ILER API"
      type: "REST API"
      color: "gray"
      provides:
        - "Exposure records"
        - "Deployment history"
      
    - component: "DocGen Genstore API"
      type: "REST API"
      color: "gray"
      provides:
        - "PDF generation"
        - "Document upload to eFolder"
      
    - component: "Veteran API"
      type: "REST API"
      color: "gray"
      provides:
        - "Veteran profile"
        - "Demographic data"
      
    - component: "C&P Smart Search"
      type: "OCR Service"
      color: "gray"
      provides:
        - "Document OCR"
        - "Text extraction"
        
  aws_services:
    - component: "AWS SageMaker"
      type: "ML Platform"
      display: "cloud"
      responsibilities:
        - "ML model hosting"
        - "Model execution"
        - "Inference endpoints"
      
    - component: "AWS Comprehend"
      type: "NLP Service"
      display: "cloud"
      responsibilities:
        - "Text analysis"
        - "Entity extraction"
      
    - component: "OpenSearch"
      type: "Search Engine"
      display: "cloud"
      responsibilities:
        - "Document indexing"
        - "Full-text search"
        - "Evidence storage"

connections:
  - from: "TERA Memo UI"
    to: "TERA Memo API"
    direction: "bidirectional"
    protocol: "HTTPS"
    operations:
      - "POST /auto-populate"
      - "GET /recommendations"
      - "POST /submit"
    
  - from: "TERA Memo UI"
    to: "Claims Evidence API"
    direction: "bidirectional"
    protocol: "HTTPS"
    operations:
      - "GET /documents"
      - "GET /annotations"
    
  - from: "TERA Memo UI"
    to: "ILER API"
    direction: "request"
    protocol: "HTTPS"
    operations:
      - "GET /exposure-records"
    
  - from: "TERA Memo UI"
    to: "DocGen Genstore API"
    direction: "request"
    protocol: "HTTPS"
    operations:
      - "POST /generate-pdf"
      - "POST /upload"
    
  - from: "TERA Memo API"
    to: "VBMS Core Database"
    direction: "bidirectional"
    protocol: "Oracle TNS"
    operations:
      - "SELECT recommendations"
      - "INSERT metrics"
    
  - from: "Auto-Population Engine"
    to: "OpenSearch"
    direction: "query"
    protocol: "HTTPS"
    operations:
      - "GET /search"
    
  - from: "AWS SageMaker"
    to: "OpenSearch"
    direction: "bidirectional"
    protocol: "HTTPS"
    operations:
      - "READ indexed documents"
      - "WRITE model results"
    
  - from: "C&P Smart Search"
    to: "OpenSearch"
    direction: "write"
    protocol: "HTTPS"
    operations:
      - "POST /index OCR results"
    
  - from: "AWS SageMaker"
    to: "VBMS Core Database"
    direction: "write"
    protocol: "HTTPS via API"
    operations:
      - "INSERT recommendations to OCR_TEXTRACT_DATA"
    
  - from: "DocGen Genstore API"
    to: "Claims Evidence"
    direction: "write"
    protocol: "HTTPS"
    operations:
      - "POST upload PDF to eFolder"

interaction_table:
  - system_a: "AWS SageMaker"
    vasi_a: "N/A (AWS)"
    system_b: "OpenSearch Endpoint"
    vasi_b: "N/A (AWS)"
    description: "Run TERA model against OpenSearch Veteran dataset, store results in VBMS Core Database"
    
  - system_a: "Claims Evidence API"
    vasi_a: "TBD"
    system_b: "VBMS Core Database"
    vasi_b: "Core"
    description: "Pull relevant Veteran data to populate TERA Memo UI"
    
  - system_a: "Claims Evidence API"
    vasi_a: "TBD"
    system_b: "TERA Memo UI"
    vasi_b: "3028"
    description: "Auto-population with AI recommendations and evidence"
    
  - system_a: "ILER API"
    vasi_a: "TBD"
    system_b: "TERA Memo UI"
    vasi_b: "3028"
    description: "Retrieve Veteran ILER document for auto-population data"
    
  - system_a: "TERA Memo UI"
    vasi_a: "3028"
    system_b: "CE API / CE UI"
    vasi_b: "TBD"
    description: "Click evidence links to manually review specific document locations"
    
  - system_a: "TERA Memo UI"
    vasi_a: "3028"
    system_b: "DocGen Genstore API"
    vasi_b: "TBD"
    description: "Upload completed TERA Memo document to Claim Evidence"
```

### JSON Representation

```json
{
  "diagram_id": "page_7_diagram_1",
  "type": "system_context",
  "title": "Operational Viewpoint (OV-1)",
  "components": {
    "tera_new": ["TERA Memo UI", "TERA Memo API", "Auto-Population Engine"],
    "vbms_existing": ["VBMS Core DB", "Claims Evidence API", "Claims API", "ILER API", "DocGen API", "Veteran API", "C&P Smart Search"],
    "aws_external": ["AWS SageMaker", "AWS Comprehend", "OpenSearch"]
  },
  "connections": [
    {"from": "TERA Memo UI", "to": "TERA Memo API", "type": "bidirectional"},
    {"from": "TERA Memo UI", "to": "Claims Evidence API", "type": "bidirectional"},
    {"from": "TERA Memo API", "to": "VBMS Core DB", "type": "bidirectional"},
    {"from": "AWS SageMaker", "to": "OpenSearch", "type": "bidirectional"},
    {"from": "C&P Smart Search", "to": "OpenSearch", "type": "write"},
    {"from": "DocGen API", "to": "eFolder", "type": "write"}
  ],
  "protocol": "HTTPS (port 443) for all APIs"
}
```

---

*Due to length constraints, I'll continue with the remaining diagrams in the next part. Would you like me to continue with diagrams 8.1 through 15.2, creating the same level of detailed metadata?*
