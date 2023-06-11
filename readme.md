EL8 aarch64 kernel with 4K cpu pages enabled. 
*Warning: This is only intented for testing as I built it with kabichk disabled.

I made this to test on the apple m1 with UTM with 'hypervisor' set to on.
The machine  expects 4K or 16K pages but the default in el8 is detected as 64K.


Compile your own with:
<code>
#!/bin/sh
rpmbuild -ba --target=$(uname -m) kernel.spec \
--without debug \
--without debuginfo \
--without kabichk \
kernel.spec 2> build-err.log | tee build-out.log
</code>

*Note: patches have been included for testing seperate but are already in the SRPM/Source.
Debug patch included too incase you want to rebuild with that enabled.
<hr>
<hr>
*Its unrelated to the rebuilt kernel-4k itself. I should mention for anyone else trying
to rebuild/clone. 
The build host for this subproject:
Built on rocky-8.x minimal, that was upgraded to later versions. 
For now, I'm((all me im sure, TM) having issues with 'initial' rocky-aarch64-min iso installs 
on rocky spins>8.x   ***Someone else suggested it might be a ks issue.
IDK, yet. It could also be an issue with my aarch64-kvmhost or unknown.


*Here's what I will say for now about starting with aarch64 iso's and me:

8.3 works: INITRAMFS OK! but is a known dev version with warnings in "ISSUE"-DO NOT START/BUILD WITH/FROM THIS ONE

8.4 works: INITRAMFS OK! older release, newer working for 'me'

8.5 works: INITRAMFS OK! older release, newer working for 'me'

8.6 works: INITRAMFS OK! best one so far to start with for 'me'. 
                          -Tested 2nd round, OK. (460 rpm pkgs)
                          <p>
   
   ![alt text](/rocky-8.6-aarch64-iso-install.png)
   
   
  
  
  ![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
  
  




![test](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
  

8.7 works: INITRAMFS OK! Software default install selections appear to have changed.WORKS. 
                          best one so far to start with for 'me'.

8.8 TESTING

*If these all work,SPECULATION: I could assume I had a EFI firmware fart that somehow followed up by cascade failing subequent attempts.
Then , I could have rebooted/refresh the firmware, and got good installs after. retesting still.
Trying to trigger the issue again!

<br>

So I just working around some issues building, for now instead of:
trying to fix everything on the planet route first. 
Some bridges you just cross instead of trying to hammer every
nail that is sticking up.
People get mad at me if/when I even happen to mention it 'could be' a bug that is not ME(TM) ,

Often then this happens,asking next lines;
 -did you fix it?
 -where is your patch(s)?
 -did you join the forumns and post it?
 -why didn't you post the error?
  then
 -why did  you mention it?
 -etc, etc, etc, etc. etc
  done!

I will explain what it took later to do what, in more detail.
All bridges do not belong to me, nor is it my duty to go saying others bridges need work.
I do not get paid to do that!

I know how to cross bridges without meeting Billy Goat Gruff each time, besides it is not always under the bridge! thank you!
