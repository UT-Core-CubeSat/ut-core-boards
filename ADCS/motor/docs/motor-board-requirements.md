# Motor

The motor board operates the four reaction wheels via tourque commands recieved from the ADCS. The motor board is responsible for physically executing the controller and orentiation. 

Owner: Averie: Controls | PCB revision: No edits yet | Last reviewed: 9/30/2026
Board files: C:ut-core-boards\ADCS\Motor | Related documents: "Motor Board Documentation.docx" 

## 1. Purpose & Design

This board turns input from the controller (ADCS) board into PWM signals and transmits them to motor drivers. The motor drivers then turn that signal into three phases and the motors operate accordingly.

## Dependencies
This board is dependent on the ADCS, and cannot operate without input from it.

## Drivers “L6234PD013TR”
There are four drivers. PWM signals go to the IN pins on each driver. The sense pins on the driver are connected to the current-sensing op-amps, which measure two phases of the motor directly and the third is calculated in software. 

Currently, the ENABLE pins for all drivers are tied together. This is hardly functional and is one of the major problems with this board.

This driver selection seems reasonable and there is no reason to change it....yet.

## Current-Sensing Op-Amps
"This device measures the phase current through shunt resistors (high precision/ low ohms resistor) and feeds that information back to the MCU. Accurate current measurement is critical for monitoring motor performance, detecting faults, and enabling closed loop control strategies. This part was selected because it is designed specifically for high common mode environments like motor drives and provides strong noise rejection, which is important given the switching noise from the driver. The voltage divider circuit on the right was used to supply Vref with 1.65v. Doing so makes it so the MCU can read + /- currents in both directions."
^^Tyler Dalton, Motor board document

## eFuse "TPS25940ARVCR”
This is used to protect from overcurrent and short circuit for EACH motor power path. It does not require replacement like a typical fuse, and instead recovers itself after responding quickly. This is crucial for space applications. It can also disable individual motors.

The EFUSE has an overheating problem. Last year's docs believe this was beacause it was forced into current limiting mode and was attempting to dissapate too much heat accross itself (from startup).

They suggested selecting a NEW EFUSE either in addition or instead of this one. Potenitally the TPS25982




## High-level block diagram 


    Input               -- ADCS BOARD---          Output            MOTOR BOARD                    4 REACTION WHEELS
 Sensor data |----->   | Controller/Obs.|------>Actuation-------->|Current Shunts |
 Mode command|----->   |[NDI, EKF, BDOT]|------>Telemetry         |Motor drivers  |----PWM-------> Motors move
                       | Calculations   |------>Debug/SIL         |Rotor feedback |<-------------> Hall effect sensor data 
                       |----------------|                         |3rd phase calc |
                                                                  |---------------|


## 2. Specifications


| Specification | Value / limit | Notes |
|---------------|---------------|-------|
| Input power   | 0-3.3V CC     |4 motors |
| Power consumption |TBD| Normal and peak |
| Outputs / capabilities |TBD | |
| Performance | TBD| |
| Dimensions / mounting | |Mount for new reaction wheels needed |
| Operating environment | | TBD|

Add or remove rows as needed.

## 3. Interfaces

Where does input come from ADCS board? Where exactly
### [Connection Name]
EVERY PIN IS OCCUPIED 

PIN 1	Motor 3 Fault 	Digital input efuse for motor 3 tripped. Error = Low
PIN 2	Motor 4 Fault 	Digital input efuse for motor 4 tripped. Error = Low
PIN 3	Motor 1 Kill	Digital output kill switch for motor 1. Kill power = Low
PIN 4	Motor 2 Kill	Digital output kill switch for motor 2 Kill power = Low
PIN 5	Motor 3 Kill	Digital output kill switch for motor 3. Kill power = Low
PIN 6	VBAT	
PIN 7	LED 1	
PIN 8	Crystal Oscillator	
PIN 9	Crystal Oscillator	
PIN 10	VSS	
PIN 11	VDD	
PIN 12	N/C	
PIN 13	N/C	
PIN 14	NRST	
PIN 15	Motor 1, Phase A	Analog Input for current in motor 1 phase A.( 0-3.3 V. 1.65V = 0A)
PIN 16	Motor 1, Phase B	Analog Input for current in motor 1 phase B.( 0-3.3 V. 1.65V = 0A)
PIN 17	Motor 2, Phase A	Analog Input for current in motor 2 phase A.( 0-3.3 V. 1.65V = 0A)
PIN 18	Motor 2, Phase B	Analog Input for current in motor 2 phase B.( 0-3.3 V. 1.65V = 0A)
PIN 19	VSSA	
PIN 20	VREF  -	
PIN 21	VREF +	
PIN 22	VDDA	
PIN 23	FRAM3_F	
PIN 24	FRAM2_F	
PIN 25	USART2_1	
PIN 26	USART2_2	
PIN 27	GND	
PIN 28	VDD	
PIN 29	FRAM1_F	
PIN 30	MCU_MR	
PIN 31	Motor 4 Phase A	Analog Input for current in motor 4 phase A.( 0-3.3 V. 1.65V = 0A)
PIN 32	Motor 4 Phase B	Analog Input for current in motor 4 phase B.( 0-3.3 V. 1.65V = 0A)
PIN 33	Motor 3, Phase A	Analog Input for current in motor 3 phase A.( 0-3.3 V. 1.65V = 0A)
PIN 34	Motor 3, Phase B	Analog Input for current in motor 3 phase B.( 0-3.3 V. 1.65V = 0A)
PIN 35	Motor 2 PWM C	Digital output PWM for Motor 2 Phase C (TIM3_CH3)
PIN 36	Motor 2 PWM B	Digital output PWM for Motor 2 Phase B (TIM3_CH4)
PIN 37	WD	watch dog WDI
PIN 38	Motor 4 Kill	Digital output kill switch for motor 4. Kill power = Low
PIN 39	Motor 4 Hall A	Digital input for Motor 4, hall sensor A
PIN 40	Motor 4 Hall B	Digital input for Motor 4, hall sensor B
PIN 41	Motor 4 Hall C	Digital input for Motor 4, hall sensor C
PIN 42	Motor 4 PWM C	Digital output PWM for Motor 4 Phase C (TIM1_CH2)
PIN 43	N/C	
PIN 44	Motor 4 PWM A	Digital output PWM for Motor 4 Phase A (TIM1_CH3)
PIN 45	Motor 4 PWM B	Digital output PWM for Motor 4 Phase B (TIM1_CH4)
PIN 46	VREF/GND	MCU 1 is conncected to VREF, MCU 2 is GND to tell which MCU is active.
PIN 47	CS1	
PIN 48	VCAP	
PIN 49	GND	
PIN 50	VDD	
PIN 51	WP1	
PIN 52	SPI2_SCK	SPI clock for FRAM
PIN 53	SPI2_MISO	SPI MISO for FRAM
PIN 54	SPI2_MOSI	SPI MOSI for FRAM
PIN 55	Motor 3 Hall B	Digital input for Motor 3, hall sensor B
PIN 56	Motor 3 Hall C	Digital input for Motor 3, hall sensor C
PIN 57	Motor 4 Enable	Digital output to enable all gates on driver. Enabled = High
PIN 58	Motor 3 Enable	Digital output to enable all gates on driver. Enabled = High
PIN 59	Motor 1 PWM A	Digital output PWM for Motor 1 Phase A (TIM4_CH1)
PIN 60	Motor 1 PWM B	Digital output PWM for Motor 1 Phase B (TIM4_CH2)
PIN 61	Motor 1 PWM C	Digital output PWM for Motor 1 Phase C (TIM4_CH3)
PIN 62	LED 2	
PIN 63	Motor 3 PWM A	Digital output PWM for Motor 3 Phase A (TIM8_CH1)
PIN 64	Motor 3 PWM B	Digital output PWM for Motor 3 Phase B (TIM8_CH2)
PIN 65	Motor 3 PWM C	Digital output PWM for Motor 3 Phase C (TIM8_CH3)
PIN 66	Motor 1 Enable	Digital output to enable all gates on driver. Enabled = High
PIN 67	PA6_1	AND lock 1 IN
PIN 68	PA9_1	
PIN 69	CS3	
PIN 70	PA11	CAN transeiver RXD
PIN 71	PA12	CAN transeiver TXD
PIN 72	PA13	SIO
PIN 73	VDDUSB	
PIN 74	GND	
PIN 75	VDD	
PIN 76	PA14	CLK
PIN 77	PA7	AND lock 2 IN
PIN 78	2 pin header	
PIN 79	2 pin header	
PIN 80	Motor 2 Enable	Digital output to enable all gates on driver. Enabled = High
PIN 81	Motor 1 Hall A	Digital input for Motor 1, hall sensor A
PIN 82	Motor 1 Hall B	Digital input for Motor 1, hall sensor B
PIN 83	PD2	AND lock 1
PIN 84	Motor 1 Hall C	Digital input for Motor 1, hall sensor C
PIN 85	Motor 2 Hall A	Digital input for Motor 2,  hall sensor A
PIN 86	Motor 2 Hall B	Digital input for Motor 2, hall sensor B
PIN 87	Motor 2 Hall C	Digital input for Motor 2, hall sensor C
PIN 88	Motor 3 Hall A	Digital input for Motor 3,  hall sensor A
PIN 89	B0	AND lock1 IN
PIN 90	Motor 2 PWM A	Digital output PWM for Motor 2 Phase A (TIM3_CH1)
PIN 91	WP3	
PIN 92	I2C_SCL	SCl for temp sensors I2C
PIN 93	I2C_SDA	SDA for temp sensors I2C
PIN 94	PH3	AND lock 1 OUT
PIN 95	CS2	
PIN 96	WP2	
PIN 97	Motor 1 Fault	Digital input efuse for motor 1 tripped. Error = Low
PIN 98	Motor 2 Fault	Digital input efuse for motor 2 tripped. Error = Low
PIN 99	GND	
PIN 100	VDD	



Still deriving as they are not in the docs the following:
- Power limits, grounding, and startup order.
- Protocol, speed, addresses, and termination/pull-ups.
- Commands accepted and data/status provided; link message definitions.
- Timing requirements and signal/output states during startup, reset, and power loss.
- Physical fit and clearance.

Determined via KiCad simulation



## 4. Operation & Limitations

- Startup and normal operation.
- Shutdown, reset, and loss of power or communication.
- Faults and recovery, including any backup functionality.

eFuse exists to assist in recovery and fault safety. 


## 5. Notes

Bigger reactionn wheels needed to execute the torque calculations from controller!!










Template stuff

Anything important that doesn't fit in the sections above.
Keep detailed implementation notes and design history in the board files and PRs.



Keep detailed implementation notes in the board files and PRs.
List the requirements and limits that matter for designing and using this
board. Include units and operating conditions. Distinguish required values
from what this revision supports; mark estimates, unverified values, and TBDs.