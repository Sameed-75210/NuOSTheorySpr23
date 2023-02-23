Programmer: Muahammad Sameed
Roll no: K21-3100


**Step 01:**
First we need to download these modules:
• sudo apt-get install gcc
• sudo apt-get install libncurses5-dev
• sudo apt-get install bison
• sudo apt-get install flex
• sudo apt install make
• sudo apt-get install libssl-dev
• sudo apt-get install libelf-dev
• sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main
universe"
• sudo apt-get update
• sudo apt-get upgrade



**Step 02: Making a new folder called hello:**



![image](https://user-images.githubusercontent.com/92264901/221014564-720c250d-d560-48ea-ae4c-0e8ad43ed090.png)


**Step 03:** Adding a C code for the system call:


![image](https://user-images.githubusercontent.com/92264901/221016370-ac3cea25-edbc-4224-ba82-c57b4fc0def7.png)

**Code explanation:**


a. We used #include <linux/kernel> because we are building a system call for our linux kernel.


b. Amslinkage simply means that the arguments for this function will be on the stack instead of the CPU registers.


c. Printk is used instead of printf because we are going to print in the kernel’s log file.


d. If the code is run and it returns 0, then it will mean that our program ran successfully
and Hello world is written to out kernel’s log file.



**Step 04:** : **Creating a Makefile for the C code:**


![image](https://user-images.githubusercontent.com/92264901/221016539-e33cfd59-e48e-4a44-8f76-a734f751bba1.png)
![image](https://user-images.githubusercontent.com/92264901/221016606-52fdb314-2987-40d6-a88c-5362ebcfebf7.png)

**Step 05:** **Adding the new code into the system table file:**


![image](https://user-images.githubusercontent.com/92264901/221016685-4a120949-fcee-4423-9601-15527b71d87b.png)

**Step 06:** **Adding the prototype of the new system call into the system calls header file:**


![image](https://user-images.githubusercontent.com/92264901/221016844-d8d12f7f-ad5e-4325-8f53-c4dd9c9b66aa.png)

**Step 07:** **Changing version and adding the hello folder in the kernel’s Makefile:**

![image](https://user-images.githubusercontent.com/92264901/221017066-b8663cfd-69fd-4cf6-bb03-cbd88d094219.png)

![image](https://user-images.githubusercontent.com/92264901/221017093-0e6b79f1-3087-440c-9405-102420db445b.png)


**Step 08:** **Creating a config file:**

![image](https://user-images.githubusercontent.com/92264901/221019800-d0a41e10-713e-4973-a11a-f4e30208b8c2.png)


![image](https://user-images.githubusercontent.com/92264901/221019843-475deb87-19c8-4865-bd14-1682c88f0655.png)

**Step 09:** **Cleaning and Compiling the kernel:**

![image](https://user-images.githubusercontent.com/92264901/221020053-f6fa17e4-ad74-4fdd-b426-e2bffc6916cc.png)


![image](https://user-images.githubusercontent.com/92264901/221020474-57890f9a-1c66-4d34-92f6-319ddb1b10dc.png)

**Step 10:** **Checking if the System call is Working Properly:**

After logging into the newly compiled kernel, we check the system call by making a C code

named “userspace.c” and putting the following code in it:

#include <stdio.h>

#include <linux/kernel.h>
#include <sys/syscall.h>
#include <unistd.h>
int main()
{
long int i = syscall(335);
printf("System call sys_hello returned %ld\n", i);
return 0;
}
Now we compile the code by typing “gcc userspace.c” and executing it by typing “./a.out”. If
it returns 0, this means that our code has compiled successfully and the system call is
working fine (Note that in calling syscall(335), 335 is the number where we added our
system call in the table) and finally, we run “dmesg” to see the kernel messages and we will
find “Hello World” written at the end of it.


![image](https://user-images.githubusercontent.com/92264901/221020967-c0dcb20d-245c-4f20-8864-f92a086d1dbe.png)


![image](https://user-images.githubusercontent.com/92264901/221021032-8d3fd9a5-381d-4ef5-a515-a01c29d36147.png)


