Huzaifa Zulfiqar Rajput K21-3010

Step1: We must first download the following modules: 
• GCC installation through sudo apt-get 
• sudo apt-get install bison
• sudo apt-get install libncurses5-dev
• apt-get sudo install flex
• sudo apt install make
• sudo apt-get install libssl-dev
• sudo apt-get install libelf-dev
• sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main universe"
• sudo apt-get update
• sudo apt-get upgrade

Step2: Inside the kernel directory make a new folder "hello"
![image](https://user-images.githubusercontent.com/125996317/222536354-352c535c-2dd7-4c8d-8b97-ff461e530910.png)

Step3: Adding a C code for system call


![image](https://user-images.githubusercontent.com/125996317/222536610-83a9c20d-8ef4-4fad-af8f-dbf492e91a2a.png)


Explaination of code:
1. Because we are developing a system call for our Linux kernel, we used the #include linux/kernel> directive.
2. Amslinkage just indicates that the arguments to this function will be on the stack rather than in the CPU registers.
3. Because we'll be printing to the kernel's log file, Printk is chosen over Printf.
4. The programme ran properly if the code is executed and returns 0, in which case Hello World will be recorded in the kernel's log file.

Step4: Create a Makefile for C code


![image](https://user-images.githubusercontent.com/125996317/222537235-5c8db174-b2b7-43b0-96b1-f4d088af16bc.png)



Step5: Adding a new code into the system table


we have to add the system call entry into the syscall_64.tbl file which keeps the name of all the system calls in
our system.


![image](https://user-images.githubusercontent.com/125996317/222537553-d51abadb-6d74-4e83-9aee-6aaf65ba8a37.png)


Step6: Adding the prototype of the new system call into the system calls header file


![image](https://user-images.githubusercontent.com/125996317/222537794-91b4c097-b39e-49a6-8f43-1817eb5f1d01.png)


Step7: Changing version and adding the hello folder in the kernel’s Makefile


![image](https://user-images.githubusercontent.com/125996317/222538035-d840e83a-1da7-48e8-b2d4-66065740adbd.png)


Step8: Create a config file


![image](https://user-images.githubusercontent.com/125996317/222538457-9e654759-7886-4187-8d71-c7e57047ef47.png)


Step9: Compile the kernel using "make -j(number of processor given to linux)" command


![image](https://user-images.githubusercontent.com/125996317/222539301-83546e1e-b48c-42c9-ab24-304dfb08ca5b.png)


![image](https://user-images.githubusercontent.com/125996317/222539402-2a6837ac-1e13-4805-bceb-b447e1c59abe.png)


![image](https://user-images.githubusercontent.com/125996317/222539694-9f840bcb-f4e1-49a6-94ca-d67de7a9e7fd.png)


Step10: Installing modules

By entering "make modules install install," which will install the kernel and update our grub, we must now install the kernel that we generated. When everything is finished and the terminal displays "done," we can either manually restart our laptop or do so by entering "shutdown -r now".


![image](https://user-images.githubusercontent.com/125996317/222540517-eaef2ee6-95dd-42f6-bc97-a55c745cd6ec.png)


![image](https://user-images.githubusercontent.com/125996317/222540602-98c93d93-af28-4325-bd9c-4360c5512852.png)


![image](https://user-images.githubusercontent.com/125996317/222540735-d1b96d2b-2c4b-464f-9424-ae6b2bb33d83.png)


Step11: Checking if the System call is Working Properly

After logging into the newly compiled kernel, we check the system call by making a C code named “userspace.c” and putting the following code in it:
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
it returns 0,


![image](https://user-images.githubusercontent.com/125996317/222541256-e8f26b8e-c971-4f41-a158-7e4a2d65b355.png)


![image](https://user-images.githubusercontent.com/125996317/222541279-54b0de1f-7a3b-47f4-b887-09be50b92970.png)


![image](https://user-images.githubusercontent.com/125996317/222541314-f364b168-0b07-47cc-91c1-c4e9cabc2275.png)


![image](https://user-images.githubusercontent.com/125996317/222541366-675f2193-1419-4362-aad2-5509c4db4a2e.png)



