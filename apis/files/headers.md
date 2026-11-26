# File Headers

Source: `_G.files.open(...)`

## Summary

Files headers allow for programs to interact with files by writing and reading data.
Do note that headers use resources, and its good form to close before no longer using them.

Note, file headers are no self-referential, and should be called with a . instead of a : .

## Functions

### read(format = 'l')
Starts reading data from the reading cursor to an endpoint determined by the Format parameter, the cursor will then be moved to that point.

The "l"(lowercase L) and "L" formats will read to the next line, if "L" format then the newline character will be returned as well.

The "a" format will read until the end of the file.

`returns: String | Binary String`

### read(amount)
Starts reading data from the read cursor for 'amount' characters, then moved the read cursor past the last character read.

`returns: String | Binary String`

### write(bytes | text)
Writes the data provided to the file header (if supplied as a int the number will be treated like a byte) to the file (some file modes will wipe the file before writing, to append information to the end of a existing file use append (a) file modes).

### seek(whence = 'cur', offset = 0)
Repositions the read cursor, starting from a position specified by whence, to the offset.

```
"set" whence moves the cursor to 'offset' position away from the start of the file, setting its location.

"cur" whence moves the cursor by 'offset' amount away from the cursors current position, accepts negative numbers.

"end" whence moves the cursor 'offset' away from the end of the file, must be negative.
```

A neat trick is because by default seek parameters move zero units away from current pos, and returns the cursors position, calling seek with no arguments will fetch the cursors position.

`returns: Integer`

### size()
Gets the current length of the file in bytes, without moving the cursor. Works on headers opened read-only or for appending, where seeking to the end and back would move the cursor.

`returns: Integer`

### truncate(size)
Resizes the file to `size` bytes and flushes it. Growing the file fills the new space with zero bytes. Fails with `"Disk full"` if the growth would exceed the disk's remaining capacity.

### flush()
Saves the file as it exists in the header.

### close()
Flushes the file and stops using resources, this function will make the header inoperable.