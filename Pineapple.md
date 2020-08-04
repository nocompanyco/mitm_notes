http://172.16.42.1:1471/
default route is .42 so `~/bin/dhcpserver.sh eth1 172.16.42.42 1` to provide internet

Reset to factory firmware (or last version updated to)
  - hold button 7 seconds, or Configuration / sub menu of general config
Setup disk locally with gparted and ext4 filesystem then just add it to the device
For using internet upstream via extra USB wifi, the dongle should show as wlan2
(wlan0 and wlan1 are for pineapple management and pineap scanning)

# Diskspace
diskspace is sensitive even with sd card

After factory rest:
  overlayfs:/overlay        1.3M    264.0K   1016.0K  21% /
After installing `sslsplit` dependencies
  overlayfs:/overlay        1.3M    532.0K    748.0K  42% /
  What it installs:
    ~ # cat /pineapple/modules/SSLsplit/scripts/dependencies.sh
    opkg update
    opkg install sslsplit --dest sd
    opkg install openssl-util --dest sd
    opkg install libevent2 --dest sd
    opkg install libevent2-core --dest sd
    opkg install libevent2-extra --dest sd
    opkg install libevent2-openssl --dest sd
    opkg install libevent2-pthreads --dest sd
After installing `p0f` dependencies:
  overlayfs:/overlay        1.3M    564.0K    716.0K  44% /
After install `PortalAuth` dependencies:
  /bin/sh /pineapple/modules/PortalAuth/includes/scripts/depends.sh -install
  overlayfs:/overlay        1.3M    728.0K    552.0K  57% /

Modules we want to explore:
  - sslsplit  https://github.com/droe/sslsplit
  SSLsplit is a tool for man-in-the-middle attacks against SSL/TLS encrypted network connections.
  - Evil Portal - An Evil Captive Portal.	
  - P0f https://lcamtuf.coredump.cx/p0f3/
  is a OS Fingerprinting and Forensics Tool that utilizes an array of sophisticated, purely passive traffic fingerprinting mechanisms to identify the players behind any incidental TCP/IP communications (often as little as a single normal SYN) without interfering in any way.
  - Portal Auth	2.0	Captive portal cloner and payload distributor.	
  - DNSspoof	1.7	Forge replies to arbitrary DNS queries using DNSspoof	
  - tcpdump: we need this to review what is going on more easily (without having to mitm on workstation)
    add this filter: not tcp port 22 and not tcp port 1471

Maybe modules to be explored later:
  - Responder an LLMNR, NBT-NS and MDNS poisoner.  https://github.com/SpiderLabs/Responder
  - get	1.2	Profile clients through the browser plugins supported by their browser
  - DNSMasq Spoof	1.2	Forge replies to arbitrary DNS queries using DNSMasq
  - CursedScreech	1.6	Securely control compromised systems.
  - Meterpreter	1.1	meterpreter configuration utility

TCPDUMP filter:
  `not tcp port 22 and not tcp port 1471`
avoids ssh and management interface
Review on device:
  `tcpdump -ttttnnr /pineapple/modules/tcpdump/dump/dump_1596113737.pcap`

Network interfaces: 
  https://forums.hak5.org/topic/39689-wlan0wlan1-on-nano/
  - Wlan0 is for running the Open AP (hidden by default, used for pulling clients in), and Management AP (the WPA2 one you set up on first boot).
  - Wlan1 is usually used in monitor mode in conjunction with PineAP, Recon, or other modules and tools.

Test Initial:
- PineAP: turn on PineAp daemon with `Allow associations`
- PineAP: turn off `Capture SSIDs to Pool` and then add only the SSID's you want to capture
- iphone se2 mac (nathans) `48:26:2C:5F:4E:C8` can be found in Clients page
- Configure: switch on `landing page` https://softwaretester.info/create-landing-pages-for-wifi-pineapple/
  add `echo 'hi';` to the content
  NOTE: if you have `Evil Portal` installed use that instead. (create `basic` portal on SD and then restart Evil Portal)
- reconnect to the mitm ssid and try to go to an http site like http://detectportal.firefox.com
NOTE: Maybe do this before installing any modules (we try now with only p0f tcpdump and sslsplit installed) <- DID NOT WORK

# Evil Portal
Failed at first. Despite getting it to show on http://.172.16.42.1 could in no method get a iphone or android client to inject it

Finally it worked. After restart and not providing IP's via laptop interface (ip's provided by upstream)
Worked on Android by on iphone had to visit a non ssl link


# sslsplit
couldn't get it work
ps shows:
  /bin/sh /pineapple/modules/SSLsplit/scripts/sslsplit.sh start
  sslsplit -D -l /pineapple/modules/SSLsplit/connections.log -L /pineapple/modules/SSLsplit/log/output_1596118060.log -k /pineapple/modules/SSLsplit/cert/certificate.key -c /pineapple/modules/SSLsplit/cert/certificate.crt ssl 0.0.0.0 8443 tcp 0.0.0.0 8080
manual setup information: 
  https://champagneandsecurity.wordpress.com/2014/07/26/sslsplit-on-wifi-pineapple/
perhaps we just try by hand: https://www.roe.ch/SSLsplit

# p0f works
/sd/usr/sbin/p0f -f /etc/p0f/p0f.fp -i wlan0

results can be sometime sstrange
https://null-byte.wonderhowto.com/how-to/hack-like-pro-use-new-p0f-3-0-for-os-fingerprinting-forensics-0151703/