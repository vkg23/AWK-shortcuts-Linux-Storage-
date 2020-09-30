# AWK-shortcuts-Linux-Storage-
Quick AWK Tips for Unix , linux and Storage related data processing


## Processing DF output , Onliner :
> Find the filesystems whose usage % beyond 60 
>> df -k | awk 'NR == 1 {print;next} ; {if (strtonum($5) >= 60) {print}}'



```
Filesystem            kbytes    used   avail capacity  Mounted on
/dev/dsk/c0t0d0s6    1388419 1050390  282493    79%    /usr
/dev/dsk/c0t0d0s4    1784644 1525360  205745    89%    /export
venus:/usr/dist    20612581 13237316 6963015    66%    /usr/dist
```

