// #include "kernel/types.h"
// #include "kernel/stat.h"
// #include "user/user.h"
#include <assert.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_PROC 10
struct pinfo {
int ppid;
int syscall_count;
int page_usage;
};

int sysinfo(int param){
    long numberOfProc;
    if(param==0){
        FILE *fp;
    char size[256];
     

    const char command[] ="ps -AL --no-headers | wc -l";

    size_t bufsize = sizeof(size);

    // add dynamic allocation here

memset(size, 0, bufsize);

    if ((fp = popen(command, "r")) == NULL) {
        printf("Error opening pipe!\n");
        exit(-__LINE__);
    }


    while (fgets(&size[strlen(size)], bufsize - strlen(size), fp) != NULL);

    if(pclose(fp))  {
        printf("Command not found or exited with error status\n");
        exit(-__LINE__);
    }
        if (sscanf(size, "%ld", &numberOfProc) != 1) {
        exit(-__LINE__);
    }
    printf("Number of processes : %ld\n", numberOfProc);
return numberOfProc;
    }
    if(param==1){
        long withoutCurrentProc=numberOfProc-1;
        printf("Number of processes without current : %ld\n", withoutCurrentProc);
        return withoutCurrentProc;
    }
    
    else
    printf("-1");
}
int main()
{
int n_active_proc, n_syscalls, n_free_pages;
n_active_proc = sysinfo(0);
n_syscalls = sysinfo(1);
// n_free_pages = sysinfo(2);
printf("[sysinfo] active proc: %d, syscalls: %d, free pages: %d\n",
n_active_proc, n_syscalls, n_free_page
)
}
