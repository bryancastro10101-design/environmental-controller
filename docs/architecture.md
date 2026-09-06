# Software Architecture



## Layers



### Application



- Operating state machine

- Environmental policy

- Future ventilation policy

- Fault policy



### Services



- Cooperative scheduler

- Sensor acquisition service

- Diagnostics service



### Drivers



- Environmental sensor driver

- LED driver

- UART driver



### Platform



- Clock initialization

- GPIO

- Timer

- I2C or SPI

- UART

- Watchdog



## Dependency rule



Dependencies flow downward:



Application → Services → Drivers → Platform



Application policy shall not directly access MSPM0 peripheral registers.



## Initial states



- BOOT

- SELF\_TEST

- MONITORING

- DEGRADED



Planned transitions:



- BOOT → SELF\_TEST

- SELF\_TEST → MONITORING

- SELF\_TEST → DEGRADED

- MONITORING → DEGRADED

- DEGRADED → MONITORING



## Timing model



- System timebase resolution: 1 ms

- LED toggle interval: 500 ms

- UART reporting interval: 1000 ms

- Sensor acquisition interval: no more than 5000 ms



## Interrupt policy



Interrupt handlers shall remain short. They may acknowledge hardware,

capture required data, update small state, and notify main-context code.

Formatting, control decisions, and long transactions belong outside

interrupt context.


