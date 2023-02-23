

Programmer: Muahammad Sameed Roll no: K21-3100

Step 01: First we need to download these modules: • sudo apt-get install gcc • sudo apt-get install libncurses5-dev • sudo apt-get install bison • sudo apt-get install flex • sudo apt install make • sudo apt-get install libssl-dev • sudo apt-get install libelf-dev • sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main universe" • sudo apt-get update • sudo apt-get upgrade

Step 02: Making a new folder called hello:

image

Step 03: Adding a C code for the system call:

image

Code explanation:

a. We used #include <linux/kernel> because we are building a system call for our linux kernel.

b. Amslinkage simply means that the arguments for this function will be on the stack instead of the CPU registers.

c. Printk is used instead of printf because we are going to print in the kernel’s log file.

d. If the code is run and it returns 0, then it will mean that our program ran successfully and Hello world is written to out kernel’s log file.

Step 04: : Creating a Makefile for the C code:

image image

Step 05: Adding the new code into the system table file:

image

Step 06: Adding the prototype of the new system call into the system calls header file:

image

Step 07: Changing version and adding the hello folder in the kernel’s Makefile:

image

image

Step 08: Creating a config file:

image

image

Step 09: Cleaning and Compiling the kernel:

image

image

Step 10: Checking if the System call is Working Properly:

After logging into the newly compiled kernel, we check the system call by making a C code

named “userspace.c” and putting the following code in it:

#include <stdio.h>

#include <linux/kernel.h> #include <sys/syscall.h> #include <unistd.h> int main() { long int i = syscall(335); printf("System call sys_hello returned %ld\n", i); return 0; } Now we compile the code by typing “gcc userspace.c” and executing it by typing “./a.out”. If it returns 0, this means that our code has compiled successfully and the system call is working fine (Note that in calling syscall(335), 335 is the number where we added our system call in the table) and finally, we run “dmesg” to see the kernel messages and we will find “Hello World” written at the end of it.

image

image

