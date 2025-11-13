# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

```
DEVELOPED BY:
NAME: MANIKANDAN M
REG NO:212224040184
```

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

## C Program to print process ID and parent Process ID using Linux API system calls
# PROGRAM:



## CODE :
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h> 

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(5); 
    } else if (pid > 0) { 

        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL);
    } else {
        
        perror("Fork failed");
        exit(1);
    }

    return 0;
}




```


## OUTPUT :


<img width="617" height="484" alt="Screenshot 2025-11-13 214824" src="https://github.com/user-attachments/assets/6be60592-ac5a-4594-96df-ab7c23060600" />



## C Program to create new process using Linux API system calls fork() and exit()
## CODE :
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    int status;
    pid_t pid;

    printf("Running ps with execl (without full path, expected to fail)\n");
    
    pid = fork(); 
    if (pid == 0) {
        
        execl("ps", "ps", "ax", NULL);
        perror("execl failed");
        exit(1);
    } else if (pid > 0) {
      
        wait(&status);
        if (WIFEXITED(status))
            printf("Child exited with status %d\n", WEXITSTATUS(status));
        else
            puts("Child did not exit successfully");
    } else {
        perror("fork failed");
        exit(1);
    }

    printf("Running ps with execl (with full path)\n");

    pid = fork(); 
    if (pid == 0) {
       
        execl("/bin/ps", "ps", "ax", NULL); // 
        perror("execl failed");
        exit(1);
    } else if (pid > 0) {
       
        wait(&status);
        if (WIFEXITED(status))
            printf("Child exited with status %d\n", WEXITSTATUS(status));
        else
            puts("Child did not exit successfully");
    } else {
        perror("fork failed");
        exit(1);
    }

    printf("Done.\n");
    return 0;
}

   

```
## OUTPUT

<img width="719" height="299" alt="Screenshot 2025-11-13 214901" src="https://github.com/user-attachments/assets/72575ae5-27a5-4fa1-8fd3-18e36c734155" />


<img width="728" height="770" alt="Screenshot 2025-11-13 215128" src="https://github.com/user-attachments/assets/96c0e84e-0503-4b1c-a6f9-4f07fbb69f07" />

<img width="717" height="751" alt="Screenshot 2025-11-13 215214" src="https://github.com/user-attachments/assets/d57b1c33-79f3-4eb9-9a4a-3f7007f7fc93" />


<img width="821" height="757" alt="Screenshot 2025-11-13 215231" src="https://github.com/user-attachments/assets/8f029a27-e8e1-4e1c-b03b-a030e2b38cd4" />





## C Program to execute Linux system commands using Linux API system calls exec() family
## CODE
```
//C Program to execute Linux system commands using Linux API system calls exec() family
//
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;

    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);

    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }

    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);

    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }

    printf("Done.\n");
    return 0;
}




```

## OUTPUT

<img width="838" height="310" alt="Screenshot 2025-11-13 215351" src="https://github.com/user-attachments/assets/5044d2c9-1a12-416d-9032-84a14cfc8e08" />



# RESULT:
The programs are executed successfully.
