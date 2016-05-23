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
awk
```
echo hello |awk 'BEGIN {print "start"} {print $0}END{print "end"}'
```
awk -v
```
V = 100
echo | awk -v VAR=$V '{print VAR}'
```
alternate:
```
V = 100
echo | awk  '{print VAR}' VAR=$V
```


Examp:
remove js comments: /* */
```
sed 's:/\*.*\*/::g
```
(no escape char)
Remove spaces before or after parentheses:
```
sed 's/ \?\([{}();,:]\) \?/\1/g'
```
paste (multi column)
```
paste file1 file2 -d ","
```






#####cp5
######Downloading from a web page
```
wget http://.. -O filename -o otherlocation
```
test times
```
wget -t 5 url
```
limit-rate
```
wget --limit-rate 20k url
```
--quota, -Q
```
wget -Q 100m url
```
resume a download
```
wget -c url
```
using username and password
```
wget --user username --password pass url
```


######download web page as text
```
lynx -dump url >new.txt
```
######primer on cURL
```
curl url --silent -o new_filename
```
Or use default name
```
curl url -O
```
using referer
```
curl --referer refererurl targeturl
```
with cookie
```
curl url --cookie "user=u;pass=p"
curl url --cookie-jar file
```
with agent
```
curl --user-agent "Mozilla/5.0"
```
with auth
```
curl -u user:pass url
```
dump header
```
curl -I url
```
######Accessing gmail emails
######Parsing data from a website
```
lynx -dump -nolist url | grep -o "Rank-.*" | sed -e 's/ *Rank-\([0-9]*\) *\(.*\)/\1\t\2/' | sort -n -k1 > res.txt
```
######Image crawler and downloader (hard)
use two shifts, read file line by line using while 
```
whild read filename;
do
done < filename
```
######web photo album
imagemagick  
set width 100px
```
convert "$img" -resize "100x" "$img"
```
######Twitter command-line

######creating a define
```
curl --slient http://www.directionaryapi.com/api/v1/references/learners/xml/$1?key=$apikey | grep -o \<dt\>.*\</dt\> | sed 's$</*[a-z]*>$$g'| head -n 2 |nl
```
######finding broken links
```
lynx -traversal $1 > /dev/null
sort -u reject.dat >link.txt

while read link;
do
  output = `curl -I $link -s | grep "HTTP/.*OK";
  if [[ -z $output ]];
  then
    echo $link;
    let count++;
  fi
done < link.txt
```
######Posting to a website
```
curl http:// -d"k1=v1&k2=v2"

wget http:// --post-data "k1=v1&k2=v2"
```
#####cp6 The backup plan
######archiving with tar
list file
```
tar -tf x.tar
```
tar
```
tar -cf out.tar a b c
```
append a file
```
tar -rf original.tar newfile
```
zip a bundle and using ssh to send
```
tar cvf - files/ | ssh user@host "tar xv -C dest/"
```
append tar1, tar2 to tar1
```
tar -Af 1.tar 2.tar
```
exclude file
```
tar cvf a.tar * --exclude "*.txt"
```
using a list file to exclude
```
cat list.txt
```
see
```
filea
fileb
```
then use
```
tar -cf a.tar * -X list.txt
```
printing total
```
tar -cf a.tar * --totals
```



delete a file from tar
```
tar --delete --file a.tar file1 file2
```
######Archiving with cpio
```
touch a b
echo a b | cpio -ov > new.cpio
```
list file
```
cpio -it < new.cpio
```
extract
```
cpio -id <new.cpio
```
######compressing using gzip
```
gzip filename
gunzip filename.gz
```
list properties
```
gzip -l a.gz
```
specify output -c
```
cat file > gzip -c >file.gz
```
using tar to specify gzip format
```
tar -cavvf a.tar.gz file
```
or
```
tar a.tar file
gzip a.tar
#####cp7
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


#####8 put on the monitor's cap
```
du file1 file2
```
check files in a dict
```
du -a dict
```
using -c to get total size of multi files
```
du -c file1 file2
```
only print total
```
du -s dict
```
