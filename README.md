# Char device driver

The kernel device driver `/dev/serene` allows the user to read, write, replace, clear, empty, display data from a kernel buffer. 
Please make sure the kernel version is blah to avoid compilation issues. 

## Compilation/Insert/Remove Kernel Module 

- Kernel module `chardev.c` needs to be compiled using the given Makefile with the command `make`
- Insert the kernel module before executing the userprocess.c with `insmod chardev.ko`
- Once the kernel module is inserted, it can be removed using `rmmod chardev.ko`

## How to run the user space program?

- The compiled userprocess `gcc userprocess.c` (a.out) must be executed with `sudo ./a.out` to avoid permission issues
- The user must specify the kernel `buffer_size` and the read/write `data_size` before proceeding with any device operations. The implemented char device gives the user with the following options:

    - Write (1)
    - Read (2)
    - Empty (3)
    - Display (4)

### Write

- The buffer write is always sequential. At any given time, the user can only write `data_size` bytes. If the write input size is greater than `data_size`, only the first `data_size` bytes will be considered. If the buffer is full, the subsequent writes will overwrite the exisiting buffer content.

### Read

- Unlike write, the read doesn't have to be sequential, it reads only the valid data by skipping the holes (Zeroes). This option lets the user to read valid `data_size` bytes at a time. The subsequent read point to the next available valid data. If all the data in the buffer has been read, the read operation starts again from beginning of the buffer.
 The user is also provided with the following options on what to do with the read data:
    - Clear the read data [c]: User can clear the currently read data. This option frees up the buffer space for some new writes. 
    - Replace the read data [r]: User can replace the currently read data with a new data of `data_size` bytes.
    - Simply Ignore the read data [n]: No action is taken, only for the monitoring purpose.


### Empty

- The user can clear the entire content of buffer. 

### Display

- The user can view the current content of the buffer at any point in time.

### Sample I/O Ops
`make`

`insmod chardev.ko`

`gcc userprocess.c -o user`

`./user`

### Possible Test cases
1. `buffer size empty`
2. `data size allocator larger than buffer size`
3.`writing into full/empty buffer with below cases`
   `writing lesser than data-size`
   `writing size greater than data-size`
   `replacing lesser than data-size`
   `replacing size greater than data-size`
4. `Reading into full/empty buffer with below cases`
      `reading size greater than data-size`
      `reading size lesser than data-size`
5. `clear`
      `clearing data size == datasize`
      `clearing data size < datasize`
6. `Read from empty buffer`
7. `Clearing empty buffer`
