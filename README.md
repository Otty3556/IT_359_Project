# AI-Assisted Email Credibility & Phishing Detection Tool - PhishScan

Video Presentation: URL

---

## Overview

PhishScan is a browser-based email threat analysis tool. It accepts a standard .eml email file, performs automated static analysis against twelve known phishing indicators, generates a numeric risk score from 0-100, and uses a locally hosted large language model via LM Studio to produce a plain-English explanation of the findings.

The goal is twofold: detection and education. PhishScan does not just flag suspicious emails — it explains why they are suspicious, helping users recognize similar attacks in the future. All analysis runs locally. No email content is ever sent to an external server.

---

## Team

James Yahr 
Bosun Moibi
Denvour Davis
Christopher Vandergriff

---

## Features

- Parse .eml files directly in the browser (RFC 2822 / MIME format)
- Extract and display key email headers (From, Reply-To, Return-Path, SPF, DKIM, DMARC)
- Detect phishing indicators, including:
  - Sender, Reply-To, and Return-Path domain mismatches
  - Brand impersonation in display names
  - SPF, DKIM, and DMARC failures (read from header)
  - Urgency and threat language in the subject and body
  - Requests for sensitive information (credentials, PII, financial data)
  - Suspicious URLs (shorteners, raw IPs, unencrypted HTTP, abused TLDs)
- Generate a 0-100 risk score with CLEAN / SUSPICIOUS / PHISHING verdict
- AI-powered plain-English explanation via LM Studio (local, private)
- Graceful fallback — static analysis always runs even if LM Studio is offline

---

## Dependencies & Requirements

PhishScan has no npm packages, no Python libraries, and no build step. It is a single .html file, using JavaScript for all of the built-in logic.;

Runtime requirements:
- A modern web browser (Chrome recommended)
- LM Studio — for the AI explanation feature, download at https://lmstudio.ai

To serve the file locally, choose one of the following:
- Python 3:  python -m http.server 8080
- Node.js:   npx serve .
- VS Code:   Live Server extension, right-click the file and select Open with Live Server

Note: A local server is required because browsers block fetch() calls made from file:// origins.
Opening PhishScan.html by double-clicking it will cause the LM Studio connection to fail silently.

---

## Setup & Installation

1. Clone the repository

   git clone https://github.com/your-username/PhishScan.git
   cd PhishScan

2. Set up LM Studio (optional, required only for AI analysis)

   - Download and install LM Studio from https://lmstudio.ai
   - Download any chat-capable model (e.g. Llama 3, Mistral, Phi-3)
   - Go to the Developer tab in LM Studio
   - Load your model
   - Enable Allow Cross-Origin Requests (CORS)
   - Click Start Server (runs on http://localhost:1234 by default)

3. Serve PhishScan locally

   cd src
   python -m http.server 8080

4. Open in your browser

   http://localhost:8080/PhishScan.html

---

## Usage Guide

Step 1 — Connect to LM Studio
Enter your LM Studio endpoint and model name at the top of the page, then click Test Connection.
- Default endpoint: http://localhost:1234/v1/chat/completions
- Model name: whatever model you have loaded in LM Studio

If you skip this step, static analysis will still run. You just will not get the AI explanation.

Step 2 — Load an email file
Drag and drop a .eml file onto the drop zone, or click it to browse.
The email headers panel will populate immediately.

How to export a .eml file:
- Gmail: Open the email, click the three-dot menu, select Download message
- Outlook: File, Save As, or drag the email to your desktop
- Thunderbird: Right-click the email, select Save As

Step 3 — Analyze
Click Analyze Email. The tool will run static analysis and display the risk score, verdict,
indicators, and extracted URLs instantly. It will then send the results to LM Studio and
display the AI explanation once it responds.

---

## Reading the Results

Risk Score Thresholds:
- 0 to 34:   CLEAN      — No significant indicators detected
- 35 to 69:  SUSPICIOUS — Ambiguous indicators, proceed with caution
- 70 to 100: PHISHING   — Multiple high-confidence indicators present

Indicator Severity:
- HIGH  — Strong phishing signal
- MED   — Moderate signal
- LOW   — Minor or no issues

SPF / DKIM / DMARC Note:
These results are read from the Authentication-Results header already present in the .eml file.
PhishScan cannot perform live DNS lookups from the browser. Auth indicators are shown as HIGH
severity but contribute fewer points to the score to reflect this limitation. Each auth indicator
includes an explicit caveat in its description.

---

## Example

A test file is included at docs/test_phishing.eml for testing purposes. It is a synthetic
phishing email designed to trigger multiple indicators and should produce a score in the 90+
PHISHING range.

---


## Project Report

The full technical writeup is available in docs/. It covers the
technical implementation, design decisions, limitations, and future work for the project.
