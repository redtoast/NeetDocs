# Files API

Source: `_G.files`

## Summary

The files API allows programs to access the files directories, and partitions stored on disks, including the computers home disk.
Disk 0 is always the home disk, disks loaded after will be given simple ids that won't change when disks are added or removed, but don't persist during computer reboots.

The files api does not read or write to files directly, instead it opens [file headers](/apis/files/headers.md) that preform these interactions.
File paths in need are formatted <partition>:/<filepath>, disks with one partition don't require specification.

## Disk capacity

Every disk has a fixed size, 10 MiB by default, set by the server's `disk-capacity` config option and shared by all disks on the server. Writes that would grow a file past the remaining space fail with `"Disk full"` rather than filling the machine the game runs on.

The size is per disk, not per partition: partitions share the disk's capacity, and `getCapacity`/`getFreeSpace` report the whole disk even when given a partition name.

## Functions

### getPartitions(disk = 0)
Returns a list of partition names belonging to the filesystem.

`returns: String[]`

### getPartition(name, disk = 0)
Sends a GET request to the given url with the supplied headers, which must be provided as strings.
Returns an id that can be used to identify the reply event.

```
returns {
    "name": String,
    "readonly": Boolean,
    "hidden": Boolean
} | Nil
```

### createPartition(name, disk = 0)
Creates a non-hidden, writable partition with the given name, if available. And indicates if the partition was created.

`returns: Boolean`

### deletePartition(name, disk = 0)
Attempts to delete a partition with the given name.

`returns: Boolean`

### setPartitionHidden(name, state, disk = 0)
Sets the given partition's hidden state to that given, if it exists. Notes that being hidden has no effect itself and is more individual programs to process (so completely useless, but I already added it so whatever).

`returns: Boolean`

### setPartitionReadOnly(name, disk = 0)
Mark the given partition as read only, after its contents won't be editable.

`returns: Boolean`

### open(path, mode='r', disk = 0)
Opens a [file header](/apis/files/headers) under the given file mode.

Nonexistent files or invalid paths will still open file headers unless `path` is set, so check the file exists before opening a header.

`returns: {String : Function}`

### open(path, mode='r', flags, disk = 0)
Opens a [file header](/apis/files/headers) under the given file mode.

The flags argument can select additional criteria for the open operation:

```
{
    "exclusive": Boolean,   -- fail if the path already exists, creating it otherwise
    "follow": Boolean,      -- false rejects symlinks with "Operation not supported"
    "directory": Boolean,   -- require a directory, which can never be opened as a header
    "path": Boolean         -- require the path to already exist
}
```

Tip: `exclusive` allows you to cancel am operation if a file already exists, while `w` silently truncates whatever is already there, so two programs can both "acquire" the same lock file. Using exclusive however will make the second operation fail instead.

Nonexistent files or invalid paths will still open file headers unless `path` is set, so check the file exists before opening a header.

`returns: {String : Function}`

### fsSize(path, disk = 0)
Gets the total and free size of the disk holding the path, in bytes. This reports the disk's own capacity (see [disk capacity](#disk-capacity)), not the free space of the machine the game runs on.

```
returns {
    "total": Integer,
    "free": Integer
}
```

### getCapacity(disk = 0, partition = nil)
Gets the total size of the disk in bytes.

When a partition is given it must name a real partition on the disk, but the size returned is always the whole disk's.

`returns: Integer, String | Nil`

### getFreeSpace(disk = 0, partition = nil)
Gets the unused size of the disk in bytes.

As with `getCapacity`, the partition argument is validated but the figure covers the whole disk.

`returns: Integer, String | Nil`

### truncate(path, size, disk = 0)
Resizes the file to `size` bytes without opening a header. Growing the file fills the new space with zero bytes.
Raises an error if the new size would exceed the disk's remaining capacity.

`returns: Boolean`

### getChildren(path, disk = 0)
Assuming the path is a directory, will list all of its subdirectories.

`returns: String[]`

### makeDir(path, disk = 0)
Attempts to make directory at the path.

`returns: Boolean`

### exists(path, disk = 0)
Checks if the path contains data.

`returns: Boolean`

### isFile(path, disk = 0)
Checks if the file first exists and then is a file / not a directory.

`returns: Boolean`

### isDir(path, disk = 0)
Checks if the file first exists and then is not a file / a directory.

`returns: Boolean`

### delete(path, disk = 0)
Attempts to delete the data at the path and returns if the operation was a success.

Will recursively delete the contents of targeted directories.

`returns: Boolean`

### diskExists(disk)
Checks if the disk exists.

`returns: Boolean`

### getNumberOfDisks()
Gets the number of disks attached to the system.

`returns: Integer`

### getDisks()
Gets a list of all simple disk ids, not to be confused with the disks' UUIDs.

`returns: Integer[]`

### getDiskReaderID(disk)
Gets the UUID of the device reading the disk, An example UUID would be `"e58ed763-928c-4155-bee9-fdbaaadc15f3"`.

`returns: String`

### getDiskID(disk)
Gets the inherent UUID of the disk itself, An example UUID would be `"e58ed763-928c-4155-bee9-fdbaaadc15f3"`.

`returns: String`

### removeDisk(disk)
Attempts to detach the disk, will always fail to delete the home disk.

`returns: Boolean`

### getBootPath(disk)
Gets the entrypoint for a disk or nil if the disk is not bootable.

`returns: String | nil`

### setBoot(entrypoint, disk)
Attempts to set the boot data of a disk, will preform an additional safety check to ensure the entrypoint exists exclusively for the home disk.
A disks boot data determines where the entrypoint will be if the disk is run by a computer.
Reloading a computer will cause the changed setBoot path to take effect.

`returns: Boolean`

### setBoot(disk)
Attempts to remove boot information from a disk, will always fail for the home disk.

`returns: Boolean`