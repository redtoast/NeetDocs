# User Events

Events related user actions, mouse events only trigger for the first user to interact with the computer.

See also
- [Keyboard Peripheral](/peripherals/keyboard)

### keyPressed [User]

Triggered when any user presses a key.

| Parameters | Type    | Description                       |
|------------|---------|-----------------------------------|
| Code       | Integer | Number Code of the Key            | 
| Letter     | String  | If applicable, the pressed letter | 
| Modifiers  | Integer | Bitmap of Modifier Keys           | 

### keyReleased [User]

Triggered when any user releases a key.

| Parameters | Type    | Description                        |
|------------|---------|------------------------------------|
| Code       | Integer | Number Code of the Key             | 
| Letter     | String  | If applicable, the released letter | 
| Modifiers  | Integer | Bitmap of Modifier Keys            | 

### mouseClicked [User]

Triggered when the priority users mouse is clicked down.

| Parameters   | Type    | Description             |
|--------------|---------|-------------------------|
| X Coordinate | Integer | X Position of the Click | 
| Y Coordinate | Integer | Y Position of the Click | 
| Mouse Key    | Integer | Mouse Key Pressed       | 

### mouseReleased [User]

Triggered when the priority users mouse is released.

| Parameters   | Type    | Description               |
|--------------|---------|---------------------------|
| X Coordinate | Integer | X Position of the Release | 
| Y Coordinate | Integer | Y Position of the Release | 
| Mouse Key    | Integer | Mouse Key Released        | 

### mouseMoved [User]

Triggered when the priority users mouse moves from one pixel to another.

| Parameters   | Type    | Description                |
|--------------|---------|----------------------------|
| X Coordinate | Integer | X Position of the Movement | 
| Y Coordinate | Integer | Y Position of the Movement | 

### mouseDragged [User]

Triggered when the priority users mouse moves from one pixel to another with a mouse key held down.

| Parameters   | Type    | Description                |
|--------------|---------|----------------------------|
| X Coordinate | Integer | X Position of the Movement | 
| Y Coordinate | Integer | Y Position of the Movement | 
| Mouse Key    | Integer | Mouse Key Being Dragged    | 

### mouseScrolled [User]

Triggered when the priority users mouse is scrolled.

| Parameters      | Type    | Description                     |
|-----------------|---------|---------------------------------|
| X Coordinate    | Integer | The Mouses Current X Coordinate | 
| Y Coordinate    | Integer | The Mouses Current Y Coordinate | 
| Horizontal Span | Integer | Horizontal Distance Scrolled    | 
| Vertical Span   | Integer | Vertical Distance Scrolled      | 