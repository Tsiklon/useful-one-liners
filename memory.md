## Top 20 Memory consuming processes and Processes using memory --
``` TMPFILE=`mktemp` || exit 1;date > $TMPFILE;ps aux >> $TMPFILE;echo -e "\n$(head -n1 $TMPFILE)\n\n~~~~~ Top 20 processes actively consuming Memory ~~~~~\n$(awk '{print $2,$4,$11,$12,$13,$14,$15}' $TMPFILE | grep "MEM") \n$(grep -v '[0-9][0-9]:[0-9][0-9]:[0-9][0-9]' $TMPFILE|awk '$4 != 0.0 {print $2,$4,$11,$12,$13,$14,$15}' | grep -v "PID"|sort --field-separator=" " -nrk2 | head -n 20)\n\n~~~~~ Number of Processes actively consuming Memory - $(awk '$4 != 0.0 {print $2,$4,$11,$12,$13,$14,$15}' $TMPFILE| grep -v "PID" | wc -l) ~~~~~\n~~~~~ Total % of memory used - $( grep -v '[0-9][0-9]:[0-9][0-9]:[0-9][0-9]' $TMPFILE| awk '$4 != 0.0 {sum += $4} END {print sum}')% ~~~~~"; ```

## Memory usage from SAR from the last 2 hours --
``` memtot=`free -m | awk '$1 ~ /Mem/ {print $2}'`; echo -e "\nTime\t\tPercent\n";sar -r -s `date --date "-2 hours" +%T`|tail -n +4 |awk -v memtot="$memtot" '{printf "%s %s %8d % \n",$1,$2,(($4-$6-$7)/1024)*100/memtot}'|grep -v Average ```

## Drop Memory Caches --
``` sync;echo 1 > /proc/sys/vm/drop_caches ```