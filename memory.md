## Top 20 Memory consuming processes and Processes using memory --
``` 
TMPFILE=`mktemp` || exit 1;date > $TMPFILE;ps aux >> $TMPFILE;echo -e "\n$(head -n1 $TMPFILE)\n\n~~~~~ Top 20 processes actively consuming Memory ~~~~~\n$(awk '{print $2,$4,$11,$12,$13,$14,$15}' $TMPFILE | grep "MEM") \n$(grep -v '[0-9][0-9]:[0-9][0-9]:[0-9][0-9]' $TMPFILE|awk '$4 != 0.0 {print $2,$4,$11,$12,$13,$14,$15}' | grep -v "PID"|sort --field-separator=" " -nrk2 | head -n 20)\n\n~~~~~ Number of Processes actively consuming Memory - $(awk '$4 != 0.0 {print $2,$4,$11,$12,$13,$14,$15}' $TMPFILE| grep -v "PID" | wc -l) ~~~~~\n~~~~~ Total % of memory used - $( grep -v '[0-9][0-9]:[0-9][0-9]:[0-9][0-9]' $TMPFILE| awk '$4 != 0.0 {sum += $4} END {print sum}')% ~~~~~"; 
```

## Memory usage from SAR from the last 2 hours --
``` 
memtot=`free -m | awk '$1 ~ /Mem/ {print $2}'`; echo -e "\nTime\t\tPercent\n";sar -r -s `date --date "-2 hours" +%T`|tail -n +4 |awk -v memtot="$memtot" '{printf "%s %s %8d % \n",$1,$2,(($4-$6-$7)/1024)*100/memtot}'|grep -v Average 
```

## Drop Memory Caches --
``` 
sync;echo 1 > /proc/sys/vm/drop_caches 
```

## Memory utilisation - Total, Swap, Usage, Slab caches, recent usage
```
tempfile=$(mktemp) ; coproc sar -B -r -o $tempfile 1 10 >/dev/null; resize; clear; echo "== Server Time: =="; date '+%F %r'; echo -e "\n== Memory Utilization Information: =="; awk '{ if ($1 == "MemTotal:") { TOTAL =$2/1024} if ($1 == "MemFree:") { FREE =$2 } if ($1== "Buffers:") { BUFFERS =$2 } if ($1 == "Cached:" ) { CACHE = $2 } USED = TOTAL-(FREE+BUFFERS+CACHE)/1024 } END {printf "Total Memory\tActive Memory\tPercentage Used\n%dM\t\t%dM\t\t%.2f%%\n",TOTAL,USED,USED/TOTAL * 100; }' /proc/meminfo; echo -e "\n== Current Swap Usage: =="; swapon -s | sed 1d | awk 'BEGIN { print "DEVICE\t\tUSED\t\tTOTAL\t\tPERCENT USED"; } { DEVICE=$1; TOTAL=($3/1024); USED=($4/1024); PERCENT=((USED/TOTAL)*100); printf "%s\t%.2fM\t%.2fM\t%.2f%%\n",DEVICE,USED,TOTAL,PERCENT; }' | column -s$'\t' -t; echo -e "\n== Top 10 Processes by Memory Usage: =="; ps -eo user,pid,%mem,rsz,args --sort=-rsz | head -11 | awk '{print $1,$2,$3,$4,$5}' | column -t; echo -e "\n== Top 10 Processes By Swap Usage: =="; ( printf "%s\t%s\t%s\n" "PID" "PROCESS" "SWAP"; (for i in /proc/[0-9]*; do PID=${i#/proc/}; NAME=$(awk '/Name/ {print $2}' ${i}/status 2>/dev/null); SWAP=$(awk '/Swap/ { sum+=$2 }; END { print sprintf("%.2f", sum/1024) "M" }' /${i}/smaps 2>/dev/null); echo ${PID} ${NAME} ${SWAP}; done | awk '!/0.00M/' |sort -grk3,3 | head -10 )) | column -t; echo -e "\n== Top 10 Kernel Slab Caches: =="; ( echo "SIZE NAME"; slabtop -o -s c | sed 1,7d | head -10 | awk '{ printf "%.2fM\t%s\n",gensub(/K$/,"","g",$(NF-1))/1024,$NF; }' ) | column -t; echo -e "\n== Last 30 Minutes Memory Usage: =="; sar -r -s $(date --date='-50 minutes' +%T) | sed 1,2d; echo -e "\n== Last 30 Minutes Paging/Swap Statistics: =="; sar -B -s $(date --date='-50 minutes' +%T) | sed 1,2d; wait 2>/dev/null; echo -e "\n== Current 1 Second Memory Usage Statistics (10 Count): =="; sar -r -f $tempfile | sed 1,2d; echo -e "\n== Current 1 Second Paging/Swap Statistics (10 Count): =="; sar -B -f $tempfile | sed 1,2d; if [[ -f $tempfile ]]; then rm -f $tempfile; fi 
```