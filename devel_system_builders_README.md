CONSTRUCTION BELOW IS FOR DEVEL/SYSTEM BUILDERS ONLY!

EL8 aarch64 kernel with 4K cpu pages enabled. 
*Warning: This is only intented for testing as I built it with kabichk disabled.


REFS:

https://www.kernel.org/doc/html/latest/arm64/memory.html

https://www.kernel.org/doc/html/v5.8/arm64/booting.html

https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/arm64/memory.rst

https://lwn.net/Articles/660632/

https://opensource.com/article/20/12/52-bit-arm64-kernel


I made this to test on the apple m1 with UTM with 'hypervisor' set to on.
The machine  expects 4K or 16K pages but the default in el7/8 is detected as 64K.


* Current RPMS in the 4K repo now were built with mock, see logs at sf repo.

Compile your own with mock with:
<code>
mock -r rocky-8-aarch64 kernel-4.18.0-477.13.1.el8_8.2_4K_pages.src.rpm --without debug --without debuginfo --without kabichk --enablerepo=devel
</code>


Compile your own using manual method with:
<code>
rpmbuild -bb --target=$(uname -m) kernel.spec --without debug --without debuginfo --without kabichk kernel.spec 2> build-err.log | tee build-out.log
</code>
*Then followup with the -bs if you need it.

*Note: patches have been included for testing seperate but are already in the SRPM/Source.
Debug patch included too incase you want to rebuild with that enabled.


*Its unrelated to the rebuilt kernel-4k itself, but as a pre-req I should mention for anyone else trying
to rebuild/clone. 

The build host for this subproject:
Built on rocky-8.x minimal, that was upgraded to later versions. 
For now, I'm((all me im sure, TM) having issues with 'initial' rocky-aarch64-min iso installs 
on rocky spins>8.x   ***Someone else suggested it might be a ks issue.
IDK, yet. It could also be an issue with my aarch64-kvmhost or unknown.


Subject to change:
*Here's what I will say for now about starting with aarch64 iso's and me:
Works, doesnt mean I tested everything, just means it booted/installed and then booted again.

8.3 works: INITRAMFS OK! but is a known dev version with warnings in "ISSUE"-DO NOT START/BUILD WITH/FROM THIS ONE

8.4 works: INITRAMFS OK! older release, newer working for 'me'

8.5 works: INITRAMFS OK! Working.Minimal Issues

8.6 works: INITRAMFS OK! Works for me but console can detach.
   
   ![8.6](/assets/images/rocky-8.6-aarch64-iso-install.png?raw=true)




8.7 boots: INITRAMFS: Fails on my setup using rocky 8.7:
![8.7](/assets/images/87no.png?raw=true)

*Note: ALMA 8.7 #1 on alma also fails, with a different error:
<code> error: ../../grub-core/kern/disk_common.c:47:attempt to read or write outside
of disk `cd0'.
error: ../../grub-core/loader/arm64/linux.c:304:you need to load the kernel</code>

Alma 8.7 has another iso: AlmaLinux-8.7-update-1-aarch64-minimal.iso
*That one fails for me with the same error in rocky 8.7
![alma 8.7](/assets/images/alma87no.png?raw=true)


8.8 boots: INITRAMFS: Fails on my setup using rocky 8.8:
![rocky 8.8](/assets/images/88rockynope.png?raw=true)

Alma 8.8: INTRAMFS: Fails on my setup.
![alma 8.8](/assets/images/88almanope.png?raw=true)

*Point is, I have to start with a version <= 8.6*, then upgrade it.
