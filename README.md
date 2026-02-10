# TERA - Toxic Exposure Risk Activity Memo Automation

## Overview

This repository contains documentation for the **TERA Memo Automation** system, a Department of Veterans Affairs platform that expedites TERA Memorandum processing using AI-powered automation.

## 📚 Documentation

Complete architecture documentation is available in the [`docs/`](./docs/) directory:

- **[Architecture Documentation](./docs/TERA_Architecture.md)** - Complete technical architecture extracted from PDF
- **[Documentation Overview](./docs/README.md)** - Quick reference and navigation guide
- **[Diagrams & Images](./docs/images/)** - All architectural diagrams and figures

## 🎯 What is TERA?

**TERA (Toxic Exposure Risk Activity) Memo Automation** enables Veteran Service Representatives (VSRs) to efficiently process claims related to toxic exposure, leveraging artificial intelligence to:

- Auto-populate TERA Memo forms from claims evidence
- Provide AI-generated recommendations with confidence scores
- Link directly to supporting evidence in documents
- Save approximately **675,000 annual labor hours**

## 🏗️ System Information

- **Platform**: Benefits Integrated Platform (BIP)
- **Component**: Compensation and Pension UI (CPUI)
- **VASI ID**: 3028
- **Status**: Deployed (January 26, 2025)

## 🔗 Related Repositories

- [bip-tera-memo-automation](https://github.com/department-of-veterans-affairs/bip-tera-memo-automation) - Backend automation
- [bip-cpui-tera-memo-ui](https://github.com/department-of-veterans-affairs/bip-cpui-tera-memo-ui) - User interface

## 🤖 AI Integration

The system uses:
- **AWS SageMaker** for ML model deployment
- **OpenSearch** for document indexing
- **OCR via C&P Smart Search** for document processing
- Daily batch processing for evidence analysis

## 📖 Key Features

✅ Modernized UI with 508 compliance  
✅ Auto-population of form questions  
✅ AI-powered evidence recommendations  
✅ Confidence scoring for decisions  
✅ Direct links to evidence documents  
✅ Performance monitoring dashboard  
✅ Feature flag management

## 🚀 Getting Started

Explore the documentation to understand:
1. System architecture and components
2. AI model processing workflow
3. User interface functionality
4. API integrations and data flows
5. Security and compliance requirements

Start with the [Documentation Overview](./docs/README.md) or dive into the [complete architecture](./docs/TERA_Architecture.md).

---

**For GitHub Copilot**: This repository contains comprehensive architecture documentation optimized for AI understanding, including diagrams, technical specifications, and integration details.