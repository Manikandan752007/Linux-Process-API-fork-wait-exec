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
#include <sys/types.h>
#include <unistd.h>
int main(void)
{	gcc 
	pid_t process_id;
	pid_t p_process_id;
	process_id = getpid();
	p_process_id = getppid();


	printf("The process id: %d\n",process_id);
	printf("The process id of parent function: %d\n",p_process_id);
	return 0;
 }
```
## OUTPUT :
<img width="697" height="226" alt="image" src="https://github.com/user-attachments/assets/33c35d82-75e4-4219-b778-4d6e49199e0f" />


## C Program to create new process using Linux API system calls fork() and exit()
## CODE :
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>  

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        exit(1);
    }

    if (pid == 0) {
        printf("I am child, my PID is %d\n", getpid());
        printf("My parent PID is: %d\n", getppid());
        sleep(2);  
    } else {
        printf("I am parent, my PID is %d\n", getpid());
        wait(NULL);  
    }

    return 0;
}

```

## OUTPUT
<img width="576" height="240" alt="image" src="https://github.com/user-attachments/assets/78bcad83-aa98-480f-840d-f719c0329131" />






## C Program to execute Linux system commands using Linux API system calls exec() family
## CODE

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    int status;
    pid_t pid;
    printf("Running ps with execl (no path)\n");
    pid = fork();
    if (pid == 0) {
        execl("ps", "ps", "ax", NULL);  
        perror("execl failed");
        exit(1);
    } else {
        wait(&status);
        if (WIFEXITED(status))
            printf("Child exited with status of %d\n", WEXITSTATUS(status));
        else
            puts("Child did not exit successfully");
    }

    printf("Running ps with execl (with /bin/ps path)\n");
    pid = fork();
    if (pid == 0) {
        execl("/bin/ps", "ps", "ax", NULL); 
        perror("execl failed");
        exit(1);
    } else {
        wait(&status);
        if (WIFEXITED(status))
            printf("Child exited with status of %d\n", WEXITSTATUS(status));
        else
            puts("Child did not exit successfully");
    }

    printf("Done.\n");
    return 0;
}


```

## OUTPUT
<img width="948" height="808" alt="image" src="https://github.com/user-attachments/assets/b3588e1c-5a69-423b-bdbc-db48b53d86f4" />

<img width="927" height="794" alt="image" src="https://github.com/user-attachments/assets/f7314e25-6576-4e76-907e-14061b43238a" />


<img width="938" height="759" alt="image" src="https://github.com/user-attachments/assets/d9d14962-8bc5-4a86-852a-81000cf6d127" />

# RESULT:
The programs are executed successfully.
