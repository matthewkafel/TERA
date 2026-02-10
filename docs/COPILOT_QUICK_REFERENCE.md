# TERA Architecture Quick Reference

> **For GitHub Copilot and AI Assistants**

This document provides a quick reference to help AI systems understand the TERA Memo Automation architecture.

## System Summary

**TERA Memo Automation** is an AI-powered system for the Department of Veterans Affairs that automates the processing of Toxic Exposure Risk Activity (TERA) memorandums.

### Core Technologies
- **Frontend**: React Micro Frontend (MFE)
- **Backend**: Node.js/Java APIs
- **AI/ML**: AWS SageMaker with AWS Comprehend
- **Database**: Oracle DB (VBMS Core)
- **Search**: OpenSearch for document indexing
- **Platform**: Benefits Integrated Platform (BIP)

### Key Components

```
┌─────────────────┐
│   TERA Memo UI  │ (React MFE)
└────────┬────────┘
         │
         ├──> TERA Memo API
         ├──> Claims Evidence API
         └──> ILER API
              │
              ├──> VBMS Core DB (Oracle)
              └──> OpenSearch (Evidence Index)
                   │
                   └──> AWS SageMaker (AI Model)
```

## Daily Processing Workflow

1. **Document Ingestion**: Evidence documents added to eFolder
2. **OCR Processing**: Documents converted from PDF/Image to text via C&P Smart Search
3. **Indexing**: Text files indexed in OpenSearch database
4. **AI Analysis**: TERA Model (AWS SageMaker) analyzes evidence
5. **Recommendations**: Model outputs written to VBMS Core database
6. **UI Display**: TERA Memo UI queries database for auto-population

## Key Questions the System Answers

The TERA Memo form has 6 main questions that the AI helps answer:

1. **Question 1**: Evidence of TERA participation based on claim evidence
2. **Question 3**: Specific toxic exposure identified
3. **Question 4**: Location and timeframe of exposure
4. **Question 6**: Supporting documentation in claim file

For each question, the system provides:
- ✅ Yes/No recommendation
- 📊 Confidence score (0-100%)
- 📎 Links to specific evidence document locations
- 📝 Supporting text/rationale

## AI Model Details

### Input Sources
- Veteran's Claim Evidence documents (via OCR)
- ILER IES record data
- PACT Act Standard Operating Procedures
- M21-1 Adjudication Procedures Manual

### Processing
- Algorithms analyze and interpret input data
- Leverage AWS SageMaker via ML-MATS Platform
- Apply PACT Act SOP and M21-1 eligibility requirements

### Output
- "Yes" determination for applicable questions
- Open-text field responses with supporting details
- Document references with confidence scores

## API Endpoints (Conceptual)

```
GET  /api/tera-memo/:claimId           # Get TERA memo data
POST /api/tera-memo/:claimId/populate  # Trigger auto-population
GET  /api/tera-memo/:claimId/evidence  # Get evidence links
POST /api/tera-memo/:claimId/submit    # Submit completed memo
GET  /api/metrics/tera-memo            # Get performance metrics
```

## Data Model (Simplified)

```javascript
{
  teraMemo: {
    claimId: string,
    veteranFileNumber: string,
    questions: [
      {
        questionId: number,
        answer: "yes" | "no" | "unsure",
        confidenceScore: number,
        supportingText: string,
        evidenceLinks: [
          {
            documentId: string,
            pageNumber: number,
            location: string
          }
        ],
        autoPopulated: boolean,
        manuallyReviewed: boolean
      }
    ],
    status: "draft" | "completed" | "submitted",
    timestamps: {...}
  }
}
```

## Security & Compliance

- **PII Protection**: Veterans name and file number
- **PHI Handling**: Medical data references (not stored directly)
- **508 Compliance**: Full accessibility support
- **Authentication**: VBMS authentication required
- **Authorization**: Role-based access (VSR permissions)

## Performance Metrics

- **Annual Labor Hours Saved**: ~675,000 hours
- **Monthly AWS Cost**: ~$7,000
- **Users**: ~30,000 potential, ~5,000 daily throughput
- **Processing Time**: Batch runs nightly

## Integration Points

1. **VBMS Core**: Data persistence and retrieval
2. **Claims Evidence API**: Evidence document access
3. **ILER API**: Individual Longitudinal Exposure Record
4. **DocGen GenStore**: Document generation and storage
5. **C&P Smart Search**: OCR and document processing
6. **AWS SageMaker**: ML model inference
7. **OpenSearch**: Document search and retrieval

## Feature Flags

The system supports feature flags for:
- ✅ Legacy vs Modernized forms
- ✅ Auto-Population button enable/disable
- ✅ Metrics gathering
- ✅ A/B testing capabilities

## User Workflow

1. VSR opens VBMS Veteran Profile
2. Selects "Upload Document" → "TERA Memo"
3. TERA Memo UI loads with Veteran info pre-populated
4. VSR clicks "Auto-Populate" button
5. System displays AI recommendations with confidence scores
6. VSR reviews evidence links and validates answers
7. VSR certifies manual review (checkbox)
8. VSR submits completed TERA Memo
9. Document uploaded to Claim Evidence

## Error Handling

- Low confidence scores trigger manual review requirement
- Missing evidence prevents auto-population
- OCR failures handled gracefully
- Fallback to manual entry always available

## Monitoring & Observability

- Performance dashboard for model accuracy
- Metrics on auto-population usage rates
- Tracking of manual overrides
- Confidence score distribution analysis
- Processing time monitoring

---

For detailed architecture, see [TERA_Architecture.md](./TERA_Architecture.md)
