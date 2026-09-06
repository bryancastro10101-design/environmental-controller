# Verification Plan



## Test environment



- Board: TBD

- MCU: TBD

- Sensor: TBD

- CCS version: TBD

- MSPM0 SDK version: TBD

- Firmware commit: Record for every test

- Measurement equipment: Serial terminal and, if available, logic analyzer



## Verification methods



- Inspection: Review documents, source code, configuration, or logs

- Analysis: Evaluate calculations or recorded measurements

- Demonstration: Observe behavior without detailed measurement

- Test: Apply inputs and compare results with pass criteria



## TEST-BOOT-001 — Initialization



**Requirement:** SYS-FUN-001  

**Method:** Demonstration



### Procedure



1\. Disconnect and reconnect board power.

2\. Observe startup.

3\. Confirm the system enters normal monitoring without debugger input.



### Pass criteria



The system begins normal operation without a manual reset.



## TEST-TIME-001 — Timebase



**Requirement:** SYS-FUN-002  

**Method:** Test



### Procedure



1\. Run the firmware for at least 60 seconds.

2\. Compare reported uptime against a reference timer.

3\. Record the difference.



### Pass criteria



The timebase increments at 1 millisecond resolution. The final allowable

clock error will be defined after the clock source is selected.



## TEST-LED-001 — Heartbeat



**Requirement:** SYS-FUN-003  

**Method:** Test



### Procedure



1\. Observe or probe the LED GPIO.

2\. Record at least 20 consecutive transitions.

3\. Measure each transition interval.



### Pass criteria



Each toggle interval is between 490 and 510 milliseconds.



## TEST-UART-001 — Status period



**Requirement:** SYS-FUN-004  

**Method:** Test



### Procedure



1\. Capture at least 20 UART status messages.

2\. Measure the intervals between messages.



### Pass criteria



Each interval is between 980 and 1020 milliseconds.



## INSPECT-SCHED-001 — Non-blocking scheduling



**Requirement:** SYS-FUN-005  

**Method:** Inspection



### Procedure



Review the main application loop and scheduling code.



### Pass criteria



No blocking delay call or unbounded busy-wait loop is used to schedule

periodic application activities.



## TEST-SENSOR-001 — Environmental acquisition



**Requirement:** SYS-FUN-006  

**Method:** Test



### Procedure



1\. Connect the supported sensor.

2\. Run the system for at least 60 seconds.

3\. Record valid measurement timestamps.



### Pass criteria



The interval between measurements does not exceed 5 seconds while the

sensor is operational.



## TEST-FAULT-001 — Enter DEGRADED state



**Requirement:** SYS-FUN-007  

**Method:** Test



### Procedure



Cause three consecutive sensor communication failures.



### Pass criteria



The system enters DEGRADED after the third consecutive failure.



## TEST-FAULT-002 — Return to MONITORING



**Requirement:** SYS-FUN-008  

**Method:** Test



### Procedure



After entering DEGRADED, provide three consecutive valid measurements.



### Pass criteria



The system returns to MONITORING after the third valid measurement.



## TEST-UART-002 — Diagnostic fields



**Requirement:** SYS-FUN-009  

**Method:** Test



### Procedure



Capture a UART status message.



### Pass criteria



The message contains operating state, uptime, and sensor-validity status.



## Evidence record



Every completed test shall record:



- Date

- Tester

- Firmware commit hash

- Board and sensor

- Measurements

- Procedure deviations

- Pass or fail result


