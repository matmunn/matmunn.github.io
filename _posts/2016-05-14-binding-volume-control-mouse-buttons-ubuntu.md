---
title: Binding volume control to mouse buttons in Ubuntu (and Arch)
---

I use a Logitech MX Master mouse and under Windows the Logitech software allows me to set the buttons on the side of the mouse to do things like controlling the volume, which I much preferred over using the buttons for forwards and backwards. This was something that I hadn't been able to solve until now and I've listed my process below.

First you'll need to install xev, xbindkeys and xautomation.

```
$ sudo apt-get install xbindkeys xev xautomation
```

xev was already installed for me so you might not need to install it.

Next you'll need to find the right mouse buttons by using xev. Start xev from the terminal.

```
$ xev
```

You'll be presented with a small white box.  This box can track keyboard and mouse events so hold your mouse over the box and press the button. You should see some output similar to that below:

![](/img/screenshots/Selection_009.png)

What you need to pay close attention to is the button number.

I want my mouse to control the volume for whatever device I happen to be using at the time (I switched between a headset and speakers) and all I really want to do with the mouse buttons is emulate pressing the media keys on a keyboard.

Firstly, you'll need to create a `.xbindkeysrc` file in your home directory. You can also use the defaults provided by xbindkeys but I didn't like the bindings and so I started with a blank file.

```
$ xbindkeys --defaults > ~/.xbindkeysrc
```

or

```
$ touch ~/.xbindkeysrc
```

Below are the commands I use to control my MX Master. The buttons may be different for your mouse.

```
# Lower volume on thumb wheel down
"xte 'key XF86AudioLowerVolume'"
  b:7

# Raise volume on thumb wheel up
"xte 'key XF86AudioRaiseVolume'"
  b:6

#Toggle play with thumb button
"sleep 0.1 && xte 'key XF86AudioPlay'"
  m:0xc + c:23

# backward button => previous song
"xte 'key XF86AudioPrev'"
   b:8

# forward button => next song
"xte 'key XF86AudioNext'"
   b:9
```
For some reason a small sleep was required on the thumb button so that it didn't double trigger the event.

Save the file and then start xbindkeys.

```
$ xbindkeys
```

You should now be able to control the volume of your computer using the buttons on your mouse.


I've since switched to Arch, these instructions remain the same, however you obviously have to substitute `apt-get install` with `pacman -S` and the packge name for `xev` is `xorg-xev`, the other two remain the same.
