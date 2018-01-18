### Low disk, replace '/' with the filesystem in question, presents date, fs information + largest 15 folders (assuming usage in Gigabytes) --
``` $ FS='/';resize;clear;date;df -h $FS; echo "Largest Directories:"; du -hcx --max-depth=2 $FS 2>/dev/null | grep [0-9]G | head -15 | sort -rk 1; ```

### Directories with the most files --
``` $ find / -xdev -printf '%h\n' | uniq -c | sort -k 1 -nr | head -n 20 ```


### Low disk, replace '/' with the filesystem in question, presents date, fs information + largest 15 folders (assuming usage in Gigabytes) and largest 30 files --
``` $ FS='/';resize;clear;date;df -h $FS; echo "Largest Directories:"; du -hcx --max-depth=2 $FS 2>/dev/null | grep [0-9]G | head -15 | sort -rk 1; echo "Largest Files:"; find $FS -mount -type f -ls | sort -rnk7 | head -30 | awk '{printf "%d MB\t%s\n",($7/1024)/1024,$NF}' ``` 
