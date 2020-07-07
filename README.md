# Bruno's Arch Linux Instructions


![Screenshot2020-06-0723:49:03](https://user-images.githubusercontent.com/65104127/83988413-a9c5e880-a932-11ea-8aa0-16465fd28b61.png)

This guide was made by me (Bruno Montezano) to help myself when doing a fresh install of Arch Linux. It's going to list some of my core applications and tools that I use in a daily basis. All of them are essential to have my workflow going on. If you want to have a system that looks and function like mine, you can just follow the instructions below, and hopefully you'll have a fully functional Arch customized system.

## What do I need to do right after installing?

First thing I'm going to do is update the system and then, installing the sudo and vim package if it's not already installed:

```
pacman -Syu
pacman -S sudo vim
```

### Create a new user and let it use sudo

```
useradd -m -g wheel pepper
```

In this case above, I'm going to create a user called "pepper" that is a part of the wheel group, and have a home directory created by the -m flag. Then I can create a password for the user "pepper" with the command passwd, like:

```
passwd pepper
```

If I end up having some kind of problem when setting up the new account, I can use some of the user and group management tools like: useradd, userdel, groupadd, groupdel, etc.

Then, I'll edit the /etc/sudoers file with the vim text editor, and uncomment the line that let my account to run commands as sudo. The line I'm talking about is the following:

```
 # %wheel ALL=(ALL) ALL
```

### First, I'm going to install an AUR (Arch User Repository) Helper 

For me to do it, I have to clone the yay package out of Arch Linux website and then make this package using the command makepkg. Let's do it:

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Now I'm able to install some other packages that were not available in the official Arch Repository, like the font I use on my i3 setup, my bibliography manager, data analysis software, etc. 

## Now, let's install i3-gaps and some other applications

In order to install i3-gaps, I have to install Xorg and some other packages to i3 properly loads when it's time. The commands to change into the new "pepper" user and installing Xorg is going to be:

```
su pepper
sudo pacman -S xorg-server xorg-xinit
```

After Xorg installs, I'll install some packages that will make my i3 setup work when I finally get into it, they are the following:

```
yay -S i3-gaps i3blocks i3lock i3status lxappearance rofi exa feh cmus pavucontrol alsa-utils arandr git elinks newsboat qutebrowser picom pulseaudio pulseaudio-alsa scrot redshift mpv sxiv youtube-dl zip unzip unrar zathura zathura-pdf-mupdf vifm udisks2 usbutils transmission-gtk ttf-liberation ttf-hack ttf-dejavu neovim man-db man-pages htop galculator exfat-utils dmenu dialog imagemagick nmap wget nerd-fonts-mononoki ttf-font-awesome ttf-joypixels ttf-ms-fonts ttf-bitstream-vera deadbeef arch-wiki-docs arch-wiki-lite shell-color-scripts
```

Some of these packages are not actually necessary for you to have a working system. A lot of them are just applications that I like to use and I find myself having a good time with them.

### Now that I have the applications, I need to grab my configurations
