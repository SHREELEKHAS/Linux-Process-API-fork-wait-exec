## SHREE LEKHA.S 212223110052
# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

int main(void) {
    // Variables to store process IDs
    pid_t process_id;
    pid_t p_process_id;

    // Get the process ID and parent process ID
    process_id = getpid();    // Returns process ID of the calling function
    p_process_id = getppid(); // Returns process ID of the parent function

    // Print the process IDs
    printf("The process ID: %d\n", process_id);
    printf("The parent process ID: %d\n", p_process_id);

    return 0;
}

```
##OUTPUT

![Screenshot 2024-09-16 105852](https://github.com/user-attachments/assets/0d798e9e-ce11-455d-9daf-26ccbd6df6ad)



![Screenshot 2024-09-16 105622](https://github.com/user-attachments/assets/2a4faa7b-0ff2-4c77-8a8c-1a4d9694a272)


## C Program to create new process using Linux API system calls fork() and exit()
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid;

    // Fork to create a new process
    pid = fork();

    if (pid == 0) {
        // Child process
        printf("I am child, my PID is %d\n", getpid());
        printf("My parent PID is: %d\n", getppid());
        exit(0);
    } else {
        // Parent process
        printf("I am parent, my PID is %d\n", getpid());
        sleep(100); // Delays parent termination to show active child process
        exit(0);
    }
}

```
##OUTPUT
![Screenshot 2024-09-16 105924](https://github.com/user-attachments/assets/96af5340-2609-4033-8387-a6ba1c8de2b8)



![Screenshot 2024-09-16 105642](https://github.com/user-attachments/assets/afc22769-4161-401a-8b49-88c665742f53)





## C Program to execute Linux system commands using Linux API system calls exec() family
```
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
#include <stdio.h>

int main() {
    int status;

    // Executing 'ps' command without specifying the path
    printf("Running 'ps' with execlp\n");
    execlp("ps", "ps", "ax", NULL); // Using execlp to execute the 'ps' command
    wait(&status);  // Wait for the child process to finish

    if (WIFEXITED(status))
        printf("Child exited with status %d\n", WEXITSTATUS(status));
    else
        printf("Child did not exit successfully\n");

    printf("Done.\n");

    // Executing 'ps' command by specifying the path
    printf("Running 'ps' with execlp. Now with path specified\n");
    execl("/bin/ps", "ps", "ax", NULL); // Specifying the full path of 'ps' command
    wait(&status);  // Wait for the child process to finish

    if (WIFEXITED(status))
        printf("Child exited with status %d\n", WEXITSTATUS(status));
    else
        printf("Child did not exit successfully\n");

    printf("Done.\n");

    exit(0);
}

```
##OUTPUT
![Screenshot 2024-09-16 105940](https://github.com/user-attachments/assets/9d177fed-7dbb-4f78-ad3b-b2137676bcc4)


![Screenshot 2024-09-16 105717](https://github.com/user-attachments/assets/710d8846-3dcf-4979-9d71-5452742a591e)


# RESULT:
The programs are executed successfully.
