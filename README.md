# SYSTEMS-INIT--PROJECT-SENTINEL-FASTAPI-PROXY-

# 🛡️ Sentinel: Zero-Trust Enterprise AI Security Proxy

![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Security](https://img.shields.io/badge/Security-Zero%20Trust-red?style=for-the-badge)

## 📌 The Core Problem
Enterprise adoption of Generative AI is heavily bottlenecked by **Data Loss Prevention (DLP)** and compliance risks (GDPR, DPDP). When employees query LLMs, they risk exposing Personally Identifiable Information (PII) or falling victim to Prompt Injection attacks. 

## 🚀 The Solution
**Sentinel** is a lightweight, containerized microservice that acts as a Zero-Trust firewall between users and external/local LLMs. 

Operating entirely offline, Sentinel intercepts network traffic and utilizes local NLP engines to enforce a "Two-Way Mirror" security protocol: scrubbing inbound prompts of sensitive data (like Indian PAN/Aadhar and standard PII) and filtering outbound LLM hallucinations to guarantee zero data leakage.

## ⚙️ Enterprise Architecture
* **Inbound DLP Engine:** Scans and redacts PII using Microsoft Presidio before the prompt touches the LLM.
* **Custom Entity Recognizers:** Implements regex-based detection for localized IDs (Indian PAN and Aadhar).
* **Jailbreak Defender:** Heuristic scanning blocks malicious "ignore previous instructions" prompt injection attempts with a 403 Forbidden response.
* **Outbound Response Filtering:** Scans the generated LLM output to catch and redact hallucinated PII.
* **Compliance Audit Trail:** Silently logs all security events (intercepts, redactions, and blocks) to a JSON-structured `security_audit.log` for regulatory reporting.
* **Local Edge Processing:** Designed to seamlessly hand off sanitized prompts to local, quantized models via Ollama (e.g., Qwen) for 100% offline intelligence.

## 🛠️ Tech Stack
* **Backend:** FastAPI, Uvicorn (Asynchronous routing)
* **NLP & Security:** Microsoft Presidio, spaCy (`en_core_web_sm`)
* **Deployment:** Docker (Production-ready containerization)
* **LLM Integration:** Ollama (Local), Anthropic API (Cloud fallback)

## 🐳 Quick Start (Docker)
Sentinel is fully containerized for deployment across any infrastructure.

```bash
# 1. Clone the repository
git clone [https://github.com/yourusername/sentinel-proxy.git](https://github.com/yourusername/sentinel-proxy.git)
cd sentinel-proxy

# 2. Build the Docker Image
docker build -t sentinel-proxy .

# 3. Run the Container
docker run -p 8000:8000 sentinel-proxy
