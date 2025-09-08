---
title: "Philippine Civil Code Will Validation System"
excerpt: "AI-powered legal document analysis tool for validating wills according to Philippine Civil Code requirements"
date: 2024-12-01
tags: [python, ai, legal-tech, flask, pdf-processing, openai]
github: "https://github.com/clsandoval/succession-tool"
layout: single
author_profile: true
---

## Project Overview

The Philippine Civil Code Will Validation System is a comprehensive legal technology solution that validates testamentary documents according to Philippine Civil Code requirements. The system combines PDF extraction, AI-powered analysis, and legal rule validation to provide detailed assessments of will validity, compulsory heirship calculations, and intestate succession scenarios.

### Key Capabilities
- **📄 PDF Processing**: Automated extraction of will content from PDF documents with fallback to image-based OCR
- **⚖️ Legal Validation**: Compliance checking against 47+ Philippine Civil Code articles
- **👥 Witness Analysis**: Verification of witness requirements and conflict detection
- **💰 Compulsory Heirship**: Calculation of legitime shares and free portions
- **🧠 AI-Powered Analysis**: OpenAI GPT-4 integration for complex legal reasoning
- **🔍 Comprehensive Testing**: Extensive test suite with real example wills

## Technical Architecture

### System Components

```
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│   PDF Documents  │    │   Family Tree    │    │  Estate Assets   │
│                  │    │   Information    │    │   Information    │
└─────────┬────────┘    └─────────┬────────┘    └─────────┬────────┘
          │                       │                       │
          ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│                    WILL VALIDATOR CORE                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │ PDF Extraction  │  │ Content Parser  │  │ Legal Analyzer  │ │
│  │   Utilities     │  │                 │  │                 │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │ Civil Code      │  │ AI Integration  │  │ Validation      │ │
│  │ Repository      │  │ (OpenAI)        │  │ Engine          │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Tech Stack
- **Backend**: Flask REST API with Gunicorn
- **AI/ML**: OpenAI GPT-4 for legal reasoning
- **PDF Processing**: PyPDF2 + PyMuPDF for text/image extraction
- **Data Validation**: Pydantic v2 models
- **Testing**: Custom comprehensive test suite
- **Deployment**: Docker + Docker Compose, Cloud-ready

### Legal Framework Implementation

The system implements specific Philippine Civil Code provisions:

#### Formal Validity (Articles 804-810)
- Testator signature requirements (Article 805)
- 3-witness minimum requirement (Article 806) 
- Witness competency assessment (Articles 807-808)
- Proper execution verification

#### Compulsory Heirship (Articles 887-900)
- Heir identification and classification
- Legitime percentage calculations by family scenario
- Preterition detection (Article 854)
- Free portion determination

#### Intestate Succession (Articles 960-1014)
- Implementation of the "25 succession combinations"
- Recursive disqualification handling with representation
- Collateral distribution with blood-type weighting
- State escheat scenarios

## Core Features

### 1. Comprehensive Will Analysis

```python
from will_validator import WillValidator
from models.estate import EstatePlanningPayload

# Initialize validator from estate payload
validator = WillValidator.from_estate_payload(payload)

# Perform comprehensive validation
validation_report = validator.validate_estate_payload(
    payload=payload, 
    pdf_path="path/to/will.pdf"
)

# Access detailed results
print(f"Overall Validity: {validation_report['overall_validity']}")
print(f"Recommendations: {validation_report['recommendations']}")
print(f"Article Citations: {validation_report['article_citations']}")
```

### 2. Intestate Succession Calculator

The system includes a sophisticated intestate calculator implementing the 25 succession combinations:

```python
from intestate_calculator import calculate_intestate_shares, Heir
from decimal import Decimal

# Define heirs
heirs = [
    Heir(name="Ana", relation="legitimate_child"),
    Heir(name="Ben", relation="legitimate_child"), 
    Heir(name="Iggy", relation="illegitimate_child"),
    Heir(name="Dana", relation="spouse")
]

# Calculate shares
shares, combination = calculate_intestate_shares(Decimal("10000000"), heirs)
print(f"Applied: {combination.description}")
```

### 3. Advanced PDF Processing

Dual-method PDF content extraction with intelligent fallback:

```python
def extract_items(pdf_path: str) -> Dict[str, Any]:
    # Primary: Text extraction with PyPDF2
    will_text = extract_text_from_pdf(pdf_path)
    
    # Fallback: Image-based OCR with PyMuPDF + OpenAI Vision
    if insufficient_text(will_text):
        will_text = extract_text_from_images(pdf_path)
    
    # AI-powered content analysis
    return analyze_will_with_openai(will_text)
```

## Testing Framework

Comprehensive testing across multiple scenarios:

### Test Categories
1. **Extraction Integration**: PDF processing pipeline validation
2. **Witness Validation**: Civil Code Articles 805-808 compliance
3. **Family Scenarios**: 5 different compulsory heirship compositions
4. **PDF Integration**: End-to-end document processing workflow

### Test Coverage Examples

```python
def test_family_scenarios():
    """Tests 5 family compositions with detailed validation"""
    scenarios = [
        "spouse_and_legitimate_children",
        "children_only_no_spouse", 
        "spouse_and_parents_no_children",
        "mixed_legitimate_illegitimate_children",
        "parents_only_no_spouse_no_children"
    ]
    # Detailed assertion logic for each scenario
```

## Real-World Impact

### Legal Accuracy
- Implements 47+ Philippine Civil Code articles with exact text storage
- AI-powered legal reasoning for complex edge cases
- Extensive validation against real will documents

### Practical Applications
- Legal professionals can validate will compliance
- Estate planners can calculate compulsory heirship
- Families can understand intestate succession rights
- Academic researchers can study succession patterns

### Performance Metrics
- Processing time: ~30-60 seconds per will
- Accuracy: Validated against legal expert review
- Coverage: Handles 25 intestate succession combinations
- Scalability: Docker-deployed, cloud-ready architecture

## Deployment

### Production-Ready Features
- **Docker containerization** with health checks
- **Flask REST API** with comprehensive endpoints
- **Environment configuration** for different deployment targets
- **CORS support** for web application integration
- **Error handling** and detailed logging

### API Endpoints
- `POST /validate-will` - Comprehensive will validation
- `POST /process-intestate` - Intestate succession calculation  
- `POST /create-checkout-session` - Payment processing integration
- `GET /health` - Health monitoring

### Quick Start
```bash
# Clone and run with Docker
docker-compose up --build

# Or deploy to cloud platforms
gcloud run deploy succession-tool --image gcr.io/PROJECT/succession-tool
```

## Technical Challenges & Solutions

### Challenge 1: PDF Text Extraction Reliability
**Problem**: Legal PDFs often have complex formatting, scanned images, or poor text extraction quality.

**Solution**: Implemented dual-extraction pipeline:
1. Primary: PyPDF2 text extraction 
2. Fallback: PyMuPDF image conversion + OpenAI Vision API OCR
3. Quality validation with automatic method selection

### Challenge 2: Complex Legal Rule Implementation  
**Problem**: Philippine Civil Code has intricate succession rules with many edge cases.

**Solution**: 
- Local file storage of 47+ Civil Code articles for exact reference
- AI integration for nuanced legal interpretation
- Comprehensive test suite with real-world scenarios

### Challenge 3: Compulsory Heirship Calculations
**Problem**: Complex mathematical calculations based on family composition and legal percentages.

**Solution**: Systematic algorithm implementing the "25 succession combinations" with recursive disqualification handling and representation rights.

## Future Enhancements

### Planned Features
- **Multi-language support** for regional Philippine languages
- **Blockchain integration** for document verification
- **Machine learning models** for will classification
- **Mobile application** for field validation

### Research Applications
- **Legal analytics** on succession patterns
- **Comparative studies** across different legal systems  
- **AI/Law intersection** research platform

## Code Quality & Standards

### Development Practices
- **Type safety** with Pydantic v2 models
- **Comprehensive testing** with detailed assertions
- **Error handling** with graceful degradation
- **Documentation** with inline code examples
- **Security** considerations for sensitive legal data

### Code Organization
```
succession-tool/
├── will_validator.py      # Core validation engine
├── intestate_calculator.py # Succession calculations  
├── articles/             # Civil Code article storage
├── models/               # Pydantic data models
├── utils/                # PDF processing utilities
├── tests/                # Comprehensive test suite
└── main.py               # Flask API application
```

This project demonstrates the intersection of legal expertise, software engineering, and AI technology to solve real-world problems in the Philippine legal system. The comprehensive approach to testing, documentation, and deployment makes it a robust foundation for legal technology applications.