# ThreatLens – Explainable Risk-Aware Hybrid Machine Learning for Network Intrusion Detection

ThreatLens is a hybrid machine learning-based Network Intrusion Detection System (NIDS) designed to identify malicious network traffic, assess potential threats, prioritize security alerts, and explain model predictions using Explainable AI.

The system combines supervised and unsupervised machine learning techniques to improve network threat detection and provides SHAP-based explanations to help security analysts understand the factors influencing attack predictions.

## Key Features

- **Hybrid Intrusion Detection:** Combines Random Forest and Isolation Forest.
- **Anomaly Detection:** Identifies unusual network traffic patterns.
- **Risk-Aware Alert Prioritization:** Assigns risk levels to detected threats.
- **Explainable AI:** Uses SHAP to explain Random Forest predictions.
- **Automated Detection Pipeline:** Processes network traffic and generates predictions.
- **Alert Management:** Stores attack alerts and supports investigation updates.
- **Real-Time Alert Events:** Uses Flask-SocketIO for real-time event communication.
- **Dashboard:** Provides a visual interface for monitoring detection results and investigating alerts.

## System Architecture

```text
              UNSW-NB15 Dataset
                      |
                      v
               Data Preprocessing
                      |
                      v
             Processed Network Features
                      |
             +--------+--------+
             |                 |
             v                 v
        Random Forest     Isolation Forest
        (Supervised)      (Unsupervised)
             |                 |
             v                 v
        Attack Probability  Anomaly Score
             |                 |
             +--------+--------+
                      |
                      v
               Hybrid Scoring
                      |
                      v
               Attack Detection
                      |
              +-------+-------+
              |               |
              v               v
         Risk Assessment   SHAP Explanation
              |               |
              +-------+-------+
                      |
                      v
               MongoDB Storage
                      |
                      v
              Security Dashboard
```

## Machine Learning Models

### 1. Random Forest

A supervised machine learning algorithm trained on labelled network traffic. It predicts the probability of traffic belonging to the attack class.

### 2. Isolation Forest

An unsupervised anomaly detection algorithm that identifies unusual observations in network traffic.

### 3. Hybrid Detection

The outputs of both models are combined using a weighted scoring approach.

**Hybrid Score Formula:**

Hybrid Score = (0.7 × RF Score) + (0.3 × Normalized Isolation Forest Score)

Configuration:
- Random Forest Weight: 0.7
- Isolation Forest Weight: 0.3
- Detection Threshold: 0.6

Traffic with a hybrid score greater than or equal to the configured threshold is classified as an attack.

## Explainable AI – SHAP

ThreatLens integrates SHAP (SHapley Additive exPlanations) using the Random Forest TreeExplainer.

It identifies the top features contributing to the Random Forest attack prediction.

The explanation includes:
- Feature name
- Feature value
- SHAP contribution value
- Direction of contribution towards or away from the attack prediction

This improves model transparency and helps security analysts understand why traffic was classified as suspicious.

**Note:** SHAP currently explains the Random Forest prediction, not the complete hybrid scoring decision.

## Dataset

This project uses the **UNSW-NB15 Network Intrusion Detection Dataset**.

The dataset includes normal network traffic and multiple attack categories, including:

- DoS
- Exploits
- Fuzzers
- Reconnaissance
- Backdoor
- Analysis
- Shellcode
- Worms
- Generic

## Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| Frontend | HTML, CSS, JavaScript |
| Backend | Flask |
| Database | MongoDB |
| Real-Time Communication | Flask-SocketIO |
| Supervised Learning | Random Forest |
| Unsupervised Learning | Isolation Forest |
| Explainable AI | SHAP |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Model Persistence | Joblib |
| Dataset | UNSW-NB15 |

## Project Structure

```text
hybrid-nids/
│
├── backend/
│   ├── app.py
│   ├── services/
│   │   └── ensemble_detector.py
│   └── requirements.txt
│
├── frontend/
│   └── dist/
│       ├── index.html
│       ├── app.js
│       └── style.css
│
├── models/
│   ├── supervised_rf.joblib
│   ├── unsupervised_iso.joblib
│   ├── preprocessor.joblib
│   ├── rf_metrics.json
│   └── iso_metrics.json
│
├── data/
│   └── unsw-nb15/
│
├── requirements.txt
└── README.md
```

*This structure describes the main project components; additional files may exist in the repository.*

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/health` | Checks backend and model status |
| POST | `/api/v1/detect/` | Analyses network traffic and returns a detection result |

## Installation and Setup

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd hybrid-nids
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure MongoDB

Set up MongoDB and configure the required connection settings in your project configuration or environment variables.

### 5. Run the backend

```bash
python -m backend.app
```

The backend runs at:

```text
http://127.0.0.1:5000
```

### 6. Check backend health

```text
http://127.0.0.1:5000/api/v1/health
```

## Project Objectives

1. Detect malicious network traffic using machine learning.
2. Combine supervised and unsupervised learning approaches.
3. Calculate hybrid detection scores for network traffic.
4. Prioritize security alerts based on risk.
5. Improve model transparency through SHAP explainability.
6. Provide a dashboard for security monitoring and investigation.

## Future Enhancements

- Live network packet capture and analysis.
- Deep learning-based intrusion detection.
- Model retraining for evolving attack patterns.
- Advanced alert correlation and threat intelligence.
- Improved false-positive reduction.
- More comprehensive model evaluation.

## Disclaimer

ThreatLens is an academic and research project developed for network intrusion detection experimentation. Its current implementation uses the UNSW-NB15 dataset and trained machine learning models. It is not a replacement for a production-grade enterprise security monitoring solution.

## Author

Developed as a final-year academic project.

**Project:** ThreatLens – Explainable Risk-Aware Hybrid Machine Learning for Network Intrusion Detection and Alert Prioritization
