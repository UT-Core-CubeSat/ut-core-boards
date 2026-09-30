# Communications Board UFH/S-Band



The communications board will provide UHF uplink/downlink and S-band downlink capability. UHF will be used for telemetry and command communication, while S-band will be used for payload data downlink

Owner: [name/team] | PCB revision: [revision] | Last reviewed: [date]
Board files: [link] | Related documents: [links and applicable revisions]

## 1. Purpose & Design

What does this board do, and what is handled elsewhere?
Explain the overall design, why it makes sense, and the main tradeoffs.
State any assumptions or dependencies on other boards or firmware.

The communications board will provide communication between the CubeSat and the UHF and S-band ground stations. The UHF system will support command uplink and telemetry downlink, while the S-band will primarily support high-data-rate payload downlink. 

The current design goal is to implement both UHF and S-band communication on a single PCB, with seperate RF signal chains and seperate antennas for each band. The final PCB layer count will need to be determined and will depend on RF routing, grounding, power distribution, signal integreity and board space requirements. 

The UHF system is intended to support simultaneous transmit and receive operation. The architecture required to achieve this is still to be determined. 

The communications board will depend on the CDH/software system for the command and data handling and on the EPS subsystem for electrical power. Required transmit power, receiver gain, amplifier stages, data rates, and acceptable error rates will be determined through link-budget analysis and component selection. 

Include a block diagram showing the main functions and connections.
Block diagram still needs to be made.
Keep detailed implementation notes in the board files and PRs.

## 2. Specifications

List the requirements and limits that matter for designing and using this
board. Include units and operating conditions. Distinguish required values
from what this revision supports; mark estimates, unverified values, and TBDs.

| Specification | Value / limit | Notes |
|---------------|---------------|-------|
| Input power | TBD | Coordinate with EPS team |
| Power consumption | TBD | Normal and peak require component selection |
| UHF uplink frquency | 434 MHz | Ground station to the CubeSat |
| UHF downlink freqency | 438 MHz | CubeSat to the ground station |
| UHF capability | TX and RX | Simultaneous TX/RX desired, implementation TBD |
| UHF data | Telemetry/commands | Exact data rate and protocol TBD |
| S-band capability | Downlink | Payload data | 
| S-band frequency | 2.4GHz | CubeSat to the ground station |
| RF impedance | 50 ohm target | RF signal paths and antenna interface | 
| PCB layer count | TBD | 6-layer board being considered | 
| Operating environment | TBD | Spacecraft environmental requirements |

Add or remove rows as needed.

## 3. Interfaces

Describe each external connection: what it connects to, the connector
and mating part, and the pin numbering/orientation.

### [Connection Name]

| Pin / signal | Direction* | Function / electrical limits |
|--------------|------------|------------------------------|
| | | |

*Direction is relative to this board. Include unused and reserved pins.*

Include what the other side needs to know:
- Power limits, grounding, and startup order.
- Protocol, speed, addresses, and termination/pull-ups.
- Commands accepted and data/status provided; link message definitions.
- Timing requirements and signal/output states during startup, reset, and power loss.
- Physical fit and clearance.

Link shared interface documents and identify the revision used.
Include this board's assignments and any differences here.

## 4. Operation & Limitations

Explain how the board behaves during:
- Startup and normal operation.
- Shutdown, reset, and loss of power or communication.
- Faults and recovery, including any backup functionality.

Include any setup needed to use the board and any known limitations
or unresolved questions that affect its use.

## 5. Notes

Anything important that doesn't fit in the sections above.
Keep detailed implementation notes and design history in the board files and PRs.
