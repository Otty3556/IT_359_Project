# AI-Assisted Email Credibility & Phishing Detection Tool

## Overview
This project is a Python-based cybersecurity tool designed to analyze `.eml` email files and determine whether an email is legitimate or potentially malicious.

The system extracts key technical and textual features from emails, assigns a credibility score, and provides an AI-generated explanation of suspicious indicators. The goal is not only detection, but also education, helping users understand how phishing attacks work.

---

## Features
- Parse `.eml` email files
- Extract sender, subject, body, and links
- Detect phishing indicators such as:
  - Sender and reply-to mismatches
  - Suspicious URLs
  - Urgent or manipulative language
  - Requests for sensitive information
  - Grammar irregularities
- Generate a credibility/risk score
- AI-powered explanation of detected threats

---

## How It Works
1. The system reads a `.eml` file
2. Extracts header and body content
3. Identifies phishing indicators using rule-based logic
4. Assigns a credibility score based on findings
5. Uses AI to explain suspicious elements in plain language

This hybrid approach improves transparency and avoids relying solely on AI.

---

## AI Usage
The AI model is used as an interpretive layer, not the primary detector.

It analyzes:
- tone (urgency, fear, authority)
- language patterns
- social engineering tactics
- message structure

It then explains why the email may be suspicious by highlighting red flags such as:
- deceptive wording
- impersonation attempts
- emotional manipulation

The system also considers:
- reducing false positives
- avoiding bias toward non-standard writing styles

---

## Tech Stack
- Python
- Email parsing libraries
- Regex / string analysis
- AI / NLP model
- GitHub

---

## Project Structure
IT_359_Project/
│── main.py
│── parser/
│── detection/
│── ai_analysis/
│── samples/
│── README.md
│── requirements.txt

---

## Team Members
- **Bosun Moibi** – Project Manager & Integration Lead  
- **Denvour Davis** – Backend Developer (Parsing & Logic)  
- **Christopher Vandergriff** – AI/NLP Implementation  
- **James** – Testing & Documentation  

---

## Objectives
- Build a functional email parser
- Detect phishing and social engineering patterns
- Generate credibility scores
- Provide clear AI explanations
- Test against real and fake email samples
