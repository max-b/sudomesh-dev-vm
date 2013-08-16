sudomesh-dev-vm
===============

For now, this is simply a place to hold an exported version of a virtual machine running OpenWRT so that folks can tinker with development on their own machines without any additional hardware. 

Unfortunately, it's somewhat incompatible with version tracking as any modifications to code won't be visible from the repository. Therefore, I'll probably just be leaving it mostly as is and setting up another repo with actual code.

Firing up the VM should be fairly easy. In VirtualBox you can go to File-&gt;Import Appliance, and you should be able to choose the .ovf file. The VM is currently setup to bridge the host machine's interface on "wan0". If your connection to your LAN (or the internet) is on a different interface, you should change this by clicking on "settings" and then going to "network". You should leave the "adapter 1" settings as is-they will allow your VM to connect to the internet through your host
machine. Change the "adapter 2" settings to match your host machine's interface.

After pressing start, the machine will boot up and you will enter be logged in. A list of log messages will appear, and you can press enter to go to the command line. As working within the VM console is a little limiting, it will probably be easiest to ssh into the machine from a separate terminal. It's currently configured with an ip address of 192.168.13. If your LAN is on the same subnet this should be fine, however, if it's on a different subnet you will have to adjust the network
configuration.

Assuming that your LAN is on 192.168.1.0, you should be able to:

```
ssh root@192.168.1.13
```

with a password: sudoer

### Httpd configurations ###

From a browser, if you navigate to 192.168.1.13, you should be presented with a login box. The user is "homeuser" and the password is "sudoer". This will eventually be the login that we would provide to home users-it will be different than the root account on the device.

### Luci Development ###

Luci is the framework that I think we'll be using to implement the web admin (and maybe some other things) on the router. Its a little tricky to navigate, parse, etc., but the learning curve isn't too bad. It's writeen in Lua, which is sort of a procedural language--it's kind of like javascript meets ruby (??), which has been pretty fun so far.

One thing that threw me for a while was that it's a little tough to get the web server to show any changes you make. I had to add this code to the /etc/init.d/uhttpd file:

```
rm /var/luci-indexcache
rm /var/luci-sessions/*
rm /tmp/luci-modulecache/*
```

That way it will delete any of the cache and it will serve you fresh code everytime you:

```
/etc/init.d/uhttpd restart
```
