

# ASSIGNMENT # 1
## About me

Muhammad Rayyan Ahmed (21k-3079), enrolled in FAST nuces currently in my 4th semester 

## About assignment

### Hello world system call

Operating system assignment where we have to implement Hello World system call and configure the kernel so that when we type -uname -r, it will display our roll number as kernel version.




## Installation

All the installtions required are given below

```bash
sudo apt-get install gcc
sudo apt-get install libncurses5-dev
sudo apt-get install bison
sudo apt-get install flex
sudo apt install make
sudo apt-get install libssl-dev
sudo apt-get install libelf-dev
sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) mainuniverse"
sudo apt-get update
sudo apt-get upgrade
```
    
## Steps

1) Existing kernel version

![App Screenshot](https://user-images.githubusercontent.com/124567636/222946374-b7796cae-82ce-48f4-955d-3f8e7b498905.png)

2) Downloading kernel version 4.19.275 from https://www.kernel.org

![App Screenshot](https://user-images.githubusercontent.com/124567636/222946491-648227de-cf5b-4a57-a194-fa0e7d1eb539.png)

3) Extract the kernel version (I have already extracted it)

![App Screenshot](https://user-images.githubusercontent.com/124567636/222947101-d26572ce-f1af-445f-b51e-3e0ec28020a0.png)

4) Create a new folder named 'hello' where you just extracted kernel.

![App Screenshot](https://user-images.githubusercontent.com/124567636/222947156-44a8c5cd-5681-4b47-8bf2-4cb90a1210ff.png)

5) Goto the folder we just created and create a new C code file by typing “gedit hello.c” and paste the following code there: 

#include <linux/kernel.h>

asmlinkage long sys_hello(void)
{

printk("Hello world\n");

return 0;

}

6) Type in terminal, “gedit Makefile” and put “obj-y := hello.o” 

![App Screenshot](https://user-images.githubusercontent.com/124567636/222947376-d35b5476-4c19-4e1c-997f-682edd548b1f.png)

7) Add new code to the system table file highlighted in Screenshot
We can go to our kernel directory by using cd and then edit the file by typing “gedit syscall_64.tbl”
![App Screenshot](https://user-images.githubusercontent.com/124567636/222947520-9be2bb15-f1fd-48d0-a6a1-a303a095d988.png)

8) Adding the prototype of the new system call into the system calls header file:
Now we have to add the prototype of our system call in the system’s header file which islocated in the kernel folder then “/include/linux/syscalls.h”. We have to add the prototype of our system call function in this file.

![App Screenshot](https://user-images.githubusercontent.com/124567636/222947792-a8a177e5-2425-4790-a13f-ec5a88f15023.png)

9) Changing version and adding the hello folder in the kernel’s Makefile:
Now, we have to add our roll number in the extraversion of the kernel’s make file and wehave to add the new module that we created into our kernel’s make file. For this, we open the Makefile of the kernel and search for “core-y” and add hello/ as highlight in screenshot 
![image](https://user-images.githubusercontent.com/124567636/222948279-2e533ead-d174-4708-a7cd-57b6d541210b.png)

10) Creating a config file:
We search for the config that we currently have by typing “ls /boot | grep config” and the we copy the config that is shown to us by typing “cp /boot/config-4.15.0-112-generic our linux kernel directory”. Then we create the old config by typing “yes "" | make oldconfig -j4”

![image](https://user-images.githubusercontent.com/124567636/222948357-e5fff0ac-2c0b-4e63-998d-6479b0164685.png)

11) Cleaning and Compiling the kernel:
We delete all of our old object and executable files by typing “make clean -j4” when this is done, we type “make -j4” to start building our kernel.

Note: This step is time consuming and can take upto hours

The screenshot is taken after the compiling has been completed 

![image](https://user-images.githubusercontent.com/124567636/222948654-810ba632-6fec-4549-8978-722227d1bc09.png)

12) Installing modules:

Now we have to install the kernel that we built by typing “make modules_install install” which will install the kernel and update our grub as well. When this all is done and the terminal says “done”, then we can restart our system by typing “shutdown -r now” and hold the “Shift” key while it is restarting to open up the grub menu and switch to the new kernel which we just installed.

The screenshot is taken after the installation has been completed 

![image](https://user-images.githubusercontent.com/124567636/222948828-178572fd-6029-4445-a97a-767dc8cab39a.png)

13) Checking the system:

Now type uname -r to see if the kernel version name changed.

Here it displays 213079 which is my roll number (21k-3079)

![image](https://user-images.githubusercontent.com/124567636/222948908-a80ea48e-0208-4209-b71a-cb7e9bd4c731.png)

We check the system call by making a C code
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

Now we compile the code by typing “gcc userspace.c” and executing it by typing
“./a.out”. If it returns 0, this means that our code has compiled successfully and the system call is working fine

![image](https://user-images.githubusercontent.com/124567636/222949872-bddcae98-0cd9-4561-9ca5-84ee12c4bdbc.png)

14) Hello world system call:

Finally we run “dmesg” to see the kernel messages and we will
find “Hello World” written at the end of it.

![image](https://user-images.githubusercontent.com/124567636/222949935-ccf183ac-b046-4dda-9d7b-21a3af56fc20.png)












