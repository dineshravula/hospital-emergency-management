# AI Agent-Based Smart Hospital Bed & Emergency Management System

A modular, rule-based multi-agent system for managing hospital bed occupancy, emergency triage, admissions, alerts, and operational reporting. Built with **Python 3.10+**, **Streamlit**, **SQLite**, **Plotly**, and **Pandas**.

## Project Structure

```
hospital_bed_system/
├── app.py                     # Main Streamlit dashboard UI
├── requirements.txt           # Python dependencies
├── README.md                  # This file
├── database/
│   ├── __init__.py
│   ├── db_manager.py          # SQLite connection, schemas, CRUD queries
│   └── seed_data.py           # Wards, beds, and historical admission seeding
└── agents/
    ├── __init__.py
    ├── orchestrator.py        # Central agent dispatcher
    ├── bed_monitor.py         # Bed Monitoring Agent
    ├── admission_agent.py     # Admission & Triage Agent
    ├── alert_agent.py         # Emergency Alerts & Notification Agent
    └── report_agent.py        # Reporting & CSV Export Agent
```

## Features

### 1. Bed Monitoring Agent (`agents/bed_monitor.py`)
- `get_bed_summary()` — total / occupied / available / maintenance / cleaning counts
- `get_ward_summary()` — per-ward occupancy with critical (>85%) flags
- `list_available_beds(ward, care_level)` — filter available beds by ward and care level
- `calculate_occupancy()` — detailed occupancy metrics with shortage warnings

### 2. Admission Assistance Agent (`agents/admission_agent.py`)
- `prepare_admission(patient_data, priority)` — triage validation and admission request creation
- `find_suitable_bed(care_level, department)` — match care requirements to available beds
- `approve_admission(admission_id, staff_name)` — human-in-the-loop staff approval before locking bed state

### 3. Emergency Alert Agent (`agents/alert_agent.py`)
- `check_thresholds()` — scan wards for >85% occupancy, suppress duplicate alerts
- `create_alert(severity, message)` — manually create alerts
- `list_active_alerts()` — list unacknowledged alerts
- `send_notification_mock(recipient, message)` — simulated staff notifications

### 4. Hospital Report Agent (`agents/report_agent.py`)
- `get_admission_counts()` — admission stats by status, priority, department, care level
- `build_daily_report()` — comprehensive operational report
- `export_report_csv()` — export report as downloadable CSV

### 5. Hospital AI Orchestrator (`agents/orchestrator.py`)
- Central dispatcher that routes actions to the appropriate agent tools
- Provides convenience methods for common operations

## Dashboard (`app.py`)

The Streamlit web interface includes:

| Page | Description |
|------|-------------|
| **Dashboard** | Key metrics, occupancy gauge, ward occupancy bar chart, active alerts |
| **Bed Management** | All beds, available beds (with filters), ward summary with charts |
| **Admissions** | New admission form with triage, admission list, human-in-the-loop approval |
| **Alerts** | Active alerts with acknowledge action, threshold check, manual alert creation |
| **Reports** | Admission statistics (pie/bar charts), ward details, CSV export |

## Installation & Usage

### 1. Navigate to the project directory

```bash
cd "c:\Users\admin\OneDrive\Desktop\The AI Agent-Based Smart Hospital Bed & Emergency Management System"
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the Streamlit dashboard

```bash
streamlit run app.py
```

The app will open at `http://localhost:8501`.

## Database

- **SQLite** file: `hospital_system.db` (auto-created in the project folder)
- **Schema**: `wards`, `beds`, `admissions`, `alerts`
- **Seeding**: On first run, default wards and beds are created, and up to 500 historical admissions are seeded from the provided CSV dataset (`hospital_bed_emergency_dataset_45000.csv`)

## Agent Responsibilities Summary

| Agent | Key Tools | Responsibility |
|-------|-----------|---------------|
| BedMonitorAgent | `get_bed_summary`, `get_ward_summary`, `list_available_beds`, `calculate_occupancy` | Track bed occupancy across General, ICU, Emergency, Pediatric wards; flag >85% |
| AdmissionAgent | `prepare_admission`, `find_suitable_bed`, `approve_admission` | Triage validation, bed matching, staff-confirmed admission |
| AlertAgent | `check_thresholds`, `create_alert`, `list_active_alerts`, `send_notification_mock` | Threshold monitoring, alert lifecycle, mock notifications |
| ReportAgent | `get_admission_counts`, `build_daily_report`, `export_report_csv` | Operational metrics and CSV export |
| Orchestrator | `route_action`, convenience wrappers | Central coordination of all agents |

## Requirements

- Python 3.10+
- Streamlit
- Pandas
- Plotly

Install all with: `pip install -r requirements.txt`

## License

MIT
