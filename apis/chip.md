# Chip API

Source: `_G.chip`

## Summary

The chip API handles basic computer tasks such as telling the time or changing the computers state.
It can also provide mod and computer identification.

## Functions

**getUUID()**\
gets a unique identifier inherent to the computers chassis.\
An example of a UUID would be `e58ed763-928c-4155-bee9-fdbaaadc15f3`.\
**returns: String**

**sleep(milli)**\
Stops code execution for the given time, it's recommended to call this function when the computer is idle.

**getMachine()**\
Gets a textual description of the computer.\
For example, `Large Computer`.\
**returns: String**

**crash(message)**<br>
Sets the computer to a crashed state, in which the computer does not execute code but preserves an error message can be read by clicking on it.
The recommended use case for crashing a computer is to register emergency errors that cant be rendered to the screen or are in other ways critical.

**shutdown()**\
Disables the computer, no code will execute after shutdown is called.

**reboot()**\
Restarts the computer without manual intervention or kicking users out of the screen interface.
Will also reload computer language settings.

**version()**\
Returns the current version of N.E.E.T. computers installed on the server.\
**returns: String**

**getTime()**\
Gets the amount of seconds the computer has been executing code, with 3 decimal points of precision.\
**returns: Decimal**

**getUnixTime()**\
Gets the current time in unix time as seconds, with 3 decimal points of precision.\
**returns: Decimal**

**getLunarTime()**\
Gets the in-game lunar time, as is functions with the /time command.
```
Day: 1000
Noon: 6000
Night: 13000
Midnight: 18000
```
**returns: Integer**