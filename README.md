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
