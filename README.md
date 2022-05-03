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

## Komponenten
- HBLink (Branch HB_Bridge)
- Analog_Bridge
- SVXLink (Branch svxlink_usrp)
- TetraPEI
- DV3000 Stick / Emulator


## Installation
```
pip install dmr-utils
cd /opt
git clone https://github.com/dl1ne/Analog_Bridge.git
git clone -b HB_Bridge https://github.com/dl1ne/HBLink.git
cd /usr/local/src
git clone -b svxlink_usrp https://github.com/dl1ne/svxlink.git
```
