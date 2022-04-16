---
title: wstat macro
layout: post
guid: urn:uuid:af6a07d7-bda3-467c-8801-2c65a64f303d
tags:
  - codes
---

在进程间通信时，经常使用wait(int* status)或waitpid(pid_t pid, int* status, int options)来等待子进程中断或结束。其中status这个参数标识子进程的结束状态。我们可以通过wstat宏来对其进行判断。


```c
    #include <sys/wait.h>
    /* int status */
    WIFEXITED(status)   /* 如果子进程正常结束则为非0值 */
    WEXITSTATUS(status)   /* 取得子进程由exit()返回的结束代码，一般会先用WIFEXITED来判断是否正常结束才能使用这个宏 */
    WIFSINGNALED(status)   /* 如果子进程是因为信号而结束，则这个宏值为真 */
    WTERMSIG(status)   /* 取得子进程因信号而中止的信号代码，一般会先用WIFSINGNALED来判断后才使用这个宏 */
    WIFSTOPPED(status)   /* 如果子进程处于暂停执行情况，则这个宏值为真。一般只有使用WUNTRACED时才会有这种情况 */
    WSTOPSIG(status)   /* 取得引发子进程暂停的信号代码，一般会先用WIFSTOPPED来判断后才使用这个宏 */
    WIFCONTINUED(status)   /* 如果状态是表示子进程继续执行则返回非0 */
    WCOREDUMP(status)   /* 如果已经生成了一个核心(core)转储文件，则返回真  */
