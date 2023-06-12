To test it in a virtual environment on a el8.x aarch64 install. 

For example, if you have
a el8-aarch64 installed already in UTM on a m1 but its running in software mode
and you want to try this kernel and test . 

Then check the virtualization box in UTM for the installation
and then install to new kernel as follows.


From your test install:

create the repo:
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
yum update kernel


Reboot and check, if all went well:
<code>
uname -a
</code>

Linux r85aarch64min 4.18.0-477.13.1.el8_8.1_4K_pages.aarch64 #1 SMP Sat Jun 10 21:40:04 EDT 2023 aarch64 aarch64 aarch64 GNU/Linux


*If you ‘still’ get a grub error complaining about 64K slices, try updating with grubby and/or grub2-mkinstall. I will rebuild a new image soon to try and fix that. You can do the same, 
just add the repo specs to your kickstart and respin.
