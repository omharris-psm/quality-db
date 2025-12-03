# How I Built the Quality Data Schema

A step-by-step guide documenting how this database schema visualization was created using AI-assisted development and deployed to GitHub Pages.

---

## Overview

**What I Built:** An interactive HTML document that visualizes a standardized database schema for end-to-end quality traceability across the product lifecycle.

**Tools Used:**
- Cursor IDE (AI-powered code editor)
- Claude AI (for schema design and code generation)
- GitHub (for hosting)
- GitHub Pages (for free web hosting)

**Time:** ~45 minutes from requirements to live deployment

**Live URL:** https://omharris-psm.github.io/quality-db/

---

## Step 1: Gather Requirements

I uploaded screenshots and documents showing the various quality data collection points across the product lifecycle.

### Files/Screenshots Provided:

| Source | Type | What It Showed |
|--------|------|----------------|
| Quality Lifecycle Matrix | Screenshot | Overview of quality checkpoints across phases (Innovate → Create → Make → Move → Marketplace) |
| RAMP Risk Criteria | Screenshot | Risk assessment framework with HIGH/MODERATE/LOW classifications, R-Values (Revolution/Renew/Refresh), risk owners (PRE/GLAM/PCC) |
| Issue Management Form | 6 Screenshots | Form fields for capturing quality issues including PO#, Issue Type, Factory Code, Defective Qty, Contact info, etc. |
| CFA Audit Template | PDF | T1 factory AQL inspection data template with fields like Internal Audit ID, Style Nbr, Colorway, Defect Codes, etc. |
| DC Audit Results | Excel (FY26 September) | Distribution center audit data with Plant, SAP PO#, Model Name, Season, Pass/Fail, Defect Codes 1-18 |
| Defect Codes Reference | Screenshot | Standardized defect codes organized by component (Upper: 1-8, Midsole: 9-15, Outsole: 16-20, Package/Label: 21-24) |

---

## Step 2: Describe What I Needed

I told the AI assistant:
> "Combine all of this information to create a DB schema that enables traceability and accountability for quality issues and performance end to end."

**Key requirements identified:**
- Cover all 4 quality phases: Create, Make, Move, Marketplace
- Include primary and foreign keys for relationships
- Make it viewable as an easy-to-interpret HTML table
- Enable traceability from product creation to consumer issues

---

## Step 3: AI Analyzed the Data

The AI identified the following data domains from my uploads:

### Phase: CREATE
- RAMP Risk Assessments
- Risk levels (HIGH, MODERATE, LOW)
- R-Values (REVOLUTION, RENEW, REFRESH)
- Risk owners (PRE, GLAM, PCC)
- Development scenarios
- Product/Material criteria

### Phase: MAKE (T1)
- Production Audits (AQL, FTT, HFPA)
- Internal Audit ID, PO Number
- Auditor information
- Sample size, Lot quantity
- Defect codes and counts
- Pass/Fail results
- Metal detection

### Phase: MOVE
- DC Audit results
- Plant codes
- Received quantity, Audit quantity
- Defect tracking (codes 1-24)
- Factory origin tracking

### Phase: MARKETPLACE
- Issue management
- Issue type/description
- Defective quantities
- Contact information
- File attachments
- Season impact (multi-select)
- Accountability (Request by: Nike/T1/T2)

---

## Step 4: AI Generated the Schema

The AI created 12 interconnected tables:

### Core Entities (4 tables)
| Table | Purpose |
|-------|---------|
| `Products` | Master product catalog (style, colorway, model) |
| `Factories` | T1/T2 manufacturing facilities |
| `PurchaseOrders` | Production order tracking |
| `Seasons` | Season reference data |

### Create Phase (1 table)
| Table | Purpose |
|-------|---------|
| `RAMP_Assessments` | Risk assessments during development |

### Make Phase (2 tables)
| Table | Purpose |
|-------|---------|
| `ProductionAudits` | T1 factory AQL/FTT/HFPA inspections |
| `AuditDefects` | Defects found during production audits |

### Move Phase (2 tables)
| Table | Purpose |
|-------|---------|
| `DC_Audits` | Distribution center audit results |
| `DC_AuditDefects` | Defects recorded at DC level |

### Marketplace Phase (4 tables)
| Table | Purpose |
|-------|---------|
| `Issues` | Quality issues from Geo/Marketplace |
| `IssueContacts` | Contact information for issues |
| `IssueSeasons` | Seasons impacted (multi-select support) |
| `IssueAttachments` | Files attached to issues |

### Reference Tables (3 tables)
| Table | Purpose |
|-------|---------|
| `DefectTypes` | Standardized defect codes |
| `Categories` | Product categories (FW/AP/EQ) |
| `IntakeFunctions` | Issue intake departments |

---

## Step 5: AI Generated the HTML Visualization

The AI created a single HTML file with:
- **Interactive filtering** - Click phase buttons to show/hide tables
- **Visual badges** for keys:
  - 🟡 PK = Primary Key
  - 🔵 FK = Foreign Key
  - 🔴 * = Required field
  - 🟢 IX = Indexed field
- **Dark theme** - Easy on the eyes, professional look
- **Responsive design** - Works on desktop and mobile
- **Entity Relationship Diagram** - Visual overview of table relationships
- **Statistics** - 12 tables, 4 phases, 95+ fields, 15 relationships

---

## Step 6: Test Locally

1. The AI saved the file to: `/Users/oharr6/quality-db-schema/index.html`

2. Opened it directly in the browser by double-clicking the file

3. Verified all tables displayed correctly and filtering worked

---

## Step 7: Upload to GitHub

### 7.1 Create Repository
1. Went to [github.com/new](https://github.com/new)
2. Named repository: `quality-db`
3. Clicked **Create repository**

### 7.2 Upload File
1. Clicked **"uploading an existing file"**
2. Dragged `index.html` from Finder into the upload area
3. Clicked **Commit changes**

### 7.3 Enable GitHub Pages
1. Went to **Settings** → **Pages**
2. Under Source, selected **Deploy from a branch**
3. Selected **main** branch and **/ (root)** folder
4. Clicked **Save**

---

## Step 8: Access the Live Schema

After ~1 minute, the schema became available at:
```
https://omharris-psm.github.io/quality-db/
```

---

## Files Created

```
quality-db-schema/
├── index.html           # Main schema visualization (uploaded to GitHub)
├── quality-schema.html  # Backup copy of the same file
└── HOW-I-MADE-THIS.md   # This documentation
```

### File Details:

| File | Size | Description |
|------|------|-------------|
| `index.html` | ~25 KB | Self-contained HTML with embedded CSS and JavaScript. No external dependencies. |

---

## Key Design Decisions

### 1. Single-File Architecture
Everything is in one HTML file (CSS and JS embedded) so:
- No build process needed
- Works offline once loaded
- Easy to share and deploy

### 2. Normalized Database Design
- Tables follow 3rd Normal Form (3NF)
- Foreign keys establish clear relationships
- Junction tables for many-to-many relationships (e.g., IssueSeasons)

### 3. Flexible Defect Tracking
- DefectTypes table supports multiple product categories
- Can accommodate Footwear, Apparel, and Equipment defect codes
- Region-specific codes supported (e.g., Japan-only defects)

### 4. End-to-End Traceability
- Products link to PurchaseOrders → Audits → Issues
- Factory accountability maintained through foreign keys
- Timeline preserved through date fields at each stage

---

## Schema Statistics

| Metric | Value |
|--------|-------|
| Total Tables | 12 |
| Quality Phases Covered | 4 (Create, Make, Move, Marketplace) |
| Total Fields | 95+ |
| Primary Keys | 12 |
| Foreign Key Relationships | 15 |
| Lookup/Reference Tables | 3 |

---

## How to Use the Schema

### For Database Developers:
1. Use the field names and data types to create actual database tables
2. Follow the FK relationships when building SQL scripts
3. Required fields (*) should have NOT NULL constraints

### For Data Analysts:
1. Understand how data flows from Create → Make → Move → Marketplace
2. Use the relationships to build JOINs for reporting
3. Defect codes link audits to issue management

### For Stakeholders:
1. Click phase buttons to focus on specific areas
2. Review the ERD for a high-level overview
3. Use as documentation for data governance

---

## Future Enhancements (Ideas)

- [ ] Generate SQL CREATE TABLE scripts
- [ ] Add sample data for demonstration
- [ ] Create data dictionary with extended definitions
- [ ] Add search/filter functionality for fields
- [ ] Export to different formats (PDF, SQL, JSON Schema)
- [ ] Add T2 Material Inspection tables
- [ ] Add VOC (Voice of Consumer) tables

---

## Related Projects

| Project | Description | URL |
|---------|-------------|-----|
| HFPA Inspector | Digital audit tool for T1 factory inspections | https://omharris-psm.github.io/hfpa-auditapp/ |

---

## Credits

**Source Documents:**
- Quality Lifecycle Matrix (FW/AP)
- RAMP Risk Criteria & Definitions (FY25 Q3)
- CFA Audit Template (Feb 2022)
- FY26 September DC Audit Results
- Issue Management Form (Apparel)

**Development:** AI-assisted using Cursor IDE + Claude

**Hosting:** GitHub Pages

---

*Document created: December 3, 2024*

