# MEMORY.DMP Review

### WinDbg

> Assuming the cause of this error was made by the Trend Micro Eagle Eye driver (tmeevw.sys) it would crash chrome.exe when it attempted to load.

````shell
kd> !analyze -v
PAGE_FAULT_IN_NONPAGED_AREA (50)
Invalid system memory was referenced.  This cannot be protected by try-except.
Typically the address is just plain bad or it is pointing at freed memory.

IMAGE_NAME:  NETIO.SYS

PROCESS_NAME:  chrome.exe

NETIO!ArbitrateAndEnforce+0xc58:
fffff806`815ad1f8 837da000        cmp     dword ptr [rbp-60h],0 ss:0018:ffffaf0c`00000fa2=????????

kd> dps ffffaf0cbd3d8138 ffffaf0cbd3d9a90
ffffaf0c`bd3d82a8  fffff806`79ea4c66Unable to load image \SystemRoot\system32\DRIVERS\tmeevw.sys, Win32 error 0n2
 tmeevw+0x4c66
````
