---
title: My journey from Windows to Linux
---

Recently I became inspired to give up Windows and move to Linux. There were many benefits, it looks nicer, can run lighter, it's free and it provides a better and more flexible development environment. There was just one thing holding me back - I occasionally like to play games on my PC. This caused problems for me, there was no native Linux version of my game of choice (World of Tanks) available for Linux and this was really all that was holding me back. Recently I learned of a way to get some programs and games working in Linux and so I decided to make the switch. Below is the process I went through to wind up with my current setup.

Before I settled on my distro I tried a few to find one that I liked. There were three main ones:

* [Linux Mint](http://www.linuxmint.com) - This is a very pretty distro but for some reason I just didn't really want to stick with it.
* [Crunchbang](http://crunchbang.org/) - I really liked this distro, it's insanely customisable, insanely lightweight and I found it intuitive. The only problem with crunchbang was that it's Debian based and I found compatibility issues with some things which led me to my final distro:
* [Ubuntu Gnome](http://ubuntugnome.org/) - After recommendation from a friend and with Linux seeming to be all about Ubuntu these days I gave Ubuntu Gnome a go. It is standard Ubuntu but running the Gnome desktop manager instead of Unity. Once I tried Ubuntu Gnome I knew this was going to be the distro I was sticking with.

#### INSTALLING THE OS

Before I went and deleted all my old partitions from my Windows drive I had a play around with Ubuntu Gnome in a VirtualBox VM just to see if I really liked it. I found a base look that I liked and knew that I would be able to implement it when I moved my desktop OS to Ubuntu. I installed the Ubuntu Gnome image to a thumb drive using [UNetbootin](http://unetbootin.sourceforge.net/), restarted my computer and I was away. I chose to do updates through the installation process so installation took a little while longer than normal but after installation I was presented with a much more updated version than the CD image provided.

First things first, updating the remaining packages.
```
$ sudo apt-get update; sudo apt-get upgrade
```

Because I'm running an NVIDIA GTX 760 I wanted to get some proprietary drivers so that I could make the most of the card, including a better framerate when I got into the games. I decided to go with NVIDIA's own drivers, available [here](http://www.nvidia.com/object/unix.html) (or [here](http://www.nvidia.com/Download/index.aspx?lang=en-us) by putting in what sort of card you have). I downloaded the correct ones for my system and then had to go through quite the process to get them installed:

To modify video drivers you can't have an X server running so press `Ctrl`+`Alt`+`F1` and login as your user.
Kill the current X server
```
$ sudo service gdm stop
```
Next you will need to remove any NVIDIA drivers the system installed.
```
$ sudo apt-get purge nvidia-*
```
Change to the directory where you downloaded the NVIDIA driver setup and issue:
```
$ sudo sh NVIDIA*
```

The above command will run the installer. Answer yes to all the prompts and the driver will install. It should also ask you if you wish to run nvidia-xconfig. Make sure you answer yes to this so your X server is configured to use your new graphics driver.
I had much trouble with this and it took me a lot of googling and reading many random articles to figure out how to get it all working, hopefully these instructions work for you as well.

After completing the above you should restart your computer by typing `$ sudo reboot`.

#### DEVELOPMENT

For my development environment I use a good text editor and the terminal a lot. My favourite text editor at the moment is [Sublime Text](http://www.sublimetext.com/), and as the name suggests it is sublime. I am currently using version 3 and the installer is available from the website.

To have a development environment we must have something to develop for. Go ahead and run the following:
```
$ sudo apt-get install php5 php5-mcrypt php5-json php5-mysql php5-gd mysql-server apache2 phpmyadmin php5-dev php5-curl
```

You don't have to install phpMyAdmin but I just find it handy to have so that I can easily work with my MySQL databases.
[Jason Lewis](http://www.jasonlewis.me) wrote a small shell script to automatically create Virtual Hosts for Apache but I found that it didn't work correctly for Ubuntu 13.10 so I forked it and fixed it, it is available [here](https://gist.github.com/matmunn14/8766759).

I also use Xdebug, just to make PHP error outputs a bit prettier and easy to read. The website is also able to generate you custom installation instructions if you paste the output of your `phpinfo(); ` into [this page](http://xdebug.org/wizard.php).

Next you should download and install Composer.
```
$ curl -sS https://getcomposer.org/installer | php
$ mv composer.phar /usr/local/bin/composer
```

If you don't have cURL installed you will need to install it with apt-get.
```
$ sudo apt-get install curl
```

#### GAMES

To get World of Tanks running on Linux I use PlayOnLinux, you can download it from [here](http://www.playonlinux.com/en/download.html). Once installed I clicked the Install button and found World of Tanks in the list. Once the game is installed it will begin the update process, there may be a problem with this as the default update mode is through torrents. After many google searches it seemed that it was a common problem and the workaround is to click the spanner in the top right in the updater and then untick the box that says 'Allow torrents'. After that the game should update properly. There are a couple more tweaks you can perform to get the game working better:

* Firstly, choose a CSMT version of Wine. To do this open up the PlayOnLinux main window, click World of Tanks and then click Configure in the right hand panel. Next to Wine version click the little plus and then choose the newest version of Wine that has CSMT. At the time of writing it was 1.7.10-CSMT-a632585. Click the little right arrow and it should install. You can then exit the Wine versions manager and you can choose your new version of Wine from the dropdown list. We've chosen a CSMT version of Wine, but by default CSMT isn't enabled so now we have to enable it. In the configuration window go to the Wine tab and open up Registry Editor. Navigate yourself to `HKEY_CURRENT_USER\Software\Wine\Direct3D`. You need to create a new String Value and set the title to "CSMT" and set the value to "enabled".
* Make sure PlayOnLinux can recognise your video card, go to the Install Components tab in the configuration, scroll down to VideoDriver and click Install.
* Finally, if you run an NVIDIA card go to the Miscellaneous tab and enter the following string in the "Command to exec before running the program":
```
export LD_PRELOAD="libpthread.so.0 libGL.so.1"
export __GL_THREADED_OPTIMIZATIONS=1
```

To speak with my friends playing games I also installed [TeamSpeak](http://www.teamspeak.com/?page=teamspeak3). I installed TeamSpeak to `~/bin/TeamSpeak3-Client-linux_amd64` and then I had to make a `.desktop` file in `/usr/share/applications`.
```
[Desktop Entry]
Version=3.0.13.1
Name=TeamSpeak 3 Client
GenericName=TeamSpeak
Exec=/path/to/bin/TeamSpeak3-Client-linux_amd64/ts3client_runscript.sh
Terminal=false
X-MultipleArgs=false
Type=Application
Icon=/path/to/bin/TeamSpeak3-Client-linux_amd64/pluginsdk/docs/client_html/images/logo.png
StartupWMClass=TeamSpeak
StartupNotify=true
```

#### NICETIES

##### CONKY

When I was trialling CrunchBang I fell in love with an application called Conky. It is a highly configurable system monitor that can display all kinds of stats about your machine on your desktop.
To install Conky all you have to do is issue:
```
$ sudo apt-get install conky
```

After installation open the file ~/.conkyrc in your preferred plaintext editor and play around with all the options. My .conkyrc file is available at https://gist.github.com/matmunn/9143677.

(Removed the image)

##### GNOME EXTENSIONS

There are a few things that GNOME doesn't do so well or I wish were done a little bit differently, so I have used a few extensions to get a look I am pretty happy with. Extensions are available at https://extensions.gnome.org.
Extensions that I use are:

* [AlternateTab](https://extensions.gnome.org/extension/15/alternatetab/)
* [Alternative Status Menu](https://extensions.gnome.org/extension/5/alternative-status-menu/)
* [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
* [Remove Accessibility](https://extensions.gnome.org/extension/112/remove-accesibility/)
* [Status Area Horizontal Spacing](https://extensions.gnome.org/extension/355/status-area-horizontal-spacing/)
* [TaskBar](https://extensions.gnome.org/extension/584/taskbar/)
* [TopIcons](https://extensions.gnome.org/extension/495/topicons/)
* [User Themes](https://extensions.gnome.org/extension/19/user-themes/)
