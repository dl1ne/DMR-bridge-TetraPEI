# DMR-bridge-TetraPEI

## Structure

```

+-------------+
| DMR Network |
+-------------+
     ||
     ||
     ||  HB-Protocol/MMDVM
     ||
     ||
+-----------+   Audio   +---------------+   Audio  +---------+
| HB_Bridge |   <--->   | Analog_Bridge |   <--->  | SVXLink |
+-----------+   AMBE    +---------------+   USRP   +---------+
     ||                                                ||
     ||                                                ||
+-----------+           Call Control               +--------------------------+
| TetraPEI  |   <------------------------------->  | Motorola MTM 800e / 5x00 |
+-----------+            Serial PEI                +--------------------------+

```

## Components
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

## Configuration

### /opt/HBLink/HB_Bridge.cfg
Just configure the voice ports to adjust to Analog_Bridge. No rules needed.

### /opt/HBLink/hblink.cfg
Create a client object which connects to your DMR master server.
No Master configuration needed.

### /opt/HBLink/tetra_pei.cfg
Configure your PEI serial settings to match your radio settings.
Also adjust GSSI to match the DMR talkgroup, repeater to match your repeater id in DMR network.

### /opt/Analog_Bridge/Analog_Bridge.ini
As specified in HB_Bridge.cfg, set your voice ports to adjust your needs.
Also specify DMR settings:
- GatewayDmrId (just for pseudo, is rewritten in HB_Bridge from PEI)
- repeaterId (same as in tetra_pei.cfg)
- txTg (same as in tetra_pei.cfg)
- txTs (Timeslot which is used in transmission to DMR network)
- Configure your AMBE decoder, maybe also serial - or emulator
- Configure USRP connection to SVXLink and remember ports for next configuration file

### /usr/local/etc/svxlink/svxlink.conf
```
[GLOBAL]
..
LOGICS=SimplexLogic,UsrpLogic
LINKS=UsrpLink
..

[UsrpLogic]
TYPE=Usrp
USRP_HOST=127.0.0.1
USRP_TX_PORT=31001
USRP_RX_PORT=31003
CALL=<YOUR CALL>
DV_USER_INFOFILE=/usr/local/etc/svxlink/dv_users.json
EVENT_HANDLER=/usr/local/share/svxlink/events.tcl
JITTER_BUFFER_DELAY=400
NET_LIMITER_THRESH=-1.0
LOCAL_LIMITER_THRESH=-1.0

[UsrpLink]
NAME=Usrp
CONNECT_LOGICS=SimplexLogic,UsrpLogic
DEFAULT_ACTIVE=1

[Rx1]
..
SQL_DET=PTY
PTY_PATH=/tmp/ptt
SQL_START_DELAY=0
SQL_DELAY=0
SQL_HANGTIME=2000
..

[Tx1]
..
PTT_TYPE=NONE
..

```

.. Also remeber to use your brain and check all other settings around.
