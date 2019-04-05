os - CS 350 OS/161 All-In-One CLI
===============

This project abstracts and simplifies the entire process of configuring, building, and running OS/161 kernels.

1. [Features/Commands](#featurescommands)
1. [Usage](#usage)

# Features/Commands
* `verbose_level` toggle to silence stdout messages (will not silence stderr) that occur when configuring and building the OS/161 kernel. Additionally, if `os run [...] <command>` is called and `verbose_level=0`, all start-up and shutdown output from OS/161 is silenced real-time as well, which makes running tests less messy.
Eg. `verbose_level=1`:
```
UWaterloo:~ george$ os run "p testbin/forktest"
[ -d /u0/l69ol/cs350-os161/root ] || mkdir /u0/l69ol/cs350-os161/root
cp kernel /u0/l69ol/cs350-os161/root/kernel-ASST3
rm -f /u0/l69ol/cs350-os161/root/kernel
ln -s kernel-ASST3 /u0/l69ol/cs350-os161/root/kernel
sys161: System/161 release 1.99.06, compiled Aug 23 2013 10:23:34

OS/161 base system version 1.99.05
Copyright (c) 2000, 2001, 2002, 2003, 2004, 2005, 2008, 2009
   President and Fellows of Harvard College.  All rights reserved.

George Lim's system version 0 (ASST3 #0)

3884k physical memory available
Device probe...
lamebus0 (system main bus)
emu0 at lamebus0
ltrace0 at lamebus0
ltimer0 at lamebus0
beep0 at ltimer0
rtclock0 at ltimer0
lrandom0 at lamebus0
random0 at lrandom0
lhd0 at lamebus0
lhd1 at lamebus0
lser0 at lamebus0
con0 at lser0

cpu0: MIPS r3000
OS/161 kernel: p testbin/forktest
testbin/forktest: Starting.
001111222222223333333333333333
testbin/forktest: Complete.
Operation took 1.301021497 seconds
OS/161 kernel: q
Shutting down.
The system is halted.
sys161: 37054891 cycles (35551880 run, 1503011 global-idle)
sys161:   cpu0: 35115213 kern, 436667 user, 0 idle)
sys161: 1568 irqs 24450 exns 0r/0w disk 0r/714w console 9r/0w/3m emufs 0r/0w net
sys161: Elapsed real time: 1.481095 seconds (25.0186 mhz)
sys161: Elapsed virtual time: 1.482195657 seconds (25 mhz)
asst=3  build=0 ramsize=4194304 cpus=1
UWaterloo:~ george$ 
```
Eg. `verbose_level=0`:
```
UWaterloo:~ george$ os run "p testbin/forktest"
testbin/forktest: Starting.
001111222222223333333333333333
testbin/forktest: Complete.
Operation took 1.299112497 seconds
asst=3  build=0 ramsize=4194304 cpus=1
UWaterloo:~ george$ 
```
* Command `os config <ASST #>` automatically configures OS/161 for an assignment. **NOTE: If an assignment has 2 parts like 2a/2b, use `os config 2`.** `config` will also clean old kernel compile files when switching assignments, and build the new assignment's dependencies. `config` is only meant to be called once when switching to a new assignment.
* Command `os current` prints the current assignment #, as well as current kernel build, ram (in bytes), and core count. `current` is called at the end of every `os run` call.
* Command `os build [-u] [-v <version #>]` builds the OS/161 kernel. Optional flags `-u` builds all user programs and `-v <version #>` sets the kernel build number for the current assignment.
* Command `os run [-c <core #>] [-r <ram #>] [<command>]` first builds the kernel, then calls `sys161 kernel` if the build succeeded. Optional flags `-c <core #>` sets the `sys161.conf` core count and `-r <ram #>` sets the amount of ram in **megabytes**. Optional parameter `[<command>]` allows OS/161 commands to be automatically executed after OS start-up. The OS/161 command `q` is automatically appended when this optional parameter is used.
* Command `os submit <ASST #>` submits the current kernel under the specified assignment number, and deletes the `os161kern.tgz` file afterwards. **NOTE: If an assignment has 2 parts like 2a/2b, use the full assignment name (eg. `os submit 2b`).**

# Usage
Firstly, `chmod 755 os` to give `os` executable permissions. If you want to call `os` from any directory, add `alias 'os'='<os_path>'` to your `~/.bash_profile`.
