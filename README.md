# 🔍 The Aadhaar Service Auditor

### UIDAI Data Hackathon 2026

**A data analytics tool that detects "Service Imbalances" in Aadhaar Seva Kendras to prevent child biometric obsolescence.**

---

## 📖 Table of Contents

- [Problem Statement](#problem-statement)
- [The Solution: Service Auditing](#the-solution-service-auditing)
- [How It Works](#how-it-works-the-logic)
  - [The Activity Proxy](#1-the-activity-proxy)
  - [The Conversion Audit](#2-the-conversion-audit)
  - [The Neglect Filter](#3-the-neglect-filter)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Key Insights](#key-insights-and-visuals)

---

## Problem Statement

**The Issue:** Children must update their biometrics at ages **5 and 15**. If these updates are missed, their Aadhaar becomes inactive, blocking access to school exams and government benefits.

**The Blind Spot:** Current reports look at "Total Transactions." A district might look "Active" because thousands of adults are updating addresses, but that same district might be completely neglecting mandatory child updates.

**The Goal:** To identify specific Pincodes where the **Service Imbalance** is high (High Adult Traffic vs. Low Child Compliance) so mobile update teams can be deployed surgically.

---

## The Solution: Service Auditing

This project is not just a dashboard; it is an **Auditor**. It scans dataset rows to flag "Neglected" centers.

- **Identifies High-Risk Zones:** Pinpoints locations where service infrastructure exists (the center is open) but child conversion is failing.
- **Optimizes Resources:** Helps the government stop sending mobile vans to random villages and start sending them to specific "Red Quadrant" pincodes.
- **Predictive Risk:** Flags areas where child Aadhaars are likely to become inactive soon due to low update rates.

---

## How It Works (The Logic)

We process anonymized UIDAI data through a Python pipeline to calculate a **"Child Conversion Rate"**.

### 1. The Activity Proxy

We first determine if a center is actually "Active" using adult transactions as a baseline:

> `Adult Activity Proxy` = `Demographic Updates` + (0.5 × `New Enrolments`)

---

### 2. The Conversion Audit

We compare the baseline activity against child mandatory updates:

> `Child Conversion Rate` = `Child Biometric Updates (5–17)` / `Adult Activity Proxy`

---

### 3. The "Neglect" Filter

A Pincode is flagged as **High Risk** only if:

1. Activity is **High** (Above Median)  
   → *The center is open and busy.*

2. Child Conversion is **Low** (Bottom 25%)  
   → *Children are not being served.*

---

## Tech Stack

- **Language:** Python  
- **Analysis:** Pandas, NumPy  
- **Visualization:** Matplotlib, Seaborn  
- **Environment:** Google Colab / Jupyter Notebooks  

---

## Project Structure

```text
├── data/                   # Folder for raw CSV files
│   ├── biometric/          # Biometric update datasets
│   ├── demographic/        # Demographic update datasets
│   └── enrolment/          # Enrolment datasets
├── notebooks/
│   └── Aadhaar_Service_Auditor.ipynb  # Main Analysis Notebook
├── output/                 # Generated graphs and reports
├── README.md               # Project documentation
└── requirements.txt        # Python dependencies
```

## How to Run

### Option 1: Google Colab (Recommended)

The code is optimized for Google Colab with Google Drive integration.

1. Upload the `Aadhaar_Service_Auditor.ipynb` file to your Google Drive.
2. Create a folder named `data` in your Drive and upload your CSV files there.
3. Open the notebook and run all cells.
* *Note: You will be asked to authenticate Google Drive access.*



### Option 2: Local Machine

1. Clone the repository:
```bash
git clone https://github.com/your-username/Aadhaar-Service-Auditor.git

```


2. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn

```


3. Update the `BASE_PATH` variable in the script to point to your local data folder.
4. Run the script:
```bash
python Aadhaar_Service_Auditor.py

```



---

## Key Insights and Visuals

The tool generates a **"Quadrant of Neglect"** analysis:

| Quadrant | Description | Action Required |
| --- | --- | --- |
| **High Activity, High Updates** | Healthy Center | No Action |
| **Low Activity, Low Updates** | Remote/Inactive Area | General Enrolment Drive |
| **High Activity, Low Updates** | **NEGLECTED ZONE** | **DEPLOY MOBILE VANS** |

<img width="1788" height="590" alt="image" src="https://github.com/user-attachments/assets/0f55a287-839d-4961-8802-5204228b9866" />
<br>
<br>
<img width="1032" height="585" alt="image" src="https://github.com/user-attachments/assets/867927f0-7313-4d2e-b569-2689ab3a1bb4" />

---

## Contributions

**Team Members:** Adil Km, Nasih Ameen, Adhil K and Najad
**Hackathon:** UIDAI Data Hackathon 2026

*This project is a submission for the UIDAI Hackathon and is intended for decision-support purposes only.*
