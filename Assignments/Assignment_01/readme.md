Programmer: Muahammad Sameed Roll no: K21-3100

Step 01: First we need to download these modules: • sudo apt-get install gcc • sudo apt-get install libncurses5-dev • sudo apt-get install bison • sudo apt-get install flex • sudo apt install make • sudo apt-get install libssl-dev • sudo apt-get install libelf-dev • sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main universe" • sudo apt-get update • sudo apt-get upgrade

Step 02: Making a new folder called hello:

![image](https://user-images.githubusercontent.com/92264901/221030357-d9de26bd-4759-4577-ac36-4c77187342ce.png)

Step 03: Adding a C code for the system call:

![image](https://user-images.githubusercontent.com/92264901/221030422-caa2df85-2809-416f-b4d6-f7a5b18d4b42.png)

Code explanation:

a. We used #include <linux/kernel> because we are building a system call for our linux kernel.

b. Amslinkage simply means that the arguments for this function will be on the stack instead of the CPU registers.

c. Printk is used instead of printf because we are going to print in the kernel’s log file.

d. If the code is run and it returns 0, then it will mean that our program ran successfully and Hello world is written to out kernel’s log file.

Step 04: : Creating a Makefile for the C code:

![image](https://user-images.githubusercontent.com/92264901/221030506-93c0af3f-08b9-4bdc-8484-a11a8c465a12.png)
![image](https://user-images.githubusercontent.com/92264901/221030557-af5f7d3f-9907-4c7f-8b54-3062b6a99f63.png)

Step 05: Adding the new code into the system table file:

![image](https://user-images.githubusercontent.com/92264901/221030622-3088d792-1bea-4773-96a0-9892270c0c7c.png)

Step 06: Adding the prototype of the new system call into the system calls header file:

![image](https://user-images.githubusercontent.com/92264901/221030669-62341882-3bad-4317-a776-5504beea4e50.png)

Step 07: Changing version and adding the hello folder in the kernel’s Makefile:

![image](https://user-images.githubusercontent.com/92264901/221030715-d5c0a02a-28bb-4d07-ad27-8f3fd68017f2.png)

![image](https://user-images.githubusercontent.com/92264901/221030745-e9d0df33-e819-4ea7-b506-34167cc762d8.png)

Step 08: Creating a config file:

![image](https://user-images.githubusercontent.com/92264901/221030836-b229f5be-b8cb-4b2d-a20c-fe44f4b7cefb.png)

![image](https://user-images.githubusercontent.com/92264901/221030876-2f7d73e5-75cc-4e03-837b-f06a74db60be.png)

Step 09: Cleaning and Compiling the kernel:

![image](https://user-images.githubusercontent.com/92264901/221030937-b707c7f8-f19b-4cf3-ae23-ec384dd97327.png)

![image](https://user-images.githubusercontent.com/92264901/221030968-f0ad1e1d-f973-49fc-bdb2-aefc9e1e1b4a.png)

Step 10: Checking if the System call is Working Properly:

After logging into the newly compiled kernel, we check the system call by making a C code

named “userspace.c” and putting the following code in it:

#include <stdio.h>

#include <linux/kernel.h> #include <sys/syscall.h> #include <unistd.h> int main() { long int i = syscall(335); printf("System call sys_hello returned %ld\n", i); return 0; } Now we compile the code by typing “gcc userspace.c” and executing it by typing “./a.out”. If it returns 0, this means that our code has compiled successfully and the system call is working fine (Note that in calling syscall(335), 335 is the number where we added our system call in the table) and finally, we run “dmesg” to see the kernel messages and we will find “Hello World” written at the end of it.

![image](https://user-images.githubusercontent.com/92264901/221031030-f45bdf03-5190-457f-bca5-5304d4fe821f.png)

![image](https://user-images.githubusercontent.com/92264901/221031070-7b07ea7f-5e4e-4a6f-902f-f832916d4254.png)
