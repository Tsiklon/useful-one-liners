## IP Tables
### Show Rules with Line numbers
` # iptables -nL --line-numbers `

### Insert Rule into input chain for all traffic from a specific IP Address at rule number 32
` # iptables -I INPUT 32 -p tcp -s 123.123.123.123 -m comment --comment "allows all traffic from 123.123.123.123" -j ACCEPT `

### Delete rule on the input chain at location 33
` # iptables -D INPUT 33 `
