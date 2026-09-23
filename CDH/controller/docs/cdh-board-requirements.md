# CDH Controller

[Brief description of what this board does.]

Owner: [name/team] | PCB revision: [revision] | Last reviewed: [date]
Board files: [hardware](../hardware/) | Related documents: [links and applicable revisions]

## 1. Purpose & Design123

What does this board do, and what is handled elsewhere?
Explain the overall design, why it makes sense, and the main tradeoffs.
State any assumptions or dependencies on other boards or firmware.

Include a block diagram showing the main functions and connections.
Keep detailed implementation notes in the board files and PRs.

## 2. Specifications

List the requirements and limits that matter for designing and using this
board. Include units and operating conditions. Distinguish required values
from what this revision supports; mark estimates, unverified values, and TBDs.

| Specification | Value / limit | Notes |
|---------------|---------------|-------|
| Input power | | |
| Power consumption | | Normal and peak |
| Outputs / capabilities | | |
| Performance | | |
| Dimensions / mounting | | |
| Operating environment | | |

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
