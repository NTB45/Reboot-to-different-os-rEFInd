# Reboot-to-different-os-rEFInd

### Filler
So, after looking at Darkhogg's "Reboot to {OS}" scripts for rEFInd Next Boot selection scripts I realised that that method doesn't work for me.

I could not find the PreviousBoot file at /sys/firmware/efi/efivars.

So, I started looking around the rEFInd efi directory and voila Its in the /boot/efi/EFI/refind/vars directory.

## How to do it

So instead of modifying the contents of the file 

I decided to take the easy route and just replace the file with the one that makes rEFInd think that a different os was running before.

### Retrieving the files

Getting the PreviousBoot file in linux (that will reboot to linux) is simple

Just copy /boot/efi/EFI/refind/vars/PreviousBoot file to somewhere safe and readable by Windows(ntfs partition prefered)

For Windows it gets a bit trickier 

First you will have to mount the EFI partition with the command 

> mountvol P: /S

but even if its mounted its not visible in the file explorer ,only available from command line, but it was visible when i opened the task manager's new task's browse option.

Well, its good enough to do basic file managing.

Copy the same refind/vars/PreviousBoot file to somewhere safe and readable by linux

Also, The data in files is stored in UTF-16 character encoding

### Replacing the files
well, to replace these files, just get the PreviousBoot file taken out from linux boot and copy it to rEFInd's vars directory.

To do this I made a few short scripts that gets the job done. You can add shutdown or reboot command too in the end

### Windows
Windows.bat
>mountvol P: /S

>copy /y D:\location\of\linux\PreviousBoot P:\EFI\refind\vars\PreviousBoot

For windows save these commands in a .bat file and go to properties then advanced then select run as administrator always

### Linux

>sudo cp -f /home/user/path/to/Windows/PreviousBoot /boot/efi/EFI/refind/vars/PreviousBoot

For linux save it in a .bash file and make it executable in its properties

### Thanks
Thanks to @Darkhogg for his Reboot to {OS} scripts https://gist.github.com/Darkhogg/82a651f40f835196df3b1bd1362f5b8c to give me the idea and the file's character encoding

Thanks to Superuser.com's user patkim for the tip of accessing efi directory from task manager's run browse option

this is copy of this gist made by me https://gist.github.com/NTB45/49576c74b557e3c2da90238c1ae5564f
putting it in a repo would
