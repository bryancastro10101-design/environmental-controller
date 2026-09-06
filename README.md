# MSPM0+ Environmental Controller



An embedded C++ learning project for environmental monitoring,

diagnostics, fault handling, and eventual low-voltage ventilation control.



## Project status



Day 3: requirements, architecture, traceability, and verification baseline.



## Version 1 goals



- Non-blocking monotonic timing

- LED heartbeat

- UART diagnostics

- Environmental sensor acquisition

- Sensor fault detection and recovery

- Deterministic memory use



## Repository structure



- `docs/` — engineering documentation

- `firmware/app/` — application behavior

- `firmware/drivers/` — device drivers

- `firmware/platform/` — MSPM0-specific code

- `tests/` — tests and test support



## Documentation



- [Requirements](docs/requirements.md)

- [Architecture](docs/architecture.md)

- [Verification plan](docs/verification-plan.md)

- [Traceability](docs/traceability.md)

- [Engineering decisions](docs/decisions.md)



## Hardware and tools



- Board: TBD

- MCU: TBD

- Environmental sensor: TBD

- IDE: Code Composer Studio, version TBD

- SDK: TI MSPM0 SDK, version TBD



## Safety



The initial project uses only extra-low-voltage development hardware. It

is not a certified safety or air-quality instrument and will not directly

switch mains voltage.


