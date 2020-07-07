# Bruno's Arch Linux Instructions


![Screenshot2020-07-0715:04:58](https://user-images.githubusercontent.com/65104127/86823544-5515aa80-c063-11ea-9b8a-c6c868611ed7.png)

This guide was made by me (Bruno Montezano) to help myself when doing a fresh install of Arch Linux. It's going to list some of my core applications and tools that I use in a daily basis. All of them are essential to have my workflow going on. If you want to have a system that looks and function like mine, you can just follow the instructions below, and hopefully you'll have a fully functional Arch customized system.

## What do I need to do right after installing?

First thing I'm going to do is update the system and then, installing the sudo, vim and git package if it's not already installed:

```sh
pacman -Syu
pacman -S sudo vim git
```

### Create a new user and let it use sudo

```sh
useradd -m -g wheel pepper
```

In this case above, I'm going to create a user called "pepper" that is a part of the wheel group, and have a home directory created by the -m flag. Then I can create a password for the user "pepper" with the command passwd, like:

```sh
passwd pepper
```

If I end up having some kind of problem when setting up the new account, I can use some of the user and group management tools like: useradd, userdel, groupadd, groupdel, etc.

Then, I'll edit the /etc/sudoers file with the vim text editor, and uncomment the line that let my account to run commands as sudo. The line I'm talking about is the following:

```sh
 # %wheel ALL=(ALL) ALL
```

### First, I'm going to install an AUR (Arch User Repository) Helper 

For me to do it, I have to clone the yay package out of Arch Linux website and then make this package using the command makepkg. Let's do it:

```sh
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Now I'm able to install some other packages that were not available in the official Arch Repository, like the font I use on my i3 setup, my bibliography manager, data analysis software, etc. 

## Now, let's install i3-gaps and some other applications

In order to install i3-gaps, I have to install Xorg and some other packages to i3 properly loads when it's time. The commands to change into the new "pepper" user and installing Xorg is going to be:

```sh
su pepper
sudo pacman -S xorg-server xorg-xinit
```

After Xorg installs, I'll install some packages that will make my i3 setup work when I finally get into it, they are the following:

```sh
yay -S i3-gaps i3blocks i3lock i3status lxappearance rofi exa feh cmus pavucontrol alsa-utils arandr elinks newsboat qutebrowser picom pulseaudio pulseaudio-alsa scrot redshift mpv sxiv youtube-dl zip unzip unrar zathura zathura-pdf-mupdf vifm udisks2 usbutils transmission-gtk ttf-liberation ttf-hack ttf-dejavu neovim man-db man-pages htop galculator exfat-utils dmenu dialog imagemagick nmap wget nerd-fonts-mononoki ttf-font-awesome ttf-joypixels ttf-ms-fonts ttf-bitstream-vera deadbeef arch-wiki-docs arch-wiki-lite shell-color-scripts nano
```

Some of these packages are not actually necessary for you to have a working system. A lot of them are just applications that I like to use and I find myself having a good time with them.

## Now that I have the applications, I need to grab my configurations

Currently, I have a reposity here on GitHub that I store my dotfiles (if you don't know what that is, you can access the repo and read it). I will use the git command to download the repository locally on my machine, and then put the files on the right place.

```sh
git clone https://github.com/brunomontezano/dotfiles
cd dotfiles
cp .vimrc ~
cp .bashrc ~
cp .bash-powerline.sh ~
cd .config
cp -r * ~/.config/
cd ..
cd .i3blocks
sudo mkdir /usr/share/i3blocks
sudo cp * /usr/share/i3blocks/
```

Disclaimer: If you are going to use my dotfiles, have in mind that if your user is not named "pepper", you'll have to rename some of the absolute paths that I have in my configuration files. Probably it's a really fast process that will take no time, but you have to pay attention.

### I will now install st (my terminal emulator of choice)

st is a terminal emulator made by the suckless guys, you can check other software they made on suckless.org. I make my build of st based on DistroTube's build, and just change the config.h file in order to have no transparency.

```
git clone https://gitlab.com/dwt1/st-distrotube
cd st-distrotube
vim config.h
```
 When you are inside the config.h file, you are going to change the line that has:
 
 ```c
 unsigned int alpha = 0xee;
 ```
 
 You are going to change the value to 0xff like it says on DT's file documentation. And then you can save the file, and still inside "st-distrotube" directory, you can compile st:
 
```sh
sudo make clean install
```

And it's done, you have st installed on your system.

## We are almost done! Let's make it even better!

Now that we have our main applications installed, we have our terminal emulator (st), we have our dotfiles inside our installation, what more do we need?

Well, it depends.

But I (Bruno) still gonna do some things.

### Vim Plugins

I will installl Vundle (Vim Plugin Manager) to be able to install my Vim plugins and use them with no problems.

```sh
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

After that, I can just open vim on my terminal and type the command to install the plugins.

```
:PluginInstall
```

### Master&Stack layout on i3 window manager

I'll use the script I have on ~/.config/i3/scripts. It's called autolayout.py, and what it does is make i3wm have a default layout (master&stack) that you would normally not have. That's a common feature on other window managers, like bspwm, dwm, xmonad, etc. So, in order to make it work, we'll have to install i3ipc and make the script executable. Let's go:

```sh
sudo pacman -S python-pip
pip install i3ipc
cd ~/.config/i3/scripts
chmod +x autolayout.py
```

### Create a .xinitrc

Now that we have our vim plugins working, the layout script executable, and i3ipc installed via pip, kind of the python package manager, and we already have on my i3 configuration file this script autostarting when we start i3-gaps, it's pretty much done. Let's just go into our home folder and create a .xinitrc file to Xorg know what to do when we call it.

```sh
cd ~
vim .xinitrc
```

And then inside this file you're going to put the following

```
exec i3
```

Then you can save it and relax.

## Will it work?

Probably. I would recommend you to reboot your system after all this, and then, to log in into your i3 setup, you can just type into your tty the Xorg command to initialize your graphic interface.

```
startx
```

And then, hopefully you'll be on your new system, probably without any wallpaper, that you can set putting a "wallpaper.jpg" file into the ~/img/ directory and then rebooting the system.

If it helped you, star the repository and give a feedback!

Have a great day!
