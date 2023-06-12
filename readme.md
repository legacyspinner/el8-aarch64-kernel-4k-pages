Wow , I just love to fix stuff that is not broken and to break stuff that is fixed!  :) As told by: My old boss.
<hr>

# To test it in a virtual environment on a el8.x aarch64 install. 

For example, if you have
a el8-aarch64 installed already in UTM on a Apple M1 but its running in software mode.
That was the only way you could normally install 7/8 in UTM.
In UTM I have 8 cores enabled with 8G memory.


Now, you can install a new kernel or upgrade the old one and test with 4K pages.

It seems really fast to me, now with 'Use Hypervisor' ticked.
*Compared to when it was using softmmu, this and the 4K build are both SMOKING-FAST.
*This is like real decent aarch64 speed now for development, no cross needed. Seems to have brought
out the potential of the machine, I'm very happy with my compile testing so far.

I assume this is the mac equivalent of KVM, but I could be wrong.

This is the 4K pages version, not fully optimised for the m1, but works fast.
*I also built a 16K pages version, based on apples m1 Native HW. 
Kernel pages is aka granular kernel* 

I did this so I could build faster packages for the Rpi's, before It would take me over a day to compile
a kernel native on a RPi4, or a not very long with CROSS ofc, but I dont want to use cross. I wanted NATIVE
and now I have it! For testing only ofc, bugs included! Soon, I'll get back to my goal when I started this, 
which spawned from another project. 




See for yourself! Ready set go?
<hr>
<hr>
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
Don't try the new kernel yet, until you check that "Use Hypervisor" box in UTM.
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-boot.png?raw=true)

Go ahead and shut down and enable better/faster/stronger Virtualization on your Mac M1 now :)
This is what you came for right? Then tick that little box that reads:
<code>
"Use Hypervisor"
</code>

*Ofc, we always wanted to 'use Hypervisor' on our aarch64/arm64 machines, now we can with all the el's  *7/8/9 :)
*7 yet to be rebuilt, but its easy peasy.

  ![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-VIRT-TICK.png?raw=true)

Then start up the machine again and you can check a couple things:
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-1.png?raw=true)

Dmesg output:

![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-dmesg1.png?raw=true)
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-dmesg2.png?raw=true)

Yes, that is 8 cores baby!
![8.8-on-Apple-Mac-M1-using-UTM](/assets/images/8.8UTM-dmesg-8cores.png?raw=true)


Enjoy!

