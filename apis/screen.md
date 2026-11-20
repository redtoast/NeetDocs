# Screen API

Source: `_G.screen`

## Summary

The screen API is the 24 bit color visual display that is opened when the user clicks a running computer. 
Screens can generate sub-screens or 'layers' that function identically, and can be drawn back to the screen.
Its also worth noting that, for performance reasons, **THE ENTIRE API IS ZERO INDEXED**, or in other words unlike in traditional lua a 400x400 screen will not have a 400, 400 pixel but will have a 0, 0 pixel.

The screen api is definitely the hardest to learn, and can be the main source of computer slowness if handled incorrectly.
If you're a beginner, using a library might be worth your time.
[Colored screen peripherals](/peripherals/color-display) have an identical api.
Screen also supports alpha (or A) values, with 0 being fully transparent and 255 being fully solid.

If your using the screen api it might be wise to also view the [user events](/apis/events/user-events) page or the [chip](/apis/chip).isViewed() function.

## Functions

### getSize()
Gets the size of the screen object.

`returns: Integer, Integer`

### createLayer(sizeX, sizeY)
Creates a new completely blank screen object, unlike the main screen API this object will not have a draw function, but shares all other functions.

`returns: {String : Function}`

### clone(x1, y1, x2, y2)
Clones the given 0-indexed region to a new screen object, who's functions as described in createLayer(...).

`returns: {String : Function}`

### substitute(srcR, srcG, srcB, destR, destG, destB)
Replaces the given 'src' color with the 'dest' color. Note, as screen objects "blend" transparent pixels to the background when drawing them, you will need to know the product of that blending when substituting such pixels.

### writeData(x, y, buffer, width)
Writes a block of data to the screen, starting at x, y (0 indexed) and drawing out the width and a height based on the size of the buffer decided by the width.
The length of the buffer should be width * height * 4, with the 4 being for the R, G, B, A bytes that define one pixel.
The buffer itself should be one big string of these bytes, provided all at once.

```
local chunks = {}
for py = 1, height do
    for px = 1, width do
        -- string.char packs one pixel's R,G,B,A into a 4-byte chunk
        chunks[#chunks + 1] = string.char(r, g, b, a)
    end
end
local buffer = table.concat(chunks) --merges all chunks together in one pass for optimal speed

screen.writeData(0, 0, buffer, width)
```

### readData(x1, y1, x2, y2)
Reads the block of data in the 0 indexed range given, and returns it as a string of bytes.
Its output is formatted the exact same way writeData received information, including an R, G, B, and A value, with A always being 255.

`returns: Binary String`

### writePixel(x, y, R, G, B, A = 255)
Writes the single pixel to the 0 indexed coordinates, it is STRONGLY discouraged to use writePixel for large operations, as individual java api calls are comparatively slow, for these operations please use writeData.

### readPixel(x, y)
Gets the color values at the 0 indexed coordinates, with alpha being assumed 255.

`returns: Integer, Integer, Integer`

### writeLine(x1, y1, x2, y2, R, G, B, A = 255)
Writes a line between the two 0 indexed points.

### fill(x1, y1, x2, y2, R, G, B, A = 255)
Sets the entire 0 indexed range to the set color.

### set(R, G, B, A = 255)
Sets the entire screen to the given color.

### set()
Sets the entire screen to black.

### draw()
Required to update the screen, no changes will take effect until draw is called.
Layer objects or other screen APIs that are not peripherals or the base api will lack this function.