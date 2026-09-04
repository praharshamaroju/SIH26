# AI-Powered MPLAD Fund Fraud & Anomaly Detection System

An AI-powered investigation system that automatically detects suspicious patterns and potential fraud in **MPLAD (Members of Parliament Local Area Development Scheme)** project and fund records.

Instead of manually checking thousands of project, vendor, and payment records, the system connects these records together to uncover suspicious relationships and patterns that are difficult to identify through traditional checks.

---

## 🚨 Problem

MPLAD funds are used for development projects within MPs' constituencies. However, identifying irregularities such as:

* Unusually inflated project or billing amounts
* Vendors repeatedly working across multiple MPs
* Suspicious concentration of projects
* Unusual spending near the end of a financial year
* Hidden relationships between vendors, MPs and projects

can be difficult when records are examined individually.

### Our Solution

We are building an intelligent system that **connects the records and automatically flags suspicious cases**, helping investigators focus their attention on the highest-risk transactions.

> **The key idea:** Fraud may not be visible in a single record — but it can become obvious when related records are connected.

---

# ✨ Key Features

## 1. 📄 Data Upload

Investigators can upload project, vendor and payment data in **CSV format**.

Example data:

```text
MP | Vendor | Project | Amount | Date | Location
```

The system processes the uploaded data automatically.

---

## 2. 🔍 Automated Detection Engine

The detection engine runs multiple checks on the uploaded data.

### Billing Amount Outliers

Identifies statistically unusual project/payment amounts.

For example:

> A project costing ₹48 lakh when similar projects in the same category usually cost ₹8–12 lakh.

---

### Vendor Collusion / Concentration

Identifies vendors appearing repeatedly across multiple MPs or projects.

For example:

> The same vendor receives projects from several MPs across different locations.

This becomes particularly useful when combined with other suspicious patterns.

---

### Financial Year-End Timing Clusters

Detects unusual concentrations of projects or payments near the end of a financial year.

For example:

> A large number of high-value projects are approved or paid within a short period immediately before the financial year closes.

---

## 3. ⚠️ Risk Scoring

Every suspicious case receives a **risk score** based on the detected indicators.

Example:

```text
Risk Score: 87/100

Indicators:
✓ Unusual billing amount
✓ Vendor appears across 5 MPs
✓ Payment occurred near financial year-end
```

Cases can then be ranked from **highest to lowest risk**, allowing investigators to prioritize their work.

---

## 4. 🕸️ Relationship Graph

### Our Main "Wow" Feature

The system creates an interactive relationship graph connecting:

```text
MP
 │
 ├── Project
 │      │
 │      └── Vendor
 │
 └── Vendor
        │
        ├── Project
        └── Other MP
```

This allows investigators to visually identify relationships that may not be obvious from a spreadsheet.

### Example

```text
MP A ─────┐
          │
          ▼
       Vendor X
          │
          ├──── Project 1
          ├──── Project 2
          ├──── Project 3
          │
MP B ─────┘
```

A vendor repeatedly appearing across multiple MPs and projects can become a potential investigation lead.

---

## 5. 🤖 Plain-Language AI Explanations

Every flagged case includes a simple explanation of **why it was flagged**.

Instead of showing only:

```text
Anomaly Score: 0.91
```

the system provides an explanation such as:

> **"This project was flagged because its payment amount is significantly higher than similar projects, and the same vendor has received projects from multiple MPs."**

This makes the system easier for investigators and non-technical users to understand.

---

## 6. ⚡ Live Rule Builder

### Bonus Feature

If time permits, investigators will be able to create a new detection rule directly from the dashboard.

Example:

```text
IF
Project Amount > ₹30,00,000
AND
Vendor appears under > 3 MPs

THEN
Flag as High Risk
```

The new rule can then be applied immediately to the uploaded dataset.

This demonstrates that the system is not limited to predefined detection patterns.

---

# 🔄 System Workflow

```text
                📄 CSV Upload
                     │
                     ▼
             🔍 Detection Engine
                     │
        ┌────────────┴────────────┐
        │                         │
        ▼                         ▼
 📊 Risk Scoring           🕸️ Relationship Graph
        │                         │
        └────────────┬────────────┘
                     │
                     ▼
             🖥️ Investigator
                Dashboard
                     │
                     ▼
       🤖 Plain-Language Explanation
                     │
                     ▼
          ⚡ Live Rule Builder
              (Bonus Feature)
```

---

# 🏗️ Architecture

```text
                         ┌──────────────────┐
                         │   CSV Dataset    │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │     Pandas       │
                         │ Data Processing  │
                         └────────┬─────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                    ▼                           ▼
          ┌──────────────────┐        ┌──────────────────┐
          │ Detection Engine │        │ Graph Engine     │
          │                  │        │                  │
          │ • Outliers       │        │ MP ↔ Vendor      │
          │ • Vendor checks  │        │ Vendor ↔ Project │
          │ • Timing checks  │        │ Project ↔ MP     │
          └────────┬─────────┘        └────────┬─────────┘
                   │                           │
                   └─────────────┬─────────────┘
                                 │
                                 ▼
                       ┌────────────────────┐
                       │   Risk Scoring     │
                       └─────────┬──────────┘
                                 │
                                 ▼
                       ┌────────────────────┐
                       │ Investigator       │
                       │ Dashboard          │
                       │                    │
                       │ • Ranked cases     │
                       │ • Graphs           │
                       │ • Explanations     │
                       └─────────┬──────────┘
                                 │
                                 ▼
                       ┌────────────────────┐
                       │   Gemini API       │
                       │ AI Explanations    │
                       └────────────────────┘
```

---

# 🛠️ Tech Stack

| Component              | Technology            | Purpose                              |
| ---------------------- | --------------------- | ------------------------------------ |
| Frontend + Application | **Streamlit**         | Interactive investigator dashboard   |
| Data Processing        | **Pandas**            | CSV processing and data manipulation |
| Numerical Analysis     | **NumPy**             | Statistical calculations             |
| Graph Analysis         | **NetworkX**          | Build relationship networks          |
| Graph Visualization    | **Streamlit-Agraph**  | Interactive relationship graph       |
| AI Explanations        | **Google Gemini API** | Generate plain-language explanations |
| Hosting                | **Render**            | Deploy the application               |
| Version Control        | **Git + GitHub**      | Collaboration and source control     |

---

# 📁 Project Structure

```text
mplad-fraud-detection/
│
├── app.py
├── detection.py
├── graph_engine.py
├── requirements.txt
├── README.md
├── .gitignore
│
├── data/
│   └── sample_data.csv
│
└── assets/
    └── screenshots/
```

### File Responsibilities

| File               | Purpose                                |
| ------------------ | -------------------------------------- |
| `app.py`           | Streamlit dashboard and user interface |
| `detection.py`     | Fraud/anomaly detection logic          |
| `graph_engine.py`  | Relationship graph generation          |
| `requirements.txt` | Python dependencies                    |
| `data/`            | Sample/demo datasets                   |
| `assets/`          | Screenshots and project assets         |

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd mplad-fraud-detection
```

## 2. Create a Virtual Environment

```bash
python -m venv venv
```

### Windows

```bash
venv\Scripts\activate
```

### macOS/Linux

```bash
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Configure Gemini API

Create a `.env` file or configure the API key through your deployment environment.

Example:

```text
GEMINI_API_KEY=your_api_key_here
```

**Never commit API keys or other secrets to GitHub.**

---

## 5. Run the Application

```bash
streamlit run app.py
```

The application will open in your browser.

---

# 📊 Demo Dataset

For demonstration purposes, the project can use a **synthetically generated MPLAD-style dataset** containing both normal and suspicious records.

The synthetic dataset can include patterns such as:

* Inflated project amounts
* Vendors shared across multiple MPs
* Multiple projects concentrated around financial year-end
* Repeated vendor-project relationships
* Normal records for comparison

This allows the detection engine and relationship graph to demonstrate the complete workflow without depending on external live datasets.

---

# 🎯 Example Investigation

Suppose the uploaded dataset contains:

```text
Vendor X → MP A → Project 1 → ₹8 Lakh
Vendor X → MP B → Project 2 → ₹42 Lakh
Vendor X → MP C → Project 3 → ₹39 Lakh
```

The system may identify:

```text
✓ Vendor appears across multiple MPs
✓ Project amounts are unusually high
✓ Multiple payments occur near financial year-end
```

The case receives a high risk score and appears near the top of the investigator dashboard.

The relationship graph then allows the investigator to visually explore the connections.

---

# 💡 Why This Approach?

Traditional checking often looks at records individually.

Our approach looks at the **relationships between records**.

```text
Traditional:

Project → Is this amount suspicious?


Our System:

MP
 ↓
Vendor
 ↓
Projects
 ↓
Payments
 ↓
Locations
 ↓
Timing
 ↓
Combined Risk
```

This makes it possible to detect **patterns and relationships that isolated record-level checking can miss.**

---

# 🏆 Key USP

### Explainable Relationship-Based Fraud Detection

Our system combines:

**Statistical anomaly detection + relationship analysis + risk scoring + explainable AI**

into a single investigator-focused dashboard.

The goal is not simply to say:

> ❌ "This record is suspicious."

It aims to show:

> 🟢 **"This case is suspicious because these specific records and relationships connect together."**

---

# 🔮 Future Scope

Potential future improvements include:

* Historical MPLAD data integration
* More advanced anomaly detection models
* Community/network-based fraud detection
* Geographic anomaly detection
* Duplicate/fake project detection
* Advanced vendor risk profiling
* Investigator case management
* Automated investigation reports
* Additional configurable detection rules
* Role-based access for investigators
* Integration with government data systems

---

# 👥 Team

Built as a team project for **Smart India Hackathon (SIH)**.

### Development Areas

* **Frontend & Dashboard:** Streamlit UI
* **Detection Engine:** Statistical and rule-based anomaly detection
* **Graph Engine:** MP–Vendor–Project relationship analysis
* **AI Layer:** Explainable natural-language insights
* **Integration:** Connecting detection, graph and dashboard components

---

# ⚠️ Disclaimer

This project is a **prototype for demonstration and research purposes**.

The generated risk scores and detected anomalies should be treated as **investigation leads, not proof of fraud**.

Final conclusions should always be made through appropriate human investigation and verification.

---

## ⭐ Vision

> **Turn thousands of disconnected records into actionable investigation leads.**

Instead of making investigators search for suspicious patterns manually, our system helps them **find, understand, and prioritize the cases that deserve attention.**
