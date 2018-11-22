## Useful AWK stuff

### Using AWK to search output ala grep;
(These also work when stdin is piped to awk)

### Searching for a single string 
``` # awk '/string to match/' /path/to/file ```

### Searching for more than one string 
``` # awk '/string 1|string 2/' /path/to/file ```     

### Excluding a single string
``` # awk '!/string to exclude/' /path/to/file ```
### Excluding more than one string
``` # awk '!/string 1|string 2/' /path/to/file ```

### Searching for a single string and outputing only the desired column 
``` # awk '/string to match/{print $1}' /path/to/file ```    - match all lines matching the string and output field 1 

### Printing a section of several matches in sequence (useful for parsing XML or JSON) - In this case Section 2 separated by delimiter ':'
``` # awk -F ':' '/String1/{ STRING1=$2; next } /String2/{ STRING2=$2; next } /String3/{print STRING1 STRING2 $2}' path/to/file ```

 - (default field separator is ' ' (a single space))

### Match all lines matching the string and output field 3, with field separator '-'
``` # awk -F '-' '/string to match/{print $3}' /path/to/file ```  

