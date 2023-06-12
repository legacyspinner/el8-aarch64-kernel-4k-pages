To test it in a virtual environment on a el8.x aarch64 install. 

For example, if you have
a el8-aarch64 installed already in UTM on a Apple M1 but its running in software mode,
which is the only way you can normally install 7/8 in UTM.

Now, you can upgrade that and test with 4K pages.
It seems really fast to me, now with Virtualiazation ticked.
I also have 8 cores enabled with 8G memory.

*Next up lets see how fast the M1 can go on UTM with el8, with native 16K pages, w00t!

Then check the virtualization box in UTM for the installation
and then install to new kernel as follows.


From your test install:

create the file for the repo:
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
