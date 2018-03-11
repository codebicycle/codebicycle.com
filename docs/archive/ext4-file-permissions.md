# EXT4 File Permissions

>Is there a religious or philosophical reason why you didn't format the data partition in NTFS?

Here's the problem. Let's say you change ownership of the mounted partition to "bart" on Ubuntu: sudo chown bart /media/Data. Now bart can add a file to the data partition.

Now you reboot into Fedora and let's say your username in Fedora is also bart. The problem is "bart" in Fedora is not the same as "bart" in Ubuntu because their uid's are different. Bart in Ubuntu has a uid = 1000 whereas bart in Fedora is 500 ( I think - it's been a while ) and bart in Suse may be something else.

You could leave the ownership as root but change permissions to 777: sudo chmod 0777 /media/Data. Then everyone in every OS can add to the partition.

But there's a bigger problem ahead. When bart on ubuntu saves a file to the data partition it will save as owner:group = bart:bart and with permissions of 644. bart can read and write to the file in ubuntu but everyone else in ubuntu can only read. Since bart on Fedora has a different uid he can read the file but cannot edit the file.

You've got some options at this point. You could change the uid's of bart in every system to the same value so that bart = bart. You could change the umask in bashrc in every OS to 000 instead of 022 so that every file saved saves with permissions of 666 - which is the sign of the devil and is frowned upon. There are more complex solutions as well.

Or you could format the partition as NTFS. Then every OS will mount the partition thinking they own it - sort of like a usb stick - only internal.



>It's not really an extra step as such, it's just that Ext filesystems support Linux file/directory ownerships and permissions, and therefore their ownership can be handled just like any other file or directory on your system.

It's the NTFS partition that needs the extra step of configuring the permissions at mount time for the whole partition (through fstab) since NTFS isn't able to handle the permissions on it's own.
