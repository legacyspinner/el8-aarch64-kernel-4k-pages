To test it in a virtual environment on a el8.x aarch64 install. 

For example, if you have
a el8-aarch64 installed already in UTM on a Apple M1 but its running in software mode,
which is the only way you can normally install 7/8 in UTM.

Now, you can install a new kernel or upgrade the old one and test with 4K pages.

It seems really fast to me, now with 'Use Hypervisor' ticked.

*I assume this is the mac equivalent of KVM, but I could be wrong, I'm sure I will be corrected if so!

I also have 8 cores enabled with 8G memory.

*Next up lets see how fast the M1 can go on UTM with el8, with native 16K pages, w00t!


*At some point I'll get back to my goal when I started which was another project, soon I will
and hopefully now I can make arm packages NATIVE and FAST, yes I did say NATIVE/FAST ARM, without using cross :)

On your UTM installed el8, to test/install to new 4K pages kernel:


From your test install(not production box):

create the file for the repo @:
<code>
/etc/yum.repos.d/el8-aarch64-4k-pages.repo
</code>

with the contents:
<code>
[el8-aarch64-4k-pages]
name=el8-aarch64 w/4k CPU PAGES repo 
baseurl=https://sourceforge.net/projects/el8-aarch64-4k-pages-repo/files/dnf/8/
gpgcheck=0
enabled=1
</code>

Then run:
<code>
yum install kernel
</code>

Reboot and check, if all went well:

If so you should see the following or similar.
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-boot.png?raw=true)

Go ahead and shut down and enabled better/faster/stronger Virtualization on your Mac M1 now :)
This is what you came for right? Then tick that little box that reads:
<code>
"Use Hypervisor"
</code>

*Ofc, we always wanted to 'use Hypervisor', now we can. :)

  ![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-VIRT-TICK.png?raw=true)

Then start up the machine again and you can check a couple things:
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-1.png?raw=true)

Dmesg output:

![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-dmesg1.png?raw=true)
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-dmesg2.png?raw=true)

Yes, that is 8 cores baby!
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-dmesg-8cores.png?raw=true)


Enjoy!

