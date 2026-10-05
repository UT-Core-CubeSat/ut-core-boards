# Communications Board UHF/S-Band



The communications board will provide UHF uplink/downlink and S-band downlink capability. UHF will be used for telemetry and command communication, while S-band will be used for payload data downlink

Owner: Drake/Armando | PCB revision: TBD | Last reviewed: TBD
Board files: TBD | Related documents: [links and applicable revisions]

## 1. Purpose & Design


The communications board will provide communication between the CubeSat and the UHF and S-band ground stations. The UHF system will support command uplink and telemetry downlink, while the S-band will primarily support high-data-rate payload downlink. 

The current design goal is to implement both UHF and S-band communication on a single PCB, with seperate RF signal chains and seperate antennas for each band. The final PCB layer count will need to be determined and will depend on RF routing, grounding, power distribution, signal integrity and board space requirements. 

The UHF system is intended to support simultaneous transmit and receive operation. The architecture required to achieve this is still to be determined. 

The communications board will depend on the CDH/software system for the command and data handling and on the EPS subsystem for electrical power. Required transmit power, receiver gain, amplifier stages, data rates, and acceptable error rates will be determined through link-budget analysis and component selection. 

The following diagram shows the preliminary communications board architecture, including the control interface, UHF transmit/receive paths, S-band transmit path, monitoring, and debug interfaces.

[Conceptual Communications Board Block Diagram](Designchoice_1commsblockdiagram.png)

## 2. Specifications

List the requirements and limits that matter for designing and using this
board. Include units and operating conditions. Distinguish required values
from what this revision supports; mark estimates, unverified values, and TBDs.

| Specification | Value / limit | Notes |
|---------------|---------------|-------|
| Input power | TBD | Coordinate with EPS team |
| Power consumption | TBD | Normal and peak require component selection |
| UHF uplink frequency | 434 MHz | Ground station to the CubeSat |
| UHF downlink frequency | 438 MHz | CubeSat to the ground station |
| UHF capability | TX and RX | Simultaneous TX/RX desired, implementation TBD |
| UHF modulation | TBD | FM-based digital modulation under consideration | 
| UHF data rate | TBD | Determined from telemetry/command requirements | 
| UHF TX power | TBD | Determine from through link-budget analysis | 
| UHF data | Telemetry/commands | Exact data rate and protocol TBD |
| S-band capability | Downlink | Payload data | 
| S-band frequency | 2.4GHz | CubeSat to the ground station |
| RF impedance | 50 ohm target | RF signal paths and antenna interface | 
| PCB layer count | TBD | 6-layer board being considered | 
| Operating environment | TBD | Spacecraft environmental requirements |
| S-band modulation | TBD | Determined from payload data and link requirements |
| S-band data rate | TBD | Determined from payload data requirements |
| S-band TX power | TBD | Determined through S-band link-budget analysis | 
| UHF receiver sensitivity | TBD | Determined by modulation, data rate, and link budget | 
| UHF receiver gain | TBD | Determined by receiver gain/noise budget | 
| UHF receiver noise figure | TBD | Determined by cascaded noise analysis | 
| UHF TX/RX isolation | TBD | Required if simultaneous TX/RX is implemented | 
| UHF/S-band cross-band isolation | TBD | Required if radios operate concurrently | 
| Frequency reference stability | TBD | Based on transceiver and Doppler requirements | 



## 3. Interfaces


The Communications Board interfaces with the rest of the CubeSat through the spacecraft CAN bus and power distribution system. It also connects to seperate UHF and S-band antennas through two SMA connectors.

## 3.1 Spacecraft Interfaces

The Communications Board interfaces with the spacecraft CDH system and EPS. 

| Signal / Interface | Direction | Description |
|---|---|---|
| CAN_H | Bidirectional | CAN differential high |
| CAN_L | Bidirectional | CAN differential low |
| VIN/ Power Rail | Input | Main board power input from EPS; voltage TBD |
| GND | - | Spacecraft common electrical ground | 
| Reset / Enable | TBD | Board reset or power enable interface (if required) |

## 3.2 UHF RF Interface

The UHF RF interface connects the communications board to a dedicated UHF antenna. 

| Signal / Interface | Direction | Description |
|---|---|---|
| UHF RF | Bidirectional | Approximately 434 MHz RX / 438 MHz TX | 
| RF Ground |-|-|

The UHF antenna interface should have a nominal impedance of 50 ohms. 

The final implementation for seperating the UHF transmit and receive paths is TBD. Possible architectures include an RF switch for half-duplex operation or a duplexing/filter network if simultaneous transmit and receive is required. 

## 3.3 S-Band RF Interface

The S-band RF interface connects the communications board to a dedicated S-band antenna. 

| Signal / Interface | Direction | Description |
|---|---|---|
| S-band RF | Output | Approximately 2.4 GHz payload data downlink |
| RF Ground |-|-|

The S-band antenna interface shall have a nominal impedance of 50 ohms. 

## 3.4 Power and Grounding 

The communications board receives electrical power from the EPS subsystem. 

Final input voltage and current limits are TBD. 

Seperate regulated power domains should be considered for:
- Digital/control circuitry
- UHF RF circuitry
- S-band RF circuitry
- High-power RF amplifiers

The board shall use the spacecraft common electrical ground while maintaining appropriate RF return paths and grounding practices. 

### 3.5 Commands and Telemetry

The communications board shall receive commands from the CDH over CAN. 

Commands could include functions such as:
- Configure radio operating mode.
- Enable or disable UHF receive.
- Enable or disable UHF transmit.
- Enable or disable S-band transmit.
- Configure radio frequency.
- Configure transmit power.
- Configure modulation/data-rate parameters
- Reset or reinitialize RF devices.

The communications board should provide status and telemetry to CDH including:
- Radio operating state. 
- Received signal strength.
- Board voltage/current.
- UHF subsystem current.
- S-band subsystem current.
- RF amplifier temperature.
- Board temperature.
- Fault status.
- Radio/transceiver communication status.

Exact CAN commands and telemetry message definitions are TBD and shall be coordinated with the software team.

### 3.6 Programming, Debugging, and Test Interfaces

The board shall provide access for controller programming and debugging.

Interfaces could include:
- UART debug interface.
- Power-rail test points.
- RF test points where practical.
- SPI/CAN test access where practical.


## 4. Operation & Limitations

### Startup

At initial power-up, RF transmitters shall remain disabled until the controller has confirmed that required subsystems are operating.

The board shall initialize the controller, radio devices, monitoring circuitry, and communication interfaces before entering normal operation


### Normal Operation

This board is expected to support several operating modes:

1. Safe/Idle
    - RF transmittters disabled. 
    - Controller and required monitoring active.

2. UHF Receive
    - UHF receiver enabled.
    - Used for command uplink.

3. UHF Transmit
    - UHF transmit enabled.
    - Used for telemetry downlink.

4. UHF Simultaneous TX/RX (If we end up going with this design choice)
    - Desired capability.

5. S-Band Transmit
    - S-band transmitter enabled.
    - Used for payload data downlink.

6. Fault / Recovery
    - Affected RF subsystem disabled or reset.
    - Fault reported to CDH when possible.

### Fault Detection, Isolation, and Recovery

The board should monitor critical RF and power system conditions.

Potential faults include:
- Excessive current.
- Excessive RF amplifier temperature.
- Loss of communication with transceiver.
- Radio configuration errors.
- Abnormal power-rail voltage.
- Antenna or RF output fault if detectable.

Where practical, the UHF and S-band RF sections should be independently enabled and disabled so if a failure were to occur one RF subsystem does not require shutting down the entire communications board.

IF an RF device stops responding, the controller should attempt to:
1. Reinitialize the device.
2. Reset the affected radio.
3. Power-cycle the affected RF section. (If supported)
4. Report the fault to CDH.

A transmitter shall be disabled if an over-current or over-temperature condition is detected.

### Known Limitations / TBD Items

The following items are not yet finalized:

- UHF simultaneous TX/RX requirement.
- UHF duplexer/filter/switch architecture.
- Allowed simultaneous operating modes between UHF and S-band.
- UHF-to-S-band and S-band-to-UHF isolation requirements.
- UHF modulation.
- S-band modulation.
- UHF data rate.
- S-band data rate.
- UHF transmit power.
- S-band transmit power.
- Receiver gain.
- Receiver sensitivity.
- Receiver noise figure. 
- RF amplifier selection.
- Input power rails. 
- Power consumption.

These values will be determined when link-budget calculations are made. Also through component selection.


### 5. Notes

The UHF and S-band RF chains will be designed seperately even if both systems are located on the same PCB board.

Receiver component selection should consider cascaded gain, noise figure, linearity, and saturation. Low-noise amplification should occur near the beginning of the receive chain after required input filtering. 

Transmit amplifier stages shall not be selected until the required RF output power has been determined through link-budget analysis. 

Purpose of RF filter shall be used to:
- Reject out of band interference.
- Reduce transmitter harmonics.
- Reduce mixer or transceiver spurious signals.
- Protect receiver stages from strong unwanted signals.

RF traces SHALL be treated as controlled-impedance transmission lines with a nominal characteristic impedance of 50 ohms. (There are many impedance calculators that can help with this, maybe altium has a built in function?)

RF layout shall prioritize:
- Continuous ground return paths. 
- Short RF traces.
- Isolation between TX and RX sections.
- Isolation between UHF and S-band sections.
- Ground-via stitching.
- Appropriate RF test points. 

The UHF and S-band link budgets should be completed before final selection of power amplifiers, LNAs, gain stages, filters, and RF power requirements. 
