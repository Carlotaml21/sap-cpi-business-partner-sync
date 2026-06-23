# SAP CPI — Business Partner Sync (S/4HANA → CRM)

> SAP Cloud Integration (CPI) iFlow that syncs Business Partner data from SAP S/4HANA to an external CRM — with OAuth2 security, error handling and Groovy.

**Status:** 🚧 In progress

## Scenario (the spec)
Sync business partners from SAP S/4HANA into an external CRM. On demand (later: scheduled), the iFlow reads Business Partners from the S/4HANA OData API, maps them to the CRM's JSON format, and sends them to the CRM's REST API. If something fails, it retries and logs a traceable error.

## Architecture
![Architecture](docs/diagram.svg)

- **Source:** SAP S/4HANA — Business Partner OData API (SAP Business Accelerator Hub sandbox)
- **Target:** External CRM — REST API (mock)
- **Trigger:** HTTPS sender (on demand) — later a scheduled timer
- **Transformation:** Message mapping (OData → CRM JSON) + Groovy for what mapping can't do cleanly (full name, date formatting, source + timestamp)
- **Quality:** API key stored as Security Material, OAuth2 / credentials for the target, exception subprocess with retry, correlation id + MPL logging

## What it demonstrates
- End-to-end SAP ↔ non-SAP integration on SAP BTP / Integration Suite
- Secure connectivity: secrets as Security Material, OAuth2
- Integration patterns: exception subprocess, retry, traceability
- Groovy applied only where it adds value

## SAP components / tech
- SAP Integration Suite — Cloud Integration (CPI)
- Adapters: HTTPS (sender), OData / HTTP (receivers)
- OData V2 · JSON · Groovy

## How to run
_(Coming)_ Import the iFlow package, configure the Security Materials (S/4HANA sandbox API key, CRM credentials) and the receiver endpoints, then deploy and call the HTTPS endpoint.

## Key decisions & learnings
_(I'll fill this in as I build — why I designed it this way, trade-offs, what I'd improve.)_
