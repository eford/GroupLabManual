+++
title = "Firewall & VPN"
# Type of content, set "slide" to display it fullscreen with reveal.js
type="page"
weight = 1200

# Creator's Display name
creatordisplayname = "Eric Ford"
# Creator's Email
#creatoremail = "ebf11 at psu dot edu"
# LastModifier's Display name
lastmodifierdisplayname = "Eric Ford"
# LastModifier's Email
#lastmodifieremail = "ebf11 at psu dot edu"
+++

# The new [Penn State Firewall]( https://news.psu.edu/story/507463/2018/02/27/impact/penn-state-migrating-next-generation-cybersecurity-firewall-platform)
(as of 11/29/2018)

1. The Global Protect VPN service no longer works.  You will need to download and install the Penn State AnyConnect VPN client ( http://kb.its.psu.edu/article/891)

2. SSH connections to internal college systems will need to connect through a SSH gateway/ jump server.  This server is ssh.science.psu.eduand will require you to use your PSU credentials.  Further information about using this server can be found here:  https://wiki.vpr.psu.edu/display/ECOSIT/Using+the+ECoS+SSH+Jump+Server.




# Installing VPN software for ubuntu

If you use the VPN, you can scp files directly from home to astro and even SSH keys work. So if you use SSH keys you don't even have to enter a password. In the official instructions for the VPN they tell you to install some third party program from Cisco, and at least on my Ubuntu laptop that program didn't work. I spoke with the helpdesk and Alan gave me instructions for Debian/Ubuntu that worked perfectly:


sudo apt-get install network-manager network-manager-gnome
sudo apt-get install openconnect network-manager-openconnect network-manager-openconnect-gnome
sudo systemctl enable NetworkManager.service
sudo systemctl restart NetworkManager.service


Most lines are probably redundant. I can't imagine that you don't have the network manager running already. Alan also suggested rebooting the computer but I certainly didn't need to. The key line seems to be the "openconnect" line. Apparently openconnect is what allows you to talk to Cisco VPNs. Apparently those use a different protocol that's not OpenVPN. Anway, after you've installed everything, do this:

1. Open the Network Manager (This will typically be available in your System Settings).
2. Add a new VPN connection for a Cisco compatible connection.
3. The name of the connection can be whatever you would like.  Move to the Identity tab and input only the following details and Save:
a) Gateway: vpn.its.psu.edu
4. Once on the Network Manager screen (or through the desktop Network Manager shortcut), connect to the VPN connection you just setup.
5. You should be asked for a username and password.  Enter your PSU ID and PSU password and click Connect.  You can choose whether or not to save these values.
6. You should now be successfully connected to the VPN.
7. To disconnect, use the Network Manager screen to slide the connection off, or use the desktop Network Manager shortcut to end the VPN connection.

## Copying files through the ECoS firewall w/o VPN

I find the new firewall to be particularly problematic when I wanted to scp some files back to Astro.  Fortunately, it is possible to scp files from ACI to computers on the astro network.  

You should be able to accomplish this using the ProxyCommand. For transferring files from ACI (LocationA) to your local machine (LocationC) through the science node (LocationB) the command would be:

```
scp -oProxyCommand="ssh -W %h:%p username@LocationB" /path/to/file/in/LocationA username@LocationC:/path/to/LocationC/destination
```

I just tested it while logged into aci-i, using `scp -oProxyCommand="ssh -W %h:%p ebf11@ssh.science.psu.edu" hello.txt ebf11@sagan.astro.psu.edu:`  and it worked for me.



