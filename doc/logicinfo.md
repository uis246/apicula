# logicinfo

The table entries are divided into key, value and zero for some reason.
Here is description of their discovered meaning.

When you see "or lack of" means when this attribute is not set is also valid state, usually it means disable.
"Something else" means there is other values that should exist but not yet discovered.

## IOB
Datasheet or UG: UG289E-2.1E

- `SLEWRATE`
Valid values: `SLOW`, `FAST`
`SLEW_RATE` from cst file
- `OPENDRAIN`
Valid values: `ON`, `OFF`
`OPEN_DRAIN` from cst file
- `PULLMODE`
Valid values: `UP`, `DOWN`, `KEEPER`, `NONE`
`PULL_MODE` from cst file
- `HYSTERESIS`
Valid values: `HIGH`, `H2L`, `L2H`, `NA`(acts as `NONE`)
`HYSTERESIS` from cst file
- `ODMUX`
Valid values: `TRIMUX`, something else
???
- `ODMUX_1`
Valid values: `"1"`, someting else or lack of
I speculate this is what datasheet refers as `OTMUX`, but can actually mean anything.
Found in OBUF. OBUF is basically TBUF with constant `TO`.
- `PADDI`
Valid values: `PADDI`, possibly lack of
It is present in IBUFs and IOBUFs, I think this means PAD Data Input.
PAD in UG(figures 4-1 and 4-2) is GPIO so this attribute means whether input on that pin is enabled.
- `TO`
Valid values: `INV`, something else or lack of
Related to tristate control, shown on figure 4-1.
Maybe controls if Output Enable is inverted? Or maybe it is used internally to flag when TO is actually used because I cannot find it in logicinfo for GW1NSR-4C
I have no clue.
- `TRI_MUX`
Valid values: `"0"`, `TSREG`, `TMDDR`, something else
This lines up with OTMUX.
`"0"` for GND, `TSREG` for TRIGREG, `TMDDR` for OSER.
Forth option should be for TX input directly.
- `TRIMUX_PADDT`
Valid values: `"0"`, `INV`
???
- `TLVDS_OUT`
Valid values: `ON`, lack of
Whether this pin has TLVDS output, set `ON` only for one pin in pair, other one doesn't have this enabled.

## OSC

- `MCLKCIB`
Valid values: 0-126, even numbers or lack of
It is either `FREQ_DIVISOR%128` or `FREQ_DIVISOR - 2`. I think first one.
- `MCLKCIB_EN`
Valid values: `ENABLE`, lack of
Without it OSC seems to ignore divisor.
- `POWER_SAVE`
Valid values: `ENABLE`, lack of
Looks like some default flag when OSC is not used.
Maybe used to disable OSC reduce power consumption.
- `NORMAL`
Valid values: `ENABLE`, lack of
Seems to enable OSC.
- `USERPOWER_SAVE`
Valid values: `ENABLE`, lack of
Not entirely sure what it means, but for GW1NSR-4C it sets same bit as `NORMAL` and additional one.
