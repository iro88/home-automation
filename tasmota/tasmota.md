# Shelly 2.5 as roller shutter

### Basic setup for standard `tasmota.bin` firmware:

Template for "standard" double electric momentary / non-latching buttons (not staying in ON position):
```
{"NAME":"Shelly 2.5","GPIO":[56,255,19,0,21,127,0,0,6,126,5,22,156],"FLAG":2,"BASE":18}
```

Settings for interlock (prevent to both buttons ON at the same time):
```
Interlock 1,2
Interlock ON
```

Rules to OFF power when engine stops moving (with limit switches):
```
Rule1 ON power1#state=1 DO Backlog RuleTimer1 1; Rule2 1 ENDON
      ON power2#state=1 DO Backlog RuleTimer2 1; Rule3 1 ENDON

Rule2 ON power1#state=1 DO RuleTimer1 1 ENDON
      ON energy#current[1]<0.001 DO Backlog power1 0; Rule2 0 ENDON

Rule3 ON power2#state=1 DO RuleTimer2 1 ENDON
      ON energy#current[2]<0.001 DO Backlog power2 0; Rule3 0 ENDON

Rule1 1
Rule2 1
Rule3 1
```

### Setup for custom tasmota firmware:

https://github.com/arendst/Tasmota/wiki/blinds-and-shutters
