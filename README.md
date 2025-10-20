# SENITEL
360° Threat Detection Module

[![License](https://img.shields.io/github/license/endr-us/SENITEL)](LICENSE)

Overview

SENITEL is a 360° threat detection system that aggregates sensor data, runs analysis and detection pipelines, and provides alerts and actionable intelligence for security teams.

Key features

- Multi-sensor fusion (radar, LiDAR, cameras, acoustic sensors)
- Modular detection pipelines with configurable thresholds
- Real-time alerting and logging
- Extensible plugin architecture for new detectors and integrations
- Role-based access control and audit logging

Architecture

SENITEL is organized into the following components:

- Ingest: sensor adapters and data normalization
- Detection Engine: real-time analyzers, model inference, and rules
- Correlation: fuses events across sensors and time windows
- API & UI: REST API and web UI for monitoring and configuration
- Persistence: time-series and event storage

Quick start

1. Clone the repository:
   git clone https://github.com/endr-us/SENITEL.git
2. Install dependencies (refer to each component's README for language-specific instructions)
3. Configure sensors and connectors in config/default.yml or via environment variables
4. Start services with docker-compose or the provided systemd units

Configuration

Configuration is split per component. See the config/ directory for example configurations. You can override values using environment variables or a centralized configuration service.

Usage

- Add sensor adapters in the ingest module to start feeding data.
- Tune detection thresholds in the detection engine configuration.
- Use the REST API to query events and the web UI for visualizing detections.

Contributing

Contributions are welcome. Please open issues or pull requests, follow the contribution guidelines in CONTRIBUTING.md, and sign the CLA if prompted.

License

This project is provided under the license shown above. See the LICENSE file for details.
