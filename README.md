# SIEM-log-analysis-platform
Mini SIEM platform using Wazuh + Elastic Stack for real-time log ingestion, detection rules, and alerting across Windows, Linux, and firewall logs.

# SIEM Log Analysis Platform

A mini Security Information and Event Management (SIEM) platform built using Wazuh and the Elastic Stack, deployed via Docker. Ingests real-time system logs and file integrity events from a connected endpoint, with custom detection rules for security monitoring.

## What This Project Does

- Deploys a full Wazuh SIEM stack (manager, indexer, dashboard) using Docker Compose
- Connects a live endpoint agent (macOS) that streams real security telemetry
- Monitors file integrity, system logs, and network activity in real time
- Includes custom detection rules for identifying suspicious activity (see below)

## Architecture

[macOS Agent] --> [Wazuh Manager] --> [Wazuh Indexer] --> [Wazuh Dashboard]

- **Wazuh Manager**: receives and analyzes agent data against detection rules
- **Wazuh Indexer**: stores and indexes security events (built on OpenSearch)
- **Wazuh Dashboard**: web UI for visualizing alerts, agents, and security posture

## Tech Stack

- Wazuh 4.9.0
- Docker & Docker Compose
- Elastic Stack (via Wazuh Indexer/Dashboard)
- macOS agent (Apple Silicon)

## Setup

1. Clone Wazuh's official Docker repo:

   git clone https://github.com/wazuh/wazuh-docker.git -b v4.9.0
   cd wazuh-docker/single-node

2. Generate SSL certificates:

   docker compose -f generate-indexer-certs.yml run --rm generator

3. Launch the stack:

   docker compose up -d

4. Access the dashboard at https://localhost (self-signed cert, click through the browser warning)

5. Deploy an agent from the dashboard's "Deploy new agent" flow, matching your OS/architecture

## Screenshots

(add dashboard screenshots here once available)

## What I Learned

- How SIEM architecture works end-to-end (agent to manager to indexer to dashboard)
- Configuring and troubleshooting agent-to-manager connectivity (XML config editing, cert generation)
- Writing custom detection rules for specific threat scenarios
- Docker-based deployment of multi-container security tooling

## Next Steps

- Add custom detection rules for specific attack scenarios
- Integrate additional log sources (firewall, cloud services)
- Map alerts to MITRE ATT&CK techniques

