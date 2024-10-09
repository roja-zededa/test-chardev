# Char device driver

This kernel device driver named `/dev/serene` allows the user to read, write, replace, clear data from a kernel buffer. 
Please make sure the kernel version is ****, otherwise it results in a compilation error.

## Compiling and Insert/Remove Kernel Module 
- Kernel module `chardev.c` needs to be compiled using the given Makefile with the command `make`
- Insert the kernel module before executing the userprocess.c with `insmod chardev.ko`
- Once the kernel module is inserted, it can be removed using `rmmod chardev.ko`
- The compiled userprocess (a.out) must be executed with `sudo ./a.out` to avoid permission issues

## How to run the user space program?

The user must specify the kernel `buffer\_size` and the read/write `data\_size` before proceeding with the device operations. The implemented char device gives the user with the following options:

- write (1)
- read (2)
- replace (3)
- clear (4)
- empty (5)
- display (6)

### write

- The buffer write is always sequential. At any given time, the user can only write `data\_size` bytes. If the write input size is greater than `data\_size', only the first `data\_size` bytes will be considered. If the buffer is full, the subsequent writes will overwrite the exisiting buffer content.
