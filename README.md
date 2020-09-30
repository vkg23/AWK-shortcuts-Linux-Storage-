# AWK-shortcuts-Linux-Storage-
Quick AWK Tips for Unix , linux and Storage related data processing


## Processing DF output , Onliner :
Q. Find the filesystems whose usage % beyond 60
df -k | awk 'NR == 1 {print;next} ; {if (strtonum($5) >= 60) {print}}'

Raw input Sample view 
Filesystem            kbytes    used   avail capacity  Mounted on
/dev/dsk/c0t0d0s0     384120  131596  214112    39%    /
/dev/dsk/c0t0d0s6    1388419 1050390  282493    79%    /usr
/proc                      0       0       0     0%    /proc
mnttab                     0       0       0     0%    /etc/mnttab
fd                         0       0       0     0%    /dev/fd
swap                  467152      40  467112     1%    /var/run
swap                  467160      48  467112     1%    /tmp
/dev/dsk/c0t0d0s4    1784644 1525360  205745    89%    /export
venus:/usr/dist    20612581 13237316 6963015    66%    /usr/dist


