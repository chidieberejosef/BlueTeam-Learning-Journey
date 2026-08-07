**The Processes I observed**

| Processes | PID |
|---------|-------------|
|  explorer.exe | 8904 |
| lsass.exe | 984 |
| services.exe | 976 |
| svchost.exe | multiple PID's |
|  winlogon.exe | 928 |
| crss.exe | 648 |


The reason why multiple svchost.exe existed is because it is a host service. Windows has hundreds of background services (DHCP client, DNS client, windows update, Event log etc) and instead of giving each one its executable, windows group several service under svchost.exe.  

1. What is the difference between a program and a process? A Process is a running instance of an application while a program is the application itself
2. Why does every process have a PID? To identify the instance. The PID identifies each running process uniquely and this is useful such that if chrome.exe is open in multiple instances, it is the PID that helps taskmanager to identify which to terminate
3. What is a parent process? The parent process is the process that created or launched another process (the child process).
4. Why are process trees important during incident response? It tells the story.
5. Why is WINWORD.EXE launching powershell.exe often considered suspicious? it is unusual enough that it deserves investigation.Unexpected behavior requiring investigation.


__Below is an image of Task manager on windows__
<img width="1041" height="726" alt="processes snip" src="https://github.com/user-attachments/assets/a78d79f4-f4ad-4ec9-9a72-f7003b1b790d" />
