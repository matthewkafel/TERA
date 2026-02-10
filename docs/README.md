# TERA Architecture Documentation

This directory contains the architecture documentation for the **TERA Memo Automation** system, which has been extracted from the original PDF document and converted to GitHub Copilot-friendly markdown format.

## 📁 Contents

- **[TERA_Architecture.md](./TERA_Architecture.md)** - Complete architecture documentation extracted from PDF
- **[images/](./images/)** - All diagrams, flowcharts, and architectural figures from the documentation

## 🎯 Overview

**TERA (Toxic Exposure Risk Activity) Memo Automation** is a system that enables the Department of Veterans Affairs to expedite TERA Memorandum processing, providing significant time savings for Veteran Service Representatives (VSRs) and Veterans.

### Key Information

- **Status**: Final - updated for 8/18/25 submission
- **System**: Compensation and Pension UI (CPUI)
- **VASI ID**: 3028
- **Deployment Date**: January 26, 2025
- **Platform**: Benefits Integrated Platform (BIP)

### GitHub Repositories

- [bip-tera-memo-automation](https://github.com/department-of-veterans-affairs/bip-tera-memo-automation)
- [bip-cpui-tera-memo-ui](https://github.com/department-of-veterans-affairs/bip-cpui-tera-memo-ui)

## 🔑 Key Features

1. **Auto-Population**: Automatically populate TERA Memo questions using claims evidence data
2. **AI Integration**: Leverage AWS SageMaker for AI-powered recommendations
3. **508 Compliance**: Modernized UI following VBMS standards
4. **Evidence Linking**: Direct links to specific document locations for manual review
5. **Confidence Scoring**: AI-generated confidence scores for each recommendation
6. **Metrics Dashboard**: Performance monitoring and tracking

## 🏗️ Architecture Components

### Primary Components

- **React Front-End (MFE)**: Modern micro-frontend for TERA Memo UI
- **TERA Memo API**: Backend service for data processing
- **AWS SageMaker**: AI/ML model deployment and execution
- **OpenSearch Database**: Document indexing and search
- **VBMS Core Database**: Data persistence layer

### Key Integrations

- Claims Evidence API
- ILER API
- DocGen GenStore API
- C&P Smart Search (OCR)

## 💡 Use Case

**As a Veteran Service Representative (VSR)**, I need to process Veteran claims for Toxic Exposure Risk Activity (TERA) so that I can identify if a Veteran meets the criteria for TERA-related activities.

## 🤖 AI Capabilities

TERA Automation aligns with the VA AI Inventory under:
- **Human-Like Capabilities**: Solving tasks requiring human-like perception and cognition
- **Rights Impacting**: Decisions with legally significant effects on civil rights and access

### AI Model Processing

The system uses a **daily batch process**:
1. Documents in evidence folder converted from Image/PDF to text
2. Text files indexed in OpenSearch database
3. TERA Model runs nightly to analyze evidence
4. Recommendations written to VBMS Core database
5. UI queries database for auto-population

## 📊 Value Proposition

The TERA Memo Automation delivers:
- **675,000 annual labor hours** saved
- Enhanced efficiency for VSRs
- Improved Veteran claim processing time
- Standardized TERA Memorandum review process

## 🔐 Privacy & Compliance

- **PII**: Veterans name and file number
- **PHI**: Medical data references (not stored, only referenced)
- **508 Compliance**: Yes
- **eMASS ID**: 2049 (BIP Compensation and Pension User Interface)

## 📖 Documentation Structure

The main architecture document is organized by pages from the original PDF, with sections covering:

- System metadata and overview
- Key definitions and capabilities
- Use cases and user interface functionality
- Architecture viewpoints (OV-1, OV-2, SV-1, DIV-1, DIV-3)
- Operational and logical views
- Data models and system interfaces
- Deployment architecture
- Security and compliance

## 🖼️ Diagrams

All architectural diagrams have been extracted and are available in the [images/](./images/) directory, including:

- Capability taxonomies
- Use case diagrams
- System interaction flows
- Component architectures
- Data models
- Deployment diagrams

## 📝 For GitHub Copilot

This documentation has been optimized for GitHub Copilot ingestion, providing:
- Clear section headers and navigation
- Inline diagrams with descriptive alt text
- Structured metadata
- Complete technical details
- Direct links to code repositories

---

**Last Updated**: February 10, 2026  
**Source**: TERA Memo Architecture PDF (17 pages)
