# Char device driver

This kernel device driver named `/dev/serene` allows the user to read, write, replace, clear data from a kernel buffer. 
Please make sure the kernel version is ****, otherwise it results in a compilation error.

## Compiling and Insert/Remove Kernel Module 
- Kernel module `chardev.c` needs to be compiled using the given Makefile with the command `make`
- Insert the kernel module before executing the userprocess.c with `insmod chardev.ko`
- Once the kernel module is inserted, it can be removed using `rmmod chardev.ko`
- The compiled userprocess (a.out) must be executed with `sudo ./a.out` to avoid permission issues

## How to run the user space program?

The user must specify the kernel `buffer_size` and the read/write `data_size` before proceeding with the device operations. The implemented char device gives the user with the following options:

- Write (1)
- Read (2)
- Empty (3)
- Display (4)

### Write

    - The buffer write is always sequential. At any given time, the user can only write `data_size` bytes. If the write input size is greater than `data_size`, only the first `data_size` bytes will be considered. If the buffer is full, the subsequent writes will overwrite the exisiting buffer content.

### Read

    - This option lets the user to read `data_size` bytes at a time. The subsequent reads  point to the next available data. The user is also provided with the following options on what to do with the read data:
        - Clear the read data [c]: User can clear the currently read data. This option frees up the buffer space for some new writes. 
        - Replace the read data [r]: User can replace the currently read data with a new data. 
        - Simply Ignore the read data [n]: No action is taken, only for the monitoring purpose.


### Empty

    - The user can clear the entire content of buffer using this option. 

### Display

    - To view the current content of the buffer, this option must be utilized.

