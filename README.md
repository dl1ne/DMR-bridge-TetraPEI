# DMR-bridge-TetraPEI

## Aufbau

```

+-----------+   Audio   +---------------+   Audio  +---------+
| HB_Bridge |   <--->   | Analog_Bridge |   <--->  | SVXLink |
+-----------+   AMBE    +---------------+   USRP   +---------+
     ||                                                ||
     ||                                                ||
+-----------+           Call Control               +--------------------------+
| TetraPEI  |   <------------------------------->  | Motorola MTM 800e / 5x00 |
+-----------+            Serial PEI                +--------------------------+

```

