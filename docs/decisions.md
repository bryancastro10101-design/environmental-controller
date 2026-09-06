# Architecture Decision Records



## ADR-001 — Begin with cooperative scheduling



- Status: Accepted

- Date: 2026-09-06



### Context



Version 1 has a small number of periodic activities. The exact MSPM0+

resource limits are not yet documented.



### Decision



Use a hardware timer, monotonic timebase, and cooperative scheduling.

Do not introduce an RTOS unless later requirements justify it.



### Consequences



- Low memory overhead

- Straightforward debugging

- Tasks must remain short

- Long operations must be implemented as non-blocking state machines



## ADR-002 — Separate application policy from hardware access



- Status: Accepted

- Date: 2026-09-06



### Context



Application behavior should be testable without physical hardware.



### Decision



Place MCU-specific operations in the platform and driver layers.

Application code shall not directly access peripheral registers.



### Consequences



- Application logic can be tested on a host computer

- Hardware changes affect fewer modules

- Interfaces and adapters add some initial code



## ADR-003 — Defer sensor selection



- Status: Accepted

- Date: 2026-09-06



### Context



The exact environmental sensor has not been selected.



### Decision



Define sensor-independent behavior now and select the sensor after the

board interfaces, voltage levels, resource limits, availability, and

measurement requirements are reviewed.



### Consequences



- Requirements avoid assuming unsupported hardware

- Sensor-driver work cannot begin until selection is complete


