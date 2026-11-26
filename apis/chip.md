# Chip API

Source: `_G.chip`

## Summary

The chip API handles basic computer tasks such as telling the time or changing the computers state.
It can also provide mod and computer identification.

## Functions

### getUUID()
Gets a unique identifier inherent to the computer's chassis.
An example of a UUID would be `"e58ed763-928c-4155-bee9-fdbaaadc15f3"`.

`returns: String`

### sleep(milli)
Blocks the computer for the given number of milliseconds before returning. The sleep ends early if the computer is shut down or crashes while waiting.

### getMachine()
Gets a textual description of the computer.
For example, `"Large Computer"`.

`returns: String`

### crash(message)
Sets the computer to a crashed state, in which the computer does not execute code but preserves an error message can be read by clicking on it.
The recommended use case for crashing a computer is to register emergency errors that cant be rendered to the screen or are in other ways critical.

### shutdown()
Disables the computer, no code will execute after shutdown is called.

### reboot()
Restarts the computer without manual intervention or kicking users out of the screen interface.
Will also reload computer language settings.

### version()
Returns the current version of N.E.E.T. computers installed on the server.

`returns: String`

### getTime()
Gets the amount of seconds the computer has been executing code, with 3 decimal points of precision.

`returns: Decimal`

### getUnixTime()
Gets the current time in unix time as seconds, with 3 decimal points of precision.

`returns: Decimal`

### getMonotonic()
Gets monotonic time in seconds. Unlike `getUnixTime`, this never goes backwards and is unaffected by wall clock adjustments, so it's the correct clock for measuring elapsed time or building deadlines.

`returns: Decimal`

### getMemory()
Gets memory usage for the computer's runtime.

```
returns {
    "used": Integer,
    "total": Integer
}
```

### getLunarTime()
Gets the in-game lunar time, as is functions with the /time command.
```Benchmarks
Day: 1000
Noon: 6000
Night: 13000
Midnight: 18000
```
`returns: Integer`

### isViewed()
Checks if a user is viewing the computer.

`returns: Boolean`