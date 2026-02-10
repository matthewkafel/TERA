# TERA Glossary and Index

> **For GitHub Copilot**: Key terms, acronyms, and concepts in TERA Memo Automation

## Acronyms

| Acronym | Full Name | Description |
|---------|-----------|-------------|
| **TERA** | Toxic Exposure Risk Activity | Activities or circumstances that exposed Veterans to toxic substances |
| **VSR** | Veteran Service Representative | VA employee who processes Veteran claims |
| **VBMS** | Veterans Benefits Management System | VA's system for managing benefits claims |
| **BIP** | Benefits Integrated Platform | VA's platform-as-a-service infrastructure |
| **CPUI** | Compensation and Pension UI | User interface component for C&P processing |
| **MFE** | Micro Frontend | Modular frontend architecture component |
| **OCR** | Optical Character Recognition | Technology to extract text from images/PDFs |
| **ILER** | Individual Longitudinal Exposure Record | VA record of Veteran's exposure history |
| **PACT Act** | Promise to Address Comprehensive Toxics Act | 2022 law expanding VA benefits for toxic exposure |
| **M21-1** | M21-1 Adjudication Procedures Manual | VA's claims processing manual |
| **SOP** | Standard Operating Procedure | Documented process for operations |
| **eFolder** | Electronic Folder | Digital repository of Veteran's claim evidence |
| **PII** | Personally Identifiable Information | Data that identifies individuals |
| **PHI** | Protected Health Information | Medical information protected by HIPAA |
| **eMASS** | Enterprise Mission Assurance Support Service | VA's security compliance system |
| **VASI** | VA Service Inventory | Registry of VA systems and services |
| **MSR** | Mission Support Request | VA's project tracking system |
| **BIH** | Benefits Integration Hub | Integration layer for VA systems |
| **AI** | Artificial Intelligence | Machine learning and automated decision systems |
| **ML** | Machine Learning | Subset of AI focused on learning from data |

## Key Concepts

### TERA Memorandum
A form completed by VSRs to document a Veteran's toxic exposure risk activities. The form determines if exposure triggers eligibility for VA medical examinations and benefits under 38 U.S.C. § 1168.

### Auto-Population
AI-powered feature that automatically fills TERA Memo form questions by analyzing evidence in the Veteran's claim file using machine learning models.

### Confidence Score
A percentage (0-100%) indicating the AI model's certainty in its recommendation. Higher scores indicate stronger evidence support.

### Evidence Links
Direct hyperlinks to specific locations in documents (page number, highlighted text) that support AI recommendations, enabling quick manual review.

### Daily Batch Process
Nightly automated workflow that:
1. Converts new documents to text via OCR
2. Indexes text in OpenSearch
3. Runs AI models to generate recommendations
4. Stores results in VBMS database

### Feature Flags
Configuration switches that enable/disable functionality without code changes:
- Legacy vs Modernized form
- Auto-population capability
- Individual question auto-population
- Metrics collection

## System Components

### Frontend
- **TERA Memo UI**: React-based micro frontend
- **Annotator Viewer**: Enhanced document viewer with highlighting

### Backend APIs
- **TERA Memo API**: Primary service for TERA operations
- **Claims Evidence (CE) API**: Document and evidence access
- **Claims API**: Veteran claim data
- **ILER API**: Exposure record data
- **DocGen Genstore API**: PDF generation and storage
- **Veteran API**: Veteran profile information

### Data Layer
- **VBMS Core Database**: Oracle database for persistence
- **OpenSearch**: Document indexing and full-text search
- **OCR_TEXTRACT_DATA**: Table storing AI recommendations
- **TERAMEMOUPLOADMETRICS**: Metrics tracking table

### AI/ML Platform
- **AWS SageMaker**: Model training and deployment
- **AWS Comprehend**: Natural language processing
- **ML-MATS Platform**: VA's ML model management
- **C&P Smart Search**: OCR and document processing

## TERA Form Questions

### Question 1
Evidence of TERA participation based on claim evidence
- **Auto-populated**: Yes
- **Confidence scoring**: Yes

### Question 2A
Service in location where toxic exposure is conceded
- **Auto-populated**: Partial (Yes for certain conditions)

### Question 3
Specific toxic exposure identified
- **Auto-populated**: Yes
- **Confidence scoring**: Yes

### Question 4
Location and timeframe of exposure
- **Auto-populated**: Yes
- **Confidence scoring**: Yes

### Question 5
Other deployment-related exposure
- **Auto-populated**: No (manual entry)

### Question 6
Non-deployment related exposure
- **Auto-populated**: Yes
- **Confidence scoring**: Yes

### Conclusion
Final determination if TERA triggers examination/opinion requirement

## Data Sources

### Input Data
- Veteran's claim evidence documents
- ILER exposure records
- Service records (DD214, etc.)
- Medical records
- Post-deployment health assessments

### Reference Data
- PACT Act Standard Operating Procedures
- M21-1 Adjudication Manual
- 38 C.F.R. § 3.320 (locations)
- 38 U.S.C. § 1168 (TERA statute)

## Architecture Views

### OV-1 (Operational Viewpoint)
High-level operational concept diagram showing:
- Main actors (VSR, systems)
- Data flows
- System interactions

### OV-2 (Operational Resource Flow)
Resource exchange between operational performers:
- What data flows where
- Between which systems

### SV-1 (Systems Interface Description)
System composition and interfaces:
- Component relationships
- Service dependencies
- API contracts

### DIV-1 (Conceptual Data Model)
Logical data structures and relationships

### DIV-3 (Physical Data Model)
Physical database schema and tables

### SvcV-1 (Services Context)
Service composition showing:
- APIs and their operations
- Service dependencies
- Protocols and ports

## Security & Compliance

### Authentication
- VBMS login required
- Role-based access control
- Permission validation per action

### Data Protection
- PII/PHI handling procedures
- Encryption at rest and in transit
- Audit logging

### Compliance Standards
- **508 Compliance**: Accessibility standards
- **FISMA**: Federal security requirements
- **HIPAA**: Health data protection
- **Authority to Operate (ATO)**: Security authorization

### Security Scanning
- **CodeQL**: Static code analysis
- **PrismaCloud**: Container and cloud security
- **eMASS**: Continuous compliance monitoring

## Performance Metrics

### Business Metrics
- Annual labor hours saved: ~675,000
- Auto-population usage rate
- Manual override frequency
- Time per TERA Memo completion

### Technical Metrics
- Model inference latency
- API response times
- OCR processing throughput
- Batch job completion time

### Quality Metrics
- Model accuracy/precision
- Confidence score distribution
- False positive/negative rates
- User satisfaction scores

## Common Workflows

### VSR Processing Workflow
1. Open Veteran profile in VBMS
2. Select "Upload Document" → "TERA Memo"
3. Review pre-populated Veteran info
4. Click "Auto-Populate" button
5. Review AI recommendations and confidence scores
6. Click evidence links for manual validation
7. Accept/modify recommendations
8. Certify manual review (checkbox)
9. Preview generated PDF
10. Submit to claim evidence

### Nightly Batch Workflow
1. Identify new documents in eFolders
2. Run OCR on PDF/image documents
3. Extract and normalize text
4. Index in OpenSearch
5. Execute TERA AI model
6. Store recommendations in database
7. Update monitoring dashboard
8. Send alerts for failures

## Error Handling

### Low Confidence Scenarios
- Threshold typically 70-80%
- Requires mandatory manual review
- May indicate insufficient evidence

### Missing Data
- Question not auto-populated
- Manual entry required
- Explanation provided to user

### System Failures
- Graceful degradation to manual form
- Feature flags disable auto-population
- User notifications
- Fallback procedures

## Monitoring & Observability

### Dashboards
- ML-MATS Platform dashboard
- Model performance metrics
- System health indicators
- Usage analytics

### Alerts
- Model accuracy degradation
- API latency thresholds
- Batch job failures
- Security incidents

### Logs
- Application logs
- Audit logs
- API access logs
- Error tracking

## Related Systems

### Upstream Dependencies
- VBMS Core
- Claims Evidence system
- ILER system
- AWS services

### Downstream Consumers
- VSR workstations
- Reporting systems
- Analytics platforms
- Audit systems

---

**Last Updated**: February 10, 2026  
**Purpose**: Comprehensive reference for GitHub Copilot and AI assistants
