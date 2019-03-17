# TP6_Reseau


# Lab 2 : Un peu de complexité (et d'utilité ?...)

## 1) Mise en place du Lab


## I. Ping

* Ping du `client1` sur le `server1`

```bash
[remi@client1 etc]$ ping -c 4 server1
PING server1 (10.6.202.10) 56(84) bytes of data.
64 bytes from server1 (10.6.202.10): icmp_seq=1 ttl=60 time=703 ms
64 bytes from server1 (10.6.202.10): icmp_seq=2 ttl=60 time=179 ms
64 bytes from server1 (10.6.202.10): icmp_seq=3 ttl=60 time=53.1 ms
64 bytes from server1 (10.6.202.10): icmp_seq=4 ttl=60 time=58.8 ms

--- server1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3006ms
rtt min/avg/max/mdev = 53.157/248.786/703.914/267.545 ms
```

* Ping du `client2` sur le `server1`
```bash
[remi@client2 ~]$ ping -c 4 server1
PING server1 (10.6.202.10) 56(84) bytes of data.
64 bytes from server1 (10.6.202.10): icmp_seq=1 ttl=60 time=58.2 ms
64 bytes from server1 (10.6.202.10): icmp_seq=2 ttl=60 time=46.3 ms
64 bytes from server1 (10.6.202.10): icmp_seq=3 ttl=60 time=47.2 ms
64 bytes from server1 (10.6.202.10): icmp_seq=4 ttl=60 time=57.0 ms

--- server1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3010ms
rtt min/avg/max/mdev = 46.341/52.224/58.291/5.483 ms
```

* Ping du `server1` sur le `client1`

```bash
[remi@server1 ~]$ ping -c 4 client1
PING client1 (10.6.201.10) 56(84) bytes of data.
64 bytes from client1 (10.6.201.10): icmp_seq=1 ttl=60 time=55.8 ms
64 bytes from client1 (10.6.201.10): icmp_seq=2 ttl=60 time=73.3 ms
64 bytes from client1 (10.6.201.10): icmp_seq=3 ttl=60 time=75.2 ms
64 bytes from client1 (10.6.201.10): icmp_seq=4 ttl=60 time=56.7 ms

--- client1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3019ms
rtt min/avg/max/mdev = 55.830/65.309/75.256/9.047 ms
```

* Ping du `server1` sur le `client2`

```bash
[remi@server1 ~]$ ping -c 4 client2
PING client2 (10.6.201.11) 56(84) bytes of data.
64 bytes from client2 (10.6.201.11): icmp_seq=1 ttl=60 time=58.7 ms
64 bytes from client2 (10.6.201.11): icmp_seq=2 ttl=60 time=83.2 ms
64 bytes from client2 (10.6.201.11): icmp_seq=3 ttl=60 time=46.0 ms
64 bytes from client2 (10.6.201.11): icmp_seq=4 ttl=60 time=51.8 ms

--- client2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 46.040/59.984/83.285/14.189 ms
```

## II. Traceroute

* Ping du `client1` sur le `server1`
```bash
[remi@client1 etc]$ traceroute server1
traceroute to server1 (10.6.202.10), 30 hops max, 60 byte packets
 1  gateway (10.6.201.254)  45.735 ms  46.464 ms  46.309 ms
 2  10.6.101.1 (10.6.101.1)  65.008 ms  65.458 ms  65.342 ms
 3  10.6.100.13 (10.6.100.13)  109.538 ms  119.740 ms  119.665 ms
 4  10.6.100.5 (10.6.100.5)  194.623 ms  194.551 ms  194.450 ms
 5  server1 (10.6.202.10)  229.091 ms !X  228.984 ms !X  228.882 ms !X
```

* Ping du `client2` sur le `server1`
```bash
[remi@client2 ~]$ traceroute server1
traceroute to server1 (10.6.202.10), 30 hops max, 60 byte packets
 1  gateway (10.6.201.254)  8.341 ms  8.317 ms  8.362 ms
 2  10.6.101.1 (10.6.101.1)  18.978 ms  18.971 ms  18.780 ms
 3  10.6.100.13 (10.6.100.13)  42.195 ms  42.132 ms  42.367 ms
 4  10.6.100.5 (10.6.100.5)  52.396 ms  52.332 ms  52.952 ms
 5  server1 (10.6.202.10)  84.372 ms !X  84.293 ms !X  84.388 ms !X
```

* Ping du `server1` sur le `client1`
```bash
[remi@server1 ~]$ traceroute client1
traceroute to client1 (10.6.201.10), 30 hops max, 60 byte packets
 1  gateway (10.6.202.254)  9.244 ms  9.407 ms  9.244 ms
 2  10.6.100.6 (10.6.100.6)  33.976 ms  45.227 ms  45.143 ms
 3  10.6.100.14 (10.6.100.14)  45.641 ms  50.191 ms  50.099 ms
 4  10.6.101.2 (10.6.101.2)  80.628 ms  80.560 ms  80.383 ms
 5  client1 (10.6.201.10)  90.511 ms !X  90.419 ms !X  90.284 ms !X
```

* Ping du `server1` sur le `client2`
```bash
[remi@server1 ~]$ traceroute client2
traceroute to client2 (10.6.201.11), 30 hops max, 60 byte packets
 1  gateway (10.6.202.254)  11.515 ms  11.315 ms  11.174 ms
 2  10.6.100.6 (10.6.100.6)  26.137 ms  27.339 ms  27.373 ms
 3  10.6.100.14 (10.6.100.14)  37.696 ms  37.631 ms  37.538 ms
 4  10.6.101.2 (10.6.101.2)  48.288 ms  48.392 ms  48.304 ms
 5  client2 (10.6.201.11)  61.262 ms !X  61.219 ms !X  61.102 ms !X
```

# Lab 3 : Let's end this properly

## I. NAT : accès internet

* Récupération html de `google.com` sur le `router4` :

```bash
r4.tp6.b1#telnet trip-hop.net 80
Trying trip-hop.net (213.186.33.4, 80)... Open
/HTTP/1.0 400 Bad request
Cache-Control: no-cache
Connection: close
Content-Type: text/html

<html><body><h1>400 Bad request</h1>
                                    Your browser sent an invalid request.
                                                                         </body></html>

[Connection to trip-hop.net closed by foreign host]
```

* Ping de `google.com` avec `router2`

```bash
r2.tp6.b1#ping 8.8.8.8

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 8.8.8.8, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 40/67/144 ms
```

* Ping de `google.com`avec `server1`
```bash
[remi@server1 etc]$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=130 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=913 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=44.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=47.4 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3013ms
rtt min/avg/max/mdev = 44.288/284.020/913.862/365.277 ms
```

## II. Une service d'infra

* `curl localhost` avec le server1 :
```bash
[remi@server1 ~]$ curl localhost
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
    <head>
        <title>Test Page for the Nginx HTTP Server on Fedora</title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <style type="text/css">
            /*<![CDATA[*/
            body {
                background-color: #fff;
                color: #000;
                font-size: 0.9em;
                font-family: sans-serif,helvetica;
                margin: 0;
                padding: 0;
            }
            :link {
                color: #c00;
            }
            :visited {
                color: #c00;
            }
            a:hover {
                color: #f50;
            }
            h1 {
                text-align: center;
                margin: 0;
                padding: 0.6em 2em 0.4em;
                background-color: #294172;
                color: #fff;
                font-weight: normal;
                font-size: 1.75em;
                border-bottom: 2px solid #000;
            }
            h1 strong {
                font-weight: bold;
                font-size: 1.5em;
            }
            h2 {
                text-align: center;
                background-color: #3C6EB4;
                font-size: 1.1em;
                font-weight: bold;
                color: #fff;
                margin: 0;
                padding: 0.5em;
                border-bottom: 2px solid #294172;
            }
            hr {
                display: none;
            }
            .content {
                padding: 1em 5em;
            }
            .alert {
                border: 2px solid #000;
            }

            img {
                border: 2px solid #fff;
                padding: 2px;
                margin: 2px;
            }
            a:hover img {
                border: 2px solid #294172;
            }
            .logos {
                margin: 1em;
                text-align: center;
            }
            /*]]>*/
        </style>
    </head>

    <body>
        <h1>Welcome to <strong>nginx</strong> on Fedora!</h1>

        <div class="content">
            <p>This page is used to test the proper operation of the
            <strong>nginx</strong> HTTP server after it has been
            installed. If you can read this page, it means that the
            web server installed at this site is working
            properly.</p>

            <div class="alert">
                <h2>Website Administrator</h2>
                <div class="content">
                    <p>This is the default <tt>index.html</tt> page that
                    is distributed with <strong>nginx</strong> on
                    Fedora.  It is located in
                    <tt>/usr/share/nginx/html</tt>.</p>

                    <p>You should now put your content in a location of
                    your choice and edit the <tt>root</tt> configuration
                    directive in the <strong>nginx</strong>
                    configuration file
                    <tt>/etc/nginx/nginx.conf</tt>.</p>

                </div>
            </div>

            <div class="logos">
                <a href="http://nginx.net/"><img
                    src="nginx-logo.png"
                    alt="[ Powered by nginx ]"
                    width="121" height="32" /></a>

                <a href="http://fedoraproject.org/"><img
                    src="poweredby.png"
                    alt="[ Powered by Fedora ]"
                    width="88" height="31" /></a>
            </div>
        </div>
    </body>
</html>
```

* `curl server1.tp6.b1` avec le `client1`
```bash
[remi@client1 ~]$ curl server1.tp6.b1
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
    <head>
        <title>Test Page for the Nginx HTTP Server on Fedora</title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <style type="text/css">
            /*<![CDATA[*/
            body {
                background-color: #fff;
                color: #000;
                font-size: 0.9em;
                font-family: sans-serif,helvetica;
                margin: 0;
                padding: 0;
            }
            :link {
                color: #c00;
            }
            :visited {
                color: #c00;
            }
            a:hover {
                color: #f50;
            }
            h1 {
                text-align: center;
                margin: 0;
                padding: 0.6em 2em 0.4em;
                background-color: #294172;
                color: #fff;
                font-weight: normal;
                font-size: 1.75em;
                border-bottom: 2px solid #000;
            }
            h1 strong {
                font-weight: bold;
                font-size: 1.5em;
            }
            h2 {
                text-align: center;
                background-color: #3C6EB4;
                font-size: 1.1em;
                font-weight: bold;
                color: #fff;
                margin: 0;
                padding: 0.5em;
                border-bottom: 2px solid #294172;
            }
            hr {
                display: none;
            }
            .content {
                padding: 1em 5em;
            }
            .alert {
                border: 2px solid #000;
            }

            img {
                border: 2px solid #fff;
                padding: 2px;
                margin: 2px;
            }
            a:hover img {
                border: 2px solid #294172;
            }
            .logos {
                margin: 1em;
                text-align: center;
            }
            /*]]>*/
        </style>
    </head>

    <body>
        <h1>Welcome to <strong>nginx</strong> on Fedora!</h1>

        <div class="content">
            <p>This page is used to test the proper operation of the
            <strong>nginx</strong> HTTP server after it has been
            installed. If you can read this page, it means that the
            web server installed at this site is working
            properly.</p>

            <div class="alert">
                <h2>Website Administrator</h2>
                <div class="content">
                    <p>This is the default <tt>index.html</tt> page that
                    is distributed with <strong>nginx</strong> on
                    Fedora.  It is located in
                    <tt>/usr/share/nginx/html</tt>.</p>

                    <p>You should now put your content in a location of
                    your choice and edit the <tt>root</tt> configuration
                    directive in the <strong>nginx</strong>
                    configuration file
                    <tt>/etc/nginx/nginx.conf</tt>.</p>

                </div>
            </div>

            <div class="logos">
                <a href="http://nginx.net/"><img
                    src="nginx-logo.png"
                    alt="[ Powered by nginx ]"
                    width="121" height="32" /></a>

                <a href="http://fedoraproject.org/"><img
                    src="poweredby.png"
                    alt="[ Powered by Fedora ]"
                    width="88" height="31" /></a>
            </div>
        </div>
    </body>
</html>
```
---
## III. Serveur DHCP

* Sur le `dhcp.tp6.b1`
```bash
[root@dhcp dhcp]# ss -alunp
State      Recv-Q Send-Q Local Address:Port               Peer Address:Port     
UNCONN     0      0            *:67                       *:*                   users:(("dhcpd",pid=3514,fd=7))
UNCONN     0      0            *:68                       *:*                   users:(("dhclient",pid=2919,fd=6))
```
* Sur le `client1`
```bash
[remi@client1 ~]$ sudo dhclient -v enp0s3
Internet Systems Consortium DHCP Client 4.2.5
Copyright 2004-2013 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/enp0s3/08:00:27:69:75:ef
Sending on   LPF/enp0s3/08:00:27:69:75:ef
Sending on   Socket/fallback
DHCPDISCOVER on enp0s3 to 255.255.255.255 port 67 interval 5 (xid=0x533006f8)
DHCPREQUEST on enp0s3 to 255.255.255.255 port 67 (xid=0x533006f8)
DHCPOFFER from 10.6.201.11
DHCPACK from 10.6.201.11 (xid=0x533006f8)
bound to 10.6.201.50 -- renewal in 291 seconds.
```
---
## IV. Serveur DNS

* Dig `server1.tp6.b1`
```bash
[root@server1 etc]# dig server1.tp6.b1

; <<>> DiG 9.9.4-RedHat-9.9.4-73.el7_6 <<>> server1.tp6.b1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48297
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;server1.tp6.b1.                        IN      A

;; ANSWER SECTION:
server1.tp6.b1.         604800  IN      A       10.6.202.10

;; AUTHORITY SECTION:
tp6.b1.                 604800  IN      NS      server1.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.202.10#53(10.6.202.10)
;; WHEN: Tue Mar 12 17:50:48 CET 2019
;; MSG SIZE  rcvd: 73
```

* Dig de `client2.tp6.b1`
```bash
[root@server1 etc]# dig client2.tp6.b1

; <<>> DiG 9.9.4-RedHat-9.9.4-73.el7_6 <<>> client2.tp6.b1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51406
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;client2.tp6.b1.                        IN      A

;; ANSWER SECTION:
client2.tp6.b1.         604800  IN      A       10.6.201.10

;; AUTHORITY SECTION:
tp6.b1.                 604800  IN      NS      server1.tp6.b1.

;; ADDITIONAL SECTION:
server1.tp6.b1.         604800  IN      A       10.6.202.10

;; Query time: 0 msec
;; SERVER: 10.6.202.10#53(10.6.202.10)
;; WHEN: Tue Mar 12 17:53:06 CET 2019
;; MSG SIZE  rcvd: 97
```
* Dig de `10.6.201.10`
```bash
[root@server1 etc]# dig -x 10.6.201.10

; <<>> DiG 9.9.4-RedHat-9.9.4-73.el7_6 <<>> -x 10.6.201.10
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48187
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;10.201.6.10.in-addr.arpa.      IN      PTR

;; ANSWER SECTION:
10.201.6.10.in-addr.arpa. 86400 IN      PTR     client1.tp6.b1.

;; AUTHORITY SECTION:
6.10.in-addr.arpa.      86400   IN      NS      server1.tp6.b1.

;; ADDITIONAL SECTION:
server1.tp6.b1.         604800  IN      A       10.6.202.10

;; Query time: 0 msec
;; SERVER: 10.6.202.10#53(10.6.202.10)
;; WHEN: Tue Mar 12 17:53:50 CET 2019
;; MSG SIZE  rcvd: 119
```
---
## V. Serveur NTP

* Vérifications état de la synchronisation NTP sur le `server1`

```bash
[remi@server1 etc]$ chronyc sources
210 Number of sources = 3
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? 195.154.41.195                2   6     1     3  -2658ms[-2658ms] +/-   55ms
^? 51.15.182.163                 2   6     1     4  -2662ms[-2662ms] +/-   68ms
^? cluster010.linocomm.net       2   6     1     5  -2657ms[-2657ms] +/-   38ms
[remi@server1 etc]$ chronyc tracking
Reference ID    : 7F7F0101 ()
Stratum         : 10
Ref time (UTC)  : Fri Mar 15 10:58:14 2019
System time     : 0.000000000 seconds fast of NTP time
Last offset     : +0.000000000 seconds
RMS offset      : 0.000000000 seconds
Frequency       : 0.000 ppm slow
Residual freq   : +0.000 ppm
Skew            : 0.000 ppm
Root delay      : 0.000000000 seconds
Root dispersion : 0.000000000 seconds
Update interval : 0.0 seconds
Leap status     : Normal
```
* Vérification état de la synchronisation NTP sur le `client1`

```bash
[remi@client1 ~]$ chronyc sources
210 Number of sources = 1
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^* server1                       3   7   377    94    -13ms[  -12ms] +/-   65ms
[remi@client1 ~]$ chronyc tracking
Reference ID    : 0A06CA0A (server1)
Stratum         : 4
Ref time (UTC)  : Sun Mar 17 19:38:03 2019
System time     : 0.000877020 seconds fast of NTP time
Last offset     : +0.000998453 seconds
RMS offset      : 0.227384850 seconds
Frequency       : 7.671 ppm fast
Residual freq   : +0.112 ppm
Skew            : 19.082 ppm
Root delay      : 0.104019709 seconds
Root dispersion : 0.008999578 seconds
Update interval : 130.2 seconds
Leap status     : Normal
```

* Vérification état de la synchronisation NTP sur le `client2`

```bash

[remi@client2 etc]$ chronyc sources
210 Number of sources = 4
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^- 213.251.53.11                 2   8   377   101    -11ms[  -11ms] +/-   89ms
^+ genesis01.midways-networ>     2   8   377   231  -1076us[-1076us] +/-   42ms
^+ clients6.arcanite.ch          2   8   375    95    +12ms[  +12ms] +/-   86ms
^* cluster009.linocomm.net       2   8   377   681  -3901us[-4293us] +/-   29ms
[remi@client2 etc]$ chronyc tracking
Reference ID    : 5B795BA7 (cluster009.linocomm.net)
Stratum         : 3
Ref time (UTC)  : Sun Mar 17 19:29:33 2019
System time     : 0.000154373 seconds slow of NTP time
Last offset     : -0.000391279 seconds
RMS offset      : 0.005216185 seconds
Frequency       : 3.567 ppm fast
Residual freq   : -0.065 ppm
Skew            : 4.656 ppm
Root delay      : 0.055999756 seconds
Root dispersion : 0.004530263 seconds
Update interval : 129.6 seconds
Leap status     : Normal
[remi@client2 etc]$
```