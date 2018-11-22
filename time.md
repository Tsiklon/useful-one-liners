# time conversions
 ## OS X 
   epoch -> readable
   ``` # date -jr 1468002292 ```
 
 ## Linux 
   epoch -> readable
- ``` # date -d @1468002292 ```
   
   readable -> epoch
- ``` # date +%s -d "Jan 1, 1980 00:00:01" ```
   
   Dmesg to human readable via /proc/uptime 
- ``` # date -d"70-1-1 + $(date +%s) sec - $(cut -d ' ' -f1 < /proc/uptime) sec + [DMESG TIMESTAMP HERE] sec" +"%F %T" ```
