<a href="https://masoncyber.github.io/docker/" target="_blank">
    View Project 2
</a>



# Arch Linux Beginning

  I first Downloaded the iso from arch Linux by using the wiki, and using the first link in the United States mirror site. 

## Downloaded

  Next after downloading the iso I booted up VMware, and started the Install Process. after getting into arch Linux I when pressed enter to get into the install phase

## Install Process

  
On VMware, you create a new virtual machine, go to installer disc image file (iso): put the ISO you downloaded. 
Next.
Guest operating system: Linux
Version: Other Linux 5.x and later kernal 64-bit

Name it Virtual Machine, 
Disk capacity being 20 GB and give more memory of 2GB

finally boot up and click enter to get into the Terminal of Linux


## Terminal of Linux


### First
--------------------------------------------------------------------------
In the terminal, you are going to partition the disk.

	cfdisk /dev/sda. select gpt

On free space, make a new one with a size of 1M (this being your boot loader). You will also need to make the type BIOS boot

Next select a new free space, give it 4G of memory and type of Linux Swap

Finally with all your free space make just click enter it will auto make into Linux filesystem. 

After all this is done you need to go over in the options and Write partition table to disk.  

After confirmations quit. 

### Second
------------------------------------------------------

You will need to format the partitions

	 mkfs.ext4 /dev/sda3

		mkswap /dev/sda2

		swapon -a (enabling the paritions)
### Third
--------------------------------------------------------

Next is mount the data partitions. The directory is already made

	 cd /mnt
 in the mnt folder make the disk
 
	mount /dev/sda3 /mnt

next copy the system files to the mnt folder

put the  s: 

	pacstrap /mnt base linux linux-firmware nano grub dhcpcd

(time to download these might take a little bit)

Need to now generate the fstab file

	 genfstab /mnt >> /mnt/etc/fstab

mnt directory now needs to be the root 

	  arch-chroot /mnt

set a password for the administrator

	 passwd
    (type new password)
	
### Fourth
-------------------------------------------------------

Now we need to install grub

	 grub-install /dev/sda

configure grub now

	 grub-mkconf ig -o /boot/grub/grub.cfg

now you need to exit and reboot

	exit

	reboot

Now you have the grub boot loader. log in as root, with your password you set early

### Fifth
--------------------------------------------------------


Now we need to make network connectivity  

First test it by 

	 ping -c 2 archlinux.org

Next now to fix it by putting in 

	 systemctl start dhcpcd

now wait a few seconds.

try to ping again

		  -c 2 archlinux.org 


If that works, we need to now enable it 

		 Systemctl enable dhcpcd

### Sixth
--------------------------------------------------------

Now to configure Pacman type the 

	 nano /etc/pacman.conf

You will be brought up a new terminal tab. Scroll all the way down to the bottom, you will see 

	"#[multilib]"
	"#Include = /ect/pacman.d/mirrorlist"

Get rid of the hashtags of those two.
It Should look like this 

    [multilib]
	  Include = /ect/pacman.d/mirrorlist

now CTRL X, and exit and save

Now when your back to the main terminal 

type the the   to redownload all package database files

		  pacman -Syy

Now it is done, We can now ssh!

	 systemctl start sshd
	 systemctl enable sshd

Now add a user!

	 useradd -m (your username)

	passwd (your username)

type in password

now ssh to your user!

	 ssh (yourusername)@localhost

To you are longed into your user!


If you want to download a desktop environment you can do so! Now for example if you want to download gnome all you need to do is

		 pacman-s gnome dgm

then

		systemclt enable dgm (which is gnome)

now the next time you reboot you can go into your desktop environment. 






