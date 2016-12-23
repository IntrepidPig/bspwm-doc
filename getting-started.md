# The BSPWM Getting Started guide

In this guide I will walk you through installing BSPWM and configuring the basics to have a functional system. A more in depth documentation of BSPWM will be available at the full documentation.

## Index
1. Intro
2. Installation
3. Configuration
  1. Starting
  2. Basic Configuration
4. Troubleshooting

## Intro
BSPWM is a lightweight tiling window manager that can be great to practically anybody. It works by setting a certain amount of desktops (otherwise known as workspaces) and arranging windows in a tiled fashion for each one. The entire program is controlled mostly if not completely by keyboard shortcuts created by the user than run commands to change things. BSPWM by itself cannot do much, and requires sxhkd (or another keyboard shortcut manager) to be able to recieve user input and respond accordingly.

When a program is run, it is placed in a tree, splitting the current branch. (insert complicated tree logic here) Windows can have 4 states, tiled pseudo_tiled, floating and fullscreen.

_Tiled_ means the window's size will fill up the maximum area possible without overlapping other windows around it. It will stay in it's set location based on it's position in the window tree.

_Pseudo Tiled_ is the same as tiled except the window can be resized at will. The position stays the same though.

_Floating_ means the window can be placed anywhere on the desktop and resized at will.

_Fullscreen_ is pretty self explanatory.

Any window whose state has changed can be reverted back to tiled without modifying the tree layout

BSPWM is bare-bones, and only comes with pure window manager functionality. This isn't a bad thing though, it just means you have to configure everything else, which means everything can be the way you like it. You can install any bar like lemonbar, dzen2, or polybar. You can also control things like the background with cool things like scripts that change it based on your battery level. You can even run programs your way, with programs like rofi, dmenu, or even plank. However, all this configuration is no small task and it can take a while to get everything the way you want it, or even working at all.

## Installation

It is likely that there is a package for BSPWM for your distribution. In the case that there isn't, you can build from the source on any distribution. The instruction for this can be found in the repository here.

## Configuration

### Starting

BSPWM can be started by putting it in your xinitrc, but the easier method for beginners is to install a display manager and select BSPWM as a session. I recommend installing LightDM and rebooting. You will then be able to select BSPWM from a menu in the top right.

However, before you jump straight in to starting BSPWM, you should go through basic configuration to ensure you aren't greeted by a black screen with no input available.

### Basic Configuration

Without basic configuration, BSPWM will not be able to do anything other than show a black screen with a mouse cursor. The github repository has an example configuration to get you started with BSPWM. You can simply copy the file, but I recommend you copy it by hand. In my experience, I found it helped immensely with learning the keyboard shortcuts and understanding the workings of BSPWM. It's up to you though, both methods should work.

BSPWM is configured by a shell script that it runs when it starts. This script is located at `.config/bspwm/bspwmrc`. This script will start all your daemons and stuff like a status bar and compton, as well as your keyboard shortcut manager, sxhkd. It will also run different `bspc` commands to configure your bspwm session. The `bspc` command configures options such as the width of the border around windows, the gap inbetween the windows, etc. It's also the command that controls your bspwm session by focusing windows, changing desktops, and more.

You can go ahead and create a `bspwmrc` file and put the stuff you see in the example there. This file doesn't matter that much in this stage. All that's truly necessary is that it starts the keyboard shortcut daemon, sxhkd and creates the desktops.

Once you've done that, you can create an `sxhkdrc` file in `.config/sxhkd/`. This is the file that contains the keyboard shortcut configuration, and I highly recommend you copy it by hand. This way you can omit the stuff you don't think you need and add the rest of the stuff you think you do. It will also help you remember the shortcuts better, one of the hardest parts of getting started with a tiling window manager for the first time.


All right, once all this is done, you should be able to start a bspwm session and navigate a little bit. If there's something wrong, check the troubleshooting section. If all goes well, congratulations! You have your first functioning BSPWM setup! Now you can go deeper into the configuration and really rice your system with some information at the full documentation.
