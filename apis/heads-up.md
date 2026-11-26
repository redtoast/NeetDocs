# Heads Up API

Source: `_G.headsup`

## Summary

The heads up API defines a small mono-color display that's usually visually rendered to the computer.
It can be used to provide a quick heads up reference for the state of a computer or program.

## Functions

### set(colored)
Sets the entire display, if colored then the screen will be entirely pixels and if not the screen will be blank.

### draw()
Updates the display with the drawn content, nothing will be drawn unless this is called.

### getSize()
Gets the size of the display.

`returns: Integer, Integer`

### setPixel(x, y, colored)
Enables the pixel at the given coordinates if colored is true.

### drawLine(x1, y1, x2, y2)
Sets the line of pixels between the pairs of coordinates to be enabled.

### fill(x1, y1, x2, y2, colored)
Enables or disables the entire square region based on the state of colored.