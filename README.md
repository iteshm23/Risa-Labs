# OncoInsight - AI-Assisted Clinical Dashboard for Oncology

[![Live Demo](https://img.shields.io/badge/Live%20Demo-View%20Dashboard-blue)](https://gvscyqvpdfrlm.ok.kimi.link)

A comprehensive clinical dashboard designed to help oncologists understand patient disease courses and make safer, faster decisions through intelligent data synthesis and AI-powered insights.

## 🎯 Product Goals

OncoInsight addresses the critical challenges in modern oncology care:

- **Fragmented Data**: Consolidates patient information from multiple sources into a unified view
- **Information Overload**: Surfaces what matters most at the point of care
- **Longitudinal Complexity**: Tracks disease progression, treatment responses, and biomarker trends over time
- **Decision Support**: Provides AI-generated insights that augment (not replace) clinical judgment

### Core Principles

1. **Clinical Context Awareness**: Understanding that oncology decisions depend on disease type, stage, prior treatments, and patient characteristics
2. **Longitudinal Reasoning**: Showing how patient data changes over time, not just static snapshots
3. **Data Synthesis**: Connecting related information across domains into a coherent narrative
4. **Decision Support (Not Decision-Making)**: Highlighting relevant considerations without presenting definitive clinical instructions
5. **Responsible AI Usage**: Using AI where interpretation, summarization, or pattern recognition adds value

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        OncoInsight Dashboard                     │
├─────────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌─────────────────────────────────────────┐  │
│  │ Patient List │  │           Main Content Area              │  │
│  │  (Sidebar)   │  │  ┌─────────┬─────────┬─────────┐       │  │
│  │              │  │  │Overview │Insights │ Alerts  │ ...   │  │
│  │ - Search     │  │  └─────────┴─────────┴─────────┘       │  │
│  │ - Filter     │  │                                         │  │
│  │ - Sort       │  │  ┌─────────────────────────────────┐   │  │
│  └──────────────┘  │  │      Tab Content Panel           │   │  │
│                    │  │  - Patient Overview              │   │  │
│                    │  │  - AI Insights                   │   │  │
│                    │  │  - Risk Flags                    │   │  │
│                    │  │  - Trend Charts                  │   │  │
│                    │  │  - Treatment Timeline            │   │  │
│                    │  └─────────────────────────────────┘   │  │
│                    └─────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Tech Stack

- **Frontend**: React 18 + TypeScript
- **Styling**: Tailwind CSS + shadcn/ui components
- **Charts**: Recharts for data visualization
- **Data**: CSV-based synthetic patient dataset
- **Build**: Vite for fast development and optimized production builds

## 📊 Data Model

### Patient Entity

The patient data model captures comprehensive clinical information:

| Category | Fields |
|----------|--------|
| **Demographics** | Patient_ID, Name, Age, Sex, Smoking_Status |
| **Clinical Status** | Performance_Status, Last_Encounter_Date |
| **Diagnosis** | Primary_Diagnosis, Histologic_Type, Diagnosis_Date, Initial_TNM_Stage, Current_TNM_Stage |
| **Staging** | Metastatic_Status, Metastatic_Sites, Recurrence_Status, Stage_Changes |
| **Pathology** | Pathology_Diagnosis_Text, Tumor_Grade, Biopsy_Site, Margin_Status, IHC_Markers |
| **Molecular** | EGFR, ALK, KRAS, BRAF, PDL1_Percent, TMB, MSI, ctDNA_Findings |
| **Imaging** | Latest_CT_Chest, Latest_PET_CT, RECIST, Radiology_Trend, New_Lesions |
| **Laboratory** | CEA, CA19-9, CBC, CMP, Abnormal_Labs |
| **Treatment** | Current_Line, Regimen, Treatment_Dates, Response, Prior_Therapies |
| **Comorbidities** | Diabetes, Hypertension, Heart_Disease, COPD_Asthma |

### Visit Entity (Longitudinal Data)

Tracks changes over time:
- Visit_Date, Visit_Number
- CEA, Hemoglobin
- Performance_Status, Radiology_Trend
- Treatment_Line, Response

## 🤖 AI Insights Engine

The AI insights engine generates clinical decision support through rule-based analysis:

### Insight Categories

1. **Clinical Insights**
   - Performance status decline detection
   - Comorbidity interaction warnings

2. **Molecular Insights**
   - Actionable mutation identification
   - Immunotherapy biomarker analysis (PD-L1, TMB, MSI)

3. **Treatment Insights**
   - Response assessment (CR/PR/SD/PD)
   - Treatment change recommendations

4. **Risk Insights**
   - Laboratory abnormality detection
   - CNS progression alerts

5. **Trend Insights**
   - Rising/falling tumor marker alerts
   - Early progression indicators

### Confidence Levels

Each insight is labeled with confidence:
- **High**: Based on clear clinical criteria
- **Medium**: Requires clinical correlation
- **Low**: Suggestive, needs verification

### Safety Guardrails

- All insights include evidence and suggested actions (not directives)
- Clear disclaimer: "Clinical judgment should always prevail"
- No automated treatment recommendations

## 🚨 Risk Flag System

Three-tier alert system for clinical abnormalities:

### Critical (Red)
- Severe anemia (Hb < 8)
- Severe thrombocytopenia (Plt < 50)
- Progressive disease with new lesions

### Warning (Amber)
- Moderate anemia (Hb 8-10)
- Elevated creatinine (> 1.5)
- Elevated LFTs (AST/ALT > 50)
- Reduced performance status (ECOG ≥ 2)

### Info (Blue)
- Active toxicities
- Non-urgent findings

## 📈 Visualization Features

### Longitudinal Trend Charts
- CEA (Carcinoembryonic Antigen) with normal reference line
- Hemoglobin with gender-specific normal ranges
- Treatment response tracking by visit

### Treatment Timeline
- Visual chronological display of:
  - Diagnosis
  - Surgeries
  - Radiation therapy
  - Systemic treatments by line

## 🔧 Key Tradeoffs and Assumptions

### Tradeoffs

1. **CSV vs. Database**: Chose CSV for simplicity in this demo; production would use a proper database
2. **Client-side Processing**: All AI logic runs client-side for this demo; production would use secure server-side processing
3. **Synthetic Data**: Used generated patient data to protect privacy

### Assumptions

1. **Data Completeness**: Dashboard handles missing data gracefully with null checks
2. **Clinical Validation**: AI insights are for demonstration; production requires clinical validation
3. **User Training**: Assumes clinicians understand RECIST, TNM staging, and molecular markers

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd oncoinsight

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

### Data Files

Place the following CSV files in `public/data/`:
- `oncology_patients.csv` - Main patient data
- `patient_visits.csv` - Longitudinal visit data

## 📁 Project Structure

```
├── public/
│   └── data/
│       ├── oncology_patients.csv
│       └── patient_visits.csv
├── src/
│   ├── components/
│   │   ├── AIInsightsPanel.tsx    # AI-generated insights display
│   │   ├── PatientList.tsx        # Patient roster with search/filter
│   │   ├── PatientOverview.tsx    # Clinical summary view
│   │   ├── RiskFlagsPanel.tsx     # Clinical alerts display
│   │   ├── TrendCharts.tsx        # Longitudinal data charts
│   │   └── TreatmentTimeline.tsx  # Treatment history timeline
│   ├── hooks/
│   │   └── usePatientData.ts      # Data fetching and AI logic
│   ├── types/
│   │   └── patient.ts             # TypeScript interfaces
│   ├── App.tsx                    # Main application
│   └── App.css                    # Custom styles
├── package.json
├── tailwind.config.js
├── tsconfig.json
└── vite.config.ts
```

## 📊 Dataset Summary

The synthetic dataset includes:
- **12 patients** across 4 cancer types
- **4 Cancer Types**: NSCLC, Colorectal, Breast, Pancreatic
- **All Stages**: Stage I through Stage IV
- **65+ visit records** for longitudinal tracking
- **Diverse profiles**: Various ages, comorbidities, treatment lines, and responses

### Cancer Type Distribution
- NSCLC: 4 patients
- Colorectal Cancer: 3 patients
- Pancreatic Cancer: 3 patients
- Breast Cancer: 2 patients

### Stage Distribution
- Stage IV (Metastatic): 6 patients
- Stage III: 3 patients
- Stage II: 2 patients
- Stage I: 1 patient

## 🔮 Future Enhancements

With more time, the following improvements would be valuable:

1. **Real-time Data Integration**: Connect to EHR systems via HL7/FHIR
2. **Advanced AI Models**: Implement NLP for pathology report parsing
3. **Predictive Analytics**: Survival prediction models, treatment response prediction
4. **Collaboration Features**: Multi-provider note sharing, tumor board integration
5. **Mobile App**: Tablet-optimized interface for bedside rounds
6. **Export Functionality**: PDF summary generation for patients/referrals
7. **Clinical Trial Matching**: Automated trial eligibility screening
8. **Genomic Visualization**: Interactive mutation maps, pathway analysis

## 📄 License

This project is for educational and demonstration purposes.

## 🙏 Acknowledgments

Built as part of the RISA Labs Technical APM Assignment.

---

**Disclaimer**: OncoInsight is a demonstration project. It is not intended for actual clinical use without proper validation, regulatory approval, and clinical oversight.
