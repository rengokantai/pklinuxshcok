#### pklinuxshcok
- cp4
print columns other than 3
```
cut -f 3 --complement x.txt
```
cut multiple fields,with delimiter
```
cut file.txt -c1-3,4-7 --output-delimiter ","
```
using sed to replace old text
```
sed -i 's/old/new/' file
```
Not replace old text,but save a new file.bak file
```
sed -i .bak 's/old/new/' file
```
reaplace nth occurance onwards
```
sed -i 's/old/new/4g' file
```
sed with double quote
```
text=hello
echo hello world | sed "s/$text/HELLO/"   #HELLO world
```
sed match all
```
echo hello world | sed's/\w\+/[&]/g' #[hello] [world]
```
sed match notation
```
echo love 100 | sed 's/\w\+ \([0-9]\+\)/\1/'  # 100
```
Some equiva:
```
echo abc |sed 's/a/A' | sed 's/c/C'
echo abc |sed 's/a/A/;s/c/C/'
echo abc |sed -e 's/a/A/' -e 's/c/C/'
```



- cp5

download web page as text
```
lynx -dump url >new.txt
```




- cp7
change MAC
```
ifconfig eth0 hw ether 00:00:00:00:00:00
```
(only lasts until a machine restarts)
```
echo nameserver 111.1.11.1 >>/etc/resolv.conf
```
```
route add default gw IP_ADDRESS(192.168.1.1) INTERFACE_NAME(wlan0)
```

mtr and traceroute
```
traceroute google.com
```

fping
```
fping -a 192.168.1/24 -g 2>/dev/null
fping -a 192.168.0.1 192.168.0.255
```
-a   #all live ips
-u   #all unreachable ips
-g   #groupby

```
#!/bin/bash
for ip in 192.168.0.{1..255};
do
ping $ip -c 2 &>/dev/null;
if [$? -eq 0];
then
echo $ip
fi
done
```
parallel pings:
```
#!/bin/bash
for ip in 192.168.0.{1..255};
do
(ping $ip -c 2 &>/dev/null;
if [$? -eq 0];
then
echo $ip
fi) &
done
```
sftp
```
sftp -oPort=33 user@host
```
scp
```
scp filename user@host:/home/path
```

iwlist
```
iwlist scan
```

redirect local 8000 to remote 80
```
ssh -L 8000:domain:80 user@localhost/remotehost
```
