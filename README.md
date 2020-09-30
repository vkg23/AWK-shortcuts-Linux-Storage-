# AWK-shortcuts-Linux-Storage-
Quick AWK Tips for Unix , linux and Storage related data processing

# Table of Contents
* [df output: Find the filesystems whose usage % equal or greater than 60](#df)
* [iostat output: iostat or vmstat with timestamp appended in live stream using iostat TS ](#io1)
* [iostat output: iostat or vmstat with timestamp appended in live stream ](#io1)


### <a name="df"> 1. Find the filesystems whose usage % equal or greater than 60  </a>
>> df -k | awk 'NR == 1 {print;next} ; {if (strtonum($5) >= 60) {print}}'

```
Filesystem            kbytes    used   avail capacity  Mounted on
/dev/dsk/c0t0d0s6    1388419 1050390  282493    79%    /usr
/dev/dsk/c0t0d0s4    1784644 1525360  205745    89%    /export
venus:/usr/dist    20612581 13237316 6963015    66%    /usr/dist
```
### <a name="io1"> 2. iostat or vmstat with timestamp appended in live stream (using its own provied timestamp (-t) across lines </a>
>> iostat -t 1 | awk '/..:..:../ {ts=$0;next} {print ts,$0}'

```
#unlike a while loop in iostat , AWK works in live stream making it faster and smoother
09/30/2020 04:41:50 AM Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
09/30/2020 04:41:50 AM sda               6.00         0.00        28.00          0         28
09/30/2020 04:41:50 AM dm-0              0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM dm-1              0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdb               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdc               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdd               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sde               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdf               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdg               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdh               0.00         0.00         0.00          0          0
09/30/2020 04:41:50 AM sdi               0.00         0.00         0.00          0          0

```
### <a name="io2"> 3. iostat or vmstat with timestamp appended in live stream (TS generated outside ) </a>
>> iostat 1 | awk '/Device: / {"date" | getline ts ; close ("date")} ; {print ts,$0}'

```
# This generates a date command for every iteration of iostat when 'Device' header is located and then appends to every line. 
#unlike a while loop in iostat , AWK works in live stream making it faster and smoother
Wed Sep 30 04:57:35 CEST 2020 Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
Wed Sep 30 04:57:35 CEST 2020 dm-0              1.02        18.76        12.27  164650560  107740579
Wed Sep 30 04:57:35 CEST 2020 dm-1              0.01         0.73         0.00    6375404          0

Wed Sep 30 04:57:37 CEST 2020 Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
Wed Sep 30 04:57:37 CEST 2020 dm-0              0.00         0.00         0.00          0          0
Wed Sep 30 04:57:37 CEST 2020 dm-1              0.00         0.00         0.00          0          0

Wed Sep 30 04:57:39 CEST 2020 Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
Wed Sep 30 04:57:39 CEST 2020 dm-0              0.00         0.00         0.00          0          0
Wed Sep 30 04:57:39 CEST 2020 dm-1              0.00         0.00         0.00          0          0

```

