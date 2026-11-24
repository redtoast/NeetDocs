# System Events

Events related normal computer functionality.

See also
- [IO API](/apis/IO)

### peripheralAttached [System]

Triggered when a peripheral is connected to the computer, does not apply to peripherals that already exist on startup.

| Parameters | Type   | Description            |
|------------|--------|------------------------|
| Type       | String | Type of the Peripheral | 
| UUID       | String | UUID of the Peripheral | 

### peripheralDetached [System]

Triggered when a peripheral is disconnected from the computer.

| Parameters | Type   | Description            |
|------------|--------|------------------------|
| Type       | String | Type of the Peripheral | 
| UUID       | String | UUID of the Peripheral | 