# Environmental Controller Requirements



## 1. Document control



- Project: MSPM0+ Environmental Controller

- Status: Draft

- Version: 0.1

- Owner: Bryan

- Last updated: 2026-09-06



## 2. Purpose



The system is an educational embedded environmental monitor based on an

MSPM0+ microcontroller. It will periodically collect environmental

measurements, report system status, detect sensor faults, and eventually

control low-voltage ventilation hardware.



## 3. Stakeholders



- User: observes environmental conditions and system status

- Developer: implements and maintains the firmware

- Tester: verifies the requirements and records evidence

- Occupant: benefits from environmental monitoring



## 4. Version 1 scope



Version 1 will:



- Run on an MSPM0+ development board

- Maintain a non-blocking monotonic timebase

- Indicate operation through an LED

- Report status through UART

- Read at least one environmental sensor

- Detect and report sensor failures

- Recover after communication with the sensor is restored



## 5. Out of scope



- Mains-voltage control

- Safety-critical operation

- Certified air-quality measurements

- Cloud connectivity

- Production enclosure

- Secure firmware updates



## 6. Constraints



- Firmware shall be written primarily in C++.

- TI DriverLib and SysConfig may be used.

- The application loop shall not use blocking delays for scheduling.

- The initial system shall operate only from extra-low-voltage power.

- Dynamic memory shall not be allocated after initialization.



## 7. Functional requirements



### SYS-FUN-001 — Initialization



The system shall initialize all configured clocks and peripherals before

entering normal monitoring mode.



**Verification:** TEST-BOOT-001.



### SYS-FUN-002 — Timebase



The system shall provide an unsigned 32-bit monotonic timebase with a

resolution of 1 millisecond.



**Verification:** TEST-TIME-001.



### SYS-FUN-003 — Heartbeat



The system shall toggle the user LED every 500 milliseconds with a

tolerance of ±10 milliseconds during normal monitoring.



**Verification:** TEST-LED-001.



### SYS-FUN-004 — UART status



The system shall transmit one status message every 1000 milliseconds

with a tolerance of ±20 milliseconds.



**Verification:** TEST-UART-001.



### SYS-FUN-005 — Non-blocking scheduling



The application shall schedule periodic activities using elapsed-time

checks rather than blocking delay calls.



**Verification:** INSPECT-SCHED-001.



### SYS-FUN-006 — Environmental acquisition



The system shall acquire one environmental measurement at least once

every 5 seconds while the sensor is operational.



**Verification:** TEST-SENSOR-001.



### SYS-FUN-007 — Sensor fault detection



The system shall enter the DEGRADED state after three consecutive sensor

communication failures.



**Verification:** TEST-FAULT-001.



### SYS-FUN-008 — Sensor recovery



The system shall return to the MONITORING state after three consecutive

valid sensor measurements.



**Verification:** TEST-FAULT-002.



### SYS-FUN-009 — Diagnostics content



Each UART status message shall include the operating state, system uptime,

and latest sensor-validity status.



**Verification:** TEST-UART-002.



## 8. Quality requirements



### SYS-QUAL-001 — Memory



The firmware shall perform no dynamic memory allocation after

initialization.



**Verification:** Source inspection and linker-map review.



### SYS-QUAL-002 — Interrupt design



Interrupt handlers shall acknowledge their interrupt source and defer

nonessential processing to the main execution context.



**Verification:** Source inspection.



### SYS-QUAL-003 — Build quality



Project-owned C++ source files shall compile without compiler warnings

under the documented build configuration.



**Verification:** Clean build-log inspection.



### SYS-QUAL-004 — Modularity



Application policy shall not directly access MSPM0 peripheral registers.



**Verification:** Architecture and source inspection.



## 9. Open items



- Exact MSPM0+ board: TBD

- Exact MCU: TBD

- Environmental sensor: TBD

- CCS version: TBD

- MSPM0 SDK version: TBD


