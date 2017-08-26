# The BSPWM Getting Started guide

In this guide I will walk you through installing BSPWM and configuring the basics to have a functional system. A more in depth documentation of BSPWM will be available at the full documentation.

## Index
1. Intro
2. Installation
3. Configuration
	1. Starting
	2. Basic Configuration
	3. Advanced Configuration
4. Conclusion

## Intro
BSPWM is a lightweight tiling window manager that can be great to practically anybody. It works by setting a certain amount of desktops (otherwise known as workspaces) and arranging windows in a tiled fashion for each one. The entire program is controlled mostly if not completely by keyboard shortcuts created by the user than run commands to change things. BSPWM by itself cannot do much, and requires sxhkd (or another keyboard shortcut manager) to be able to recieve user input and respond accordingly.

When a program is run, it is placed in a tree, splitting the current branch. (insert complicated tree logic here) Windows can have 4 states, tiled pseudo_tiled, floating and fullscreen.

- _Tiled_ means the window's size will fill up the maximum area possible without overlapping other windows around it. It will stay in it's set location based on it's position in the window tree.

- _Pseudo Tiled_ is the same as tiled except the window can be resized at will. The position stays the same though.

- _Floating_ means the window can be placed anywhere on the desktop and resized at will.

- _Fullscreen_ is pretty self explanatory.

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

### Advanced Configuration

#### Panel

There are plenty of options for panels, and they're all different and good, it's just a matter of picking the one that's right for you. Some of the most common ones are lemonbar, polybar, i3bar, tint2, dzen2, and so on.

The configuration for each bar will vary, so you'll have to check the documentation for the specific panel on how to customize it. To start it thouhgh, it's as simple as adding `panel &` to your `bspwmrc`, where `panel` is the executable of the panel (for example `polybar`).

Polybar is a very common choice among rices these days, due to it's straightforward configuration and host of features. Tint2 is another popular, actively developed panel. Dzen2 is old (hasn't been updated in 4 years) but still works fine for some and has the advantage of maturity. In the end, it's up to you.

#### Notifications

You'll want to be able to recieve notifications in your environment, and there's plenty of ways to accomplish that. Like the panel and many other bspwm ideals, you can pick whatever third party program you like and set it up based on it's documentation. Dunst is probably the most common with bspwm, due to the fact that it's not built on a DE by default. Again, you can start it by putting `dunst &` in your `bspwmrc`, and change `dunst` to whatever notification daemon you like.

#### Wallpaper

You might be surprised to find that there's no obvious way to set a wallpaper without a DE with built-in functionality to do so. Fortunately it's simple to set it yourself with a program called `feh`. `feh` is a general purpose command line image viewer that can set your wallpaper as an added bonus. To set your wallpaper, add `feh --bg-scale <path-to-wallpaper>` to your bspwmrc.

#### Program Launcher

I almost forgot about this one! You need a way to start programs in your new `bspwm` environment. To do this, there are many launchers that fit the criteria. I like `rofi`, and another good alternative is `dmenu` the default for i3. Again, there's many more launchers I know nothing about, and you can find them on the internet. Once you pick one, you need to add it to your `sxhkdrc`. More on this in the next section.

#### Keybinds

I've been dreading writing this section as there isn't really a good way to put it in a concise easy-to-understand way. I'll do my best though.

`sxhkd` is a hotkey daemon. It listens for key presses and when it recieves a configured one, it executes whatever command you set for that keycombo. The configuration file is `~/.config/sxhkd/sxhkdrc`, which you should've seen in the beginning of this guide.

The format for an `sxhkdrc` file is as follows:

	keybind
		command to execute

with one of these entries for each keybind you want. This is likely the most time consuming part of the setup if you do it yourself. I highly recommend you do type this entire configuration by hand however, as it will do wonders for you being able to navigate your window manager efficiently. Example configurations can be found in the `baskerville/bspwm` repository.

For navigating the window manager with these sxhkd, you need to run many different `bspc` commands. `bspc` takes arguments and passes them on to `bspwm`, which then executes the actions. These actions can be things such as close node, focus parent node, view workspace 1, etc. There's too much to list here, so the specifics of this will be in the full documentation.

The same logic applies to program launcher integration with sxhkd. Simply bind a keybind to the command to execute your program launcher. Traditionally, the keybind for this is mod + space, though it can be whatever you want.

### Conclusion

Congratulations on making it to the end of the getting started guide. You may not have a fully functioning environment yet, but that's ok. Configuring a window manager is no small task, and I usually like to do it incrementally. This guide is meant to be an overview on how all the things that make up an environment work together and each component necessary.