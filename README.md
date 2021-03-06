# kill-adobe

The background processes spawned by Adobe CC were eating up a lot of my disk cycles and spawning random update windows. I disabled them starting up on login, but they started anyway (at the latest when I opened something by Adobe and they lingered after it was closed) so I wrote this small utility to kill them and keep them closed.

## Usage

This program might not necessarily need administrator privileges, but I have confirmed that it works differently depending on whether they are present. If it does not work in restricted mode, try running with higher permissions.

It will also accept the names of other processes to kill as command line arguments, e.g. `kill-adobe.exe foo.exe`.

The program starts by checking for the processes every ten seconds, but adjusts this time depending on whether or not the processes were found to have respawned. The maximum time it will wait is two minutes, so they should never run for more than two minutes in the worst case. If it ran every second it would be no better than the processes it is closing.

## Default Processes

By default, it will look for the following processes:

```
AdobeUpdateService.exe
AGSService.exe
armsvc.exe
CoreSync.exe
Adobe Desktop Process.exe
Adobe Installer.exe
AdobeIPCBroker.exe
CCXProcess.exe
```

The run time of each iteration is linear to the number of processes being looked for, but also to the total number of processes running on the system.

## Compilation

If compiled in a debug configuration, it will keep a terminal window open and log its activities. Else it will disappear into the background and work silently.

It does not currently run properly when compiled as x64, though an x64 configuration is present in the VS project. I plan on fixing this but it is not a high priority since it won't make much of a difference here if at all.

## License

Do what you want; I just made this because it was useful to me.

