# 🌐 Automated Threat Intelligence Dashboard

## 1. Project Overview
This project is an automated Cyber Threat Intelligence (TI) platform that aggregates, enriches, and visualizes OSINT (Open-Source Intelligence) indicators of compromise (IOCs) to provide defenders with real-time, actionable insights.

## 2. Technical Stack
* **Language:** Python 3.x
* **Libraries:** `requests`, `pandas`, `elasticsearch` (or Splunk SDK)
* **Data Storage/Visualization:** Elasticsearch + Kibana (ELK Stack)
* **Threat Feeds (APIs):** AlienVault OTX, VirusTotal, AbuseIPDB, Shodan (optional)
* **Automation:** Linux Cron Job / Python `schedule` library

## 3. Key Features & Deliverables
* **Multi-Source Aggregation:** Combines data from disparate TI sources into a single unified schema.
* **Data Enrichment:** Adds **Geo-location (Latitude/Longitude)** and **Autonomous System Number (ASN)** data to all IP IOCs.
* **Real-Time Visualization:** Kibana Dashboard displaying:
    * Global heat map of malicious IP origins.
    * Top 10 observed malware families.
    * IOC type and severity distribution.
* **Actionable Output:** Generates a daily `firewall_blocklist.txt` based on the highest-reputation malicious IPs.

## 4. Architecture Flow
1.  **Extract:** Python script calls external APIs to pull raw IOCs.
2.  **Transform:** Python normalizes the data, calculates a composite reputation score, and performs Geo-location lookup.
3.  **Load:** Python pushes enriched JSON data to the dedicated Elasticsearch index.
4.  **Visualize:** Kibana renders the TI Dashboard.
5.  **Output:** A separate script exports top malicious IPs to a TXT file for defensive integration.

## 5. Setup and Execution
1.  **Clone Repository:** `git clone [Your-Repo-Link]`
2.  **Install Dependencies:** `pip install -r requirements.txt`
3.  **Configure:** Update `config.ini` or `.env` file with all required API keys (ensure these keys are **NEVER** committed to Git).
4.  **Schedule:** Set up a daily cron job to run the main ingestion script: `0 4 * * * /usr/bin/python3 /path/to/ingest_script.py`
