# Nmap Switches

### What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?

it's better to read at least ones the help docs. Using command line 
``` 
nmap -h
```
we are looking for the scan techniques and inside for Syn Scan
```
Nmap 7.95 ( https://nmap.org )
Usage: nmap [Scan Type(s)] [Options] {target specification}
TARGET SPECIFICATION:
 ...
 ...
 ...
SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU: UDP Scan
  -sN/sF/sX: TCP Null, FIN, and Xmas scans
  --scanflags <flags>: Customize TCP scan flags
  -sI <zombie host[:probeport]>: Idle scan
  -sY/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO: IP protocol scan
  -b <FTP relay host>: FTP bounce scan
 ...
 ...
EXAMPLES:
  nmap -v -A scanme.nmap.org
  nmap -v -sn 192.168.0.0/16 10.0.0.0/8
  nmap -v -iR 10000 -Pn -p 80
SEE THE MAN PAGE (https://nmap.org/book/man.html) FOR MORE OPTIONS AND EXAMPLES

```

<pre> SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans</pre> 

#### Answer: -sS


### Which switch would you use for a "UDP scan"?
using `nmap -h` and grep (filtering output by lines that contains the input) `UDP` we can find the answer

```
└─$ nmap -h | grep UDP
  -PS/PA/PU/PY[portlist]: TCP SYN, TCP ACK, UDP or SCTP discovery to given ports
  -sU: UDP Scan
  --badsum: Send packets with a bogus TCP/UDP/SCTP checksum

```
#### Answer: -sU

### If you wanted to detect which operating system the target is running on, which switch would you use?

usually people are lazy and most of the docs till now were written by humans. So "Operating System" in most cases will be "OS"

``` 
└─$ nmap -h | grep OS 
HOST DISCOVERY:
  --system-dns: Use OS's DNS resolver
OS DETECTION:
  -O: Enable OS detection
  --osscan-limit: Limit OS detection to promising targets
  --osscan-guess: Guess OS more aggressively
  -A: Enable OS detection, version detection, script scanning, and traceroute
  ```
#### Answer: -O

  ### Nmap provides a switch to detect the version of the services running on the target. What is this switch?


  ```
  └─$ nmap -h | grep version
  -sV: Probe open ports to determine service/version info
  --version-intensity <level>: Set from 0 (light) to 9 (try all probes)
  --version-light: Limit to most likely probes (intensity 2)
  --version-all: Try every single probe (intensity 9)
  --version-trace: Show detailed version scan activity (for debugging)
  -A: Enable OS detection, version detection, script scanning, and traceroute
  -V: Print version number

  ```

#### Answer: -sV

  ### The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?

Usually it's -v or --verbose 
  ```
  └─$ nmap -h | grep verbos   
  -v: Increase verbosity level (use -vv or more for greater effect)

  ```

#### Answer: -v

### Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two? (Note: it's highly advisable to always use at least this option)

Previos response has "use -vv or more for greater effect"

#### Answer: -vv

### What switch would you use to save the nmap results in three major formats?

```
└─$ nmap -h | grep format
     and Grepable format, respectively, to the given filename.
  -oA <basename>: Output in the three major formats at once

```
#### Answer: -oA 
### What switch would you use to save the nmap results in a "normal" format?

```
└─$ nmap -h | grep normal
  -oN/-oX/-oS/-oG <file>: Output scan in normal, XML, s|<rIpt kIddi3,

```
#### Answer: -oN
### A very useful output format: how would you save results in a "grepable" format?

```
OUTPUT:
  -oN/-oX/-oS/-oG <file>: Output scan in normal, XML, s|<rIpt kIddi3,
     and Grepable format, respectively, to the given filename.
  -oA <basename>: Output in the three major formats at once

```
#### Answer: -oG

### How would you activate this setting?

```
MISC:
  -6: Enable IPv6 scanning
  -A: Enable OS detection, version detection, script scanning, and traceroute
  --datadir <dirname>: Specify custom Nmap data file location

```
#### Answer: -A


### How would you set the timing template to level 5?

```
└─$ nmap -h | grep timing    
  -T<0-5>: Set timing template (higher is faster)

```
#### Answer: -T5


### How would you tell nmap to only scan port 80?

```
└─$ nmap -h | grep port | grep scan
  -sn: Ping Scan - disable port scan
  -sI <zombie host[:probeport]>: Idle scan
  -p <port ranges>: Only scan specified ports
  --exclude-ports <port ranges>: Exclude the specified ports from scanning
  -F: Fast mode - Scan fewer ports than the default scan
  --max-retries <tries>: Caps number of port scan probe retransmissions.

```
#### Answer: -p 80

### How would you tell nmap to scan ports 1000-1500?


```
-p <port ranges>: Only scan specified ports
```
#### Answer: -p 1000-1500


### How would you tell nmap to scan all ports?
nothing in help, so let's use `man nmap` and search for PORT SPECIFICATION AND SCAN ORDER
```
PORT SPECIFICATION AND SCAN ORDER
       In addition to all of the scan methods discussed previously, Nmap
       offers options for specifying which ports are scanned and whether the
       scan order is randomized or sequential. By default, Nmap scans the
       most common 1,000 ports for each protocol.

       -p port ranges (Only scan specified ports)
           This option specifies which ports you want to scan and overrides
           the default. Individual port numbers are OK, as are ranges
           separated by a hyphen (e.g.  1-1023). The beginning and/or end
           values of a range may be omitted, causing Nmap to use 1 and
           65535, respectively. So you can specify -p- to scan ports from 1
           through 65535. Scanning port zero is allowed if you specify it
           explicitly. For IP protocol scanning (-sO), this option specifies
           the protocol numbers you wish to scan for (0–255).

           When scanning a combination of protocols (e.g. TCP and UDP), you
           can specify a particular protocol by preceding the port numbers
           by T: for TCP, U: for UDP, S: for SCTP, or P: for IP Protocol.
           The qualifier lasts until you specify another qualifier. For
           example, the argument -p U:53,111,137,T:21-25,80,139,8080 would
           scan UDP ports 53, 111,and 137, as well as the listed TCP ports.
           Note that to scan both UDP and TCP, you have to specify -sU and
           at least one TCP scan type (such as -sS, -sF, or -sT). If no
           protocol qualifier is given, the port numbers are added to all
           protocol lists.  Ports can also be specified by name according to
           what the port is referred to in the nmap-services. You can even
           use the wildcards * and ?  with the names. For example, to scan
           FTP and all ports whose names begin with “http”, use -p
           ftp,http*. Be careful about shell expansions and quote the
           argument to -p if unsure.

           Ranges of ports can be surrounded by square brackets to indicate
           ports inside that range that appear in nmap-services. For
           example, the following will scan all ports in nmap-services equal
           to or below 1024: -p [-1024]. Be careful with shell expansions
           and quote the argument to -p if unsure.


```
At the end we can see `So you can specify -p- to scan ports from 1
           through 65535`
#### Answer: -p-


### How would you activate a script from the nmap scripting library (lots more on this later!)?


```
└─$ nmap -h | grep script   
  -sC: equivalent to --script=default
  --script=<Lua scripts>: <Lua scripts> is a comma separated list of
           directories, script-files or script-categories
  --script-args=<n1=v1,[n2=v2,...]>: provide arguments to scripts
  --script-args-file=filename: provide NSE script args in a file
  --script-trace: Show all data sent and received
  --script-updatedb: Update the script database.
  --script-help=<Lua scripts>: Show help about scripts.
           <Lua scripts> is a comma-separated list of script-files or
           script-categories.
  -A: Enable OS detection, version detection, script scanning, and traceroute
                                                                                      
```
#### Answer: --script


### How would you activate all of the scripts in the "vuln" category?


```
--script=<Lua scripts>: <Lua scripts> is a comma separated list of
           directories, script-files or script-categories
```
#### Answer: --script=vuln
