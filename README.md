# Bruno's Arch Linux Instructions


![Screenshot2020-06-0723:49:03](https://user-images.githubusercontent.com/65104127/83988413-a9c5e880-a932-11ea-8aa0-16465fd28b61.png)

This guide was made by me (Bruno Montezano) to help myself when doing a fresh install of Arch Linux. It's going to list some of my core applications and tools that I use in a daily basis. All of them are essential to have my workflow going on. If you want to have a system that looks and function like mine, you can just follow the instructions below, and hopefully you'll have a fully functional Arch customized system.

## What do I need to do right after installing?

First thing I'm going to do is update the system and then, installing the sudo package if it's not already installed:

```
pacman -Syu
pacman -S sudo
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

## Now, let's install i3-gaps

In order to install i3-gaps, I have to install Xorg and some other packages to i3 properly loads when it's time. The commands to change into the new "pepper" user and installing Xorg is going to be:

```
su pepper
sudo pacman -S xorg-server xorg-xinit
```
