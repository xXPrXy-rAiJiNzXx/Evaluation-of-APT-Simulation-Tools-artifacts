# Evaluation of APT Simulation Tools and Mapping Accuracy to the MITRE ATT&CK Framework

This repository contains the artifacts, configuration files, rulesets, and log datasets for the research paper focused on evaluating Advanced Persistent Threat (APT) simulation and monitoring tools.

## Abstract
In an increasingly digitalized landscape, defending against sophisticated APTs remains a significant challenge. This work analyzes how accurately APT simulation tools—**Atomic Red Team**, **PurpleSharp**, and **MITRE Caldera**—reflect the techniques and tactics they claim to cover and how effectively these simulated attacks are detected by endpoint monitoring solutions like **Sysmon**, **Wazuh**, and **Hayabusa**. The goal is to identify the gap between theoretical threat modeling and practical threat emulation.

## Project Structure

The repository is organized as follows:

- **`AtomicRedTeam/`**: Contains the Atomic Red Team framework and associated atomic tests mapped to MITRE ATT&CK.
- **`MitreCaldera/`**: Configuration and setup for the MITRE Caldera adversary emulation platform.
- **`PurpleSharp/`**: Artifacts related to the PurpleSharp adversary emulation framework.
- **`Logs/`**: Raw and processed log datasets generated during the simulation phases.
    - `AtomicRedTeam_Logs/`
    - `Caldera_Logs/`
    - `PurpleSharp_Logs/`
- **`Sigma/`**: The Sigma rulesets used for threat detection and log analysis.
- **`Hayabusa/`**: Binaries and configuration for the Hayabusa threat hunting tool used for rapid EVTX analysis.
- **`Wazuh/`**: Installation files and configuration for the Wazuh SIEM platform.
- **`Sysmon/`**: Sysmon binaries and the specific configuration (`sysmonconfig-export.xml`) used for endpoint telemetry.

## Methodology

The test environment consists of a Windows 11 target machine, an Ubuntu attacker machine (hosting Caldera), and an Ubuntu server (hosting Wazuh Manager).

1.  **Simulation**: APT techniques are executed using Atomic Red Team, PurpleSharp, and MITRE Caldera.
2.  **Telemetry**: System activities are captured via **Sysmon** and forwarded to **Wazuh**.
3.  **Analysis**: Logs are evaluated against **Sigma rules** using **Hayabusa** for offline analysis and **Wazuh** for real-time detection.
4.  **Mapping**: Detections are mapped back to the MITRE ATT\&CK framework to evaluate the accuracy of the simulation tools.

## Preliminary Results

| Tool | Tested TTPs | Exact Detections | Related Detections | Total Noise (Avg. IDs) |
| :--- | :--- | :--- | :--- | :--- |
| Atomic Red Team | 5 | 4 | 1 | Up to 16 |
| PurpleSharp | 5 | 2 | 3 | Up to 5 |
| MITRE Caldera | 20 | 8 | 4 | Up to 20 |

Key findings include:
- **Atomic Red Team** showed the highest alignment (80% accuracy) but generated significant "noise" due to the technical prerequisites of its payloads.
- **PurpleSharp** often triggered parent-level techniques rather than specific sub-techniques, particularly in Wazuh.
- **MITRE Caldera** generated broad detection chains due to its agent-server architecture and background communications.