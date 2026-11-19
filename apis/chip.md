# Chip API

Source: `_G.chip`

## Summary

The chip API handles basic computer tasks such as telling the time or changing the computers state.
It can also provide mod and computer identification.

## Functions

**getUUID()**<br>
gets a unique identifier inherent to the computers chassis.<br>
An example of a UUID would be `e58ed763-928c-4155-bee9-fdbaaadc15f3`.<br>
**returns: String**

**sleep(milli)**<br>
Stops code execution for the given time, it's recommended to call this function when the computer is idle.

**getMachine()**<br>
Gets a textual description of the computer.<br>
For example, `Large Computer`.<br>
**returns: String**

**crash(message)**<br>
Sets the computer to a crashed state, in which the computer does not execute code but preserves an error message can be read by clicking on it.<br>
The recommended use case for crashing a computer is to register emergency errors that cant be rendered to the screen or are in other ways critical.

**shutdown()**<br>
Disables the computer, no code will execute after shutdown is called.

**reboot()**<br>
Restarts the computer without manual intervention or kicking users out of the screen interface.<br>
Will also reload computer language settings.

**version()**<br>
Returns the current version of N.E.E.T. computers installed on the server.<br>
**returns: String**

**getTime()**<br>
Gets the amount of seconds the computer has been executing code, with 3 decimal points of precision.<br>
**returns: Decimal**

**getUnixTime()**<br>
Gets the current time in unix time as seconds, with 3 decimal points of precision.
**returns: Decimal**

**getLunarTime()**<br>
Gets the in-game lunar time, as is functions with the /time command.<br>
```
Day: 1000
Noon: 6000
Night: 13000
Midnight: 18000
```
**returns: Integer**