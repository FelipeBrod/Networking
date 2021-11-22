# Phase 1:

  ## 1. Converted the xlxs to csv

  ## 2. Created a script to read all ips and fping every ip

  ```Bash
  #!/bin/bash
  date
  csvFile="Rockstarserverlist.csv" 
  awk -F ',' '{print $1}' $csvFile | while read ip
  do
  echo "------------$ip--------------"
  fping -g -s $ip | grep -v unreachable >> results.txt
  done

  ```

  **Network layer 3** for deteciton whether the host is up

  ## 3.  
  > ``$: ./pinging.sh > results.txt``
  
  > ``$: cat results``
 
       12.205.151.1 is alive
       167.172.144.11 is alive
         Thu Nov 18 18:49:46 EST 202167.207.67.2
       ------------12.205.151.91/24--------------
       254 targets
       1 alive
       253 unreachable
       0 unknown addresses
       253 timeouts (waiting for response)
       continues...

# Phase 2:

 ## 1. Created a script to read all ips and nmap every port

  ```Bash
  #!/bin/bash
  date
  csvFile="Rockstarserverlist.csv" 
  awk -F ',' '{print $1}' $csvFile | while read ip
  do

  echo "------------$ip--------------"
  nmap -sS $ip >> nmapResults.txt
  done
  ```

  **Network layer 3** for deteciton whether the host is up

  **Transport layer 4** to detect which ports are open.

  **Application layer 5** for SSL/TLS: HHTP, FTP, SSH, RDP and SMB

 ## 2. ``$: cat nmapResults.txt``
 
    Starting Nmap 7.60 ( https://nmap.org ) at 2021-11-18 19:28 EST
    Nmap scan report for 12-205-151-0.static.cpe.att.net (12.   205.151.0)
    Host is up (0.0013s latency).
    All 1000 scanned ports on 12-205-151-0.static.cpe.att.net   (12.205.151.0) are filtered

    Nmap scan report for 12-205-151-1.static.cpe.att.net (12.   205.151.1)
    Host is up (0.11s latency).
    All 1000 scanned ports on 12-205-151-1.static.cpe.att.net   (12.205.151.1) are filtered

     Nmap scan report for 12-205-151-2.static.cpe.att.net (12.   205.151.2)
     Host is up (0.0013s latency).
     Not shown: 999 filtered ports
     PORT     STATE SERVICE
     5357/tcp open  wsdapi

     continues...


## Phase 3:

 ## 1. ``$: sudo nmap -sS 167.172.144.11``

     Starting Nmap 7.60 ( https://nmap.org ) at 2021-11-18 21:36 
     EST
     Nmap scan report for 167.172.144.11
     Host is up (0.0010s latency).
     Not shown: 999 filtered ports
     PORT   STATE SERVICE
     22/tcp open  ssh
    
  **Network layer 3** for deteciton whether the host is up

  **Transport layer 4** to detect which ports are open.

  **Application layer 5** for SSL/TLS: HHTP, FTP, SSH, RDP and SMB

 ## 2. ``$: ssh jimi@167.172.144.11 -y``
    
 ## 3. ``$: cat /etc/hosts | grep rollingstones.com``
  * The host file was modified
  
         98.137.246.8 rollingstones.com
 ## 4. ``$ nslookup 98.137.246.8``
       
        8.246.137.98.in-addr.arpa	name = unknown.yahoo.com.

        Authoritative answers can be found from:
  

   **Presentation Layer 6**

# Phase 4:

 ## 1. ``cat packetcaptureinfo.txt`` 
        
        https://drive.google.com/file/d/1ic-CFFGrbruloYrWaw3PvT71elTkh3eF/view

 ## 2. Evidence of ARP poisoning - Man in the middle attack.
    
   * 1 - Evidence of gratuitous ARP reply -  packets sent to thbroadcast MAC address with the target IP address set to be the samas the sender's IP address 
   ![screenshot 1 wireshark, image info](.\resources\Screenshot_1.png)
   **Datalink Layer 2 and Newtwork Layer 3**
   * 2        
   ![screenshot 2 wireshark, image info](.\resources\Screenshot_2.png)
   **Datalink Layer 2 and Newtwork Layer 3**
   * 3 - An employee from Rock Star posted in website that they arwilling to provide ssh keys for 1m dollars. 
   ![screenshot 3 wireshark, image info](.\resources\Screenshot_3.png)
   POST resquest **Application Layer 7**

