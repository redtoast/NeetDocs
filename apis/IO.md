# IO API

Source: `_G.io`

## Summary

Allows computers to interface with attached peripherals, and network with other computers.
See [system events](/apis/events/system-events) for peripheral detection events.

## Functions

### getPeripherals()
Lists the UUID's of all attached peripherals, An example of a peripheral UUID would be `"e58ed763-928c-4155-bee9-fdbaaadc15f3"`.

`returns: String[]`

### getType(uuid)
Gets the type of the peripheral, an example of a peripherals type would be `"neetcomputers:redstone_controller"`.

`returns: String`

### getTag(uuid)
Gets the assigned tag of a peripheral, or nil if it has none.

`returns: String | Nil`

### isNative(uuid)
Checks to see if the peripheral uses the native N.E.E.T. peripheral system or has been adapted from another mod, usually CC:T.

`returns: Boolean`

### setTag(uuid, tag = nil)
Sets the tag of a peripheral, which is saved to the peripheral's memory.

### queryTag(tag)
Returns the UUIDs of all attached peripherals with the given tag.

`returns: String[]`

### queryType(type)
Returns the UUIDs of all attached peripherals of the given type.

`returns: String[]`

### wrapPeripheral(uuid)
Returns a table of all the peripherals functions indexed by function name.

`returns: {String : Function}`

### callFunction(uuid, function, arguments...)
Called the indexed function of the peripheral with the given uuid, supplying the provided arguments and returning the function calls result.

`returns: Any`

### broadcastLocal(arguments...)
Broadcasts the given arguments directly to all other computers attached with network cable.
No extra information is provided, uni-cast networking and computer identification is the responsibility of individual computers.

See [network events](/apis/events/network-events) for how broadcasts are received.