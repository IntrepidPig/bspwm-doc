# BSPWM Configuration

## How BSPWM configuration works

BSPWM is configured by a shell script located at `~/.config/bspwm/bspwmrc`. This shell script runs any commands you need to configure your system the way you want. It configures BSPWM by running the bspc command to set options. The rest of yur system is controlled by external applications like sxkhd and lemonbar to add BSPWM funcionality. `bspwmrc` will start all these programs, but they will each have their own configuration file.

An instance of BSPWM organizes all the windows in a hierarchal fashion, with each domain containing smaller domains. The biggest domain is a monitor. Each monitor has desktops, (also known as workspaces). Finally, each desktop has nodes, (also know as windows).

---

### `bspc` Documentation

`bspc` is used by either targeting a component or changing global settings.

To modify settings, the command syntax is as follows:

`bspc config [selector] <setting> [<value>]`

The selector can be used to modify settings for a certain domain. The syntax for the selector is `-m MONITOR`, `-d DESKTOP`, or `-n NODE`. The domain can be targeted by using a keyword or it's ID.

A list of ID's can be retrieved with the command `bspc query <-M:-D:-N>`
The keywords availible for selection are:

- focused: selects the focused domain
- pointed: selects the node with the mouse pointer over it
- others

Desktops can be selected with the name of the desktop provided in `bspwmrc`, and monitors can be selected with the name of the output.

If no selector is provided, the setting will change globally.
If no value is provided, the currently set value will be outputted to the stdout. This is good for incrementing or decrementing settings.

---

### Navigation with `bspc`

Another way of using the `bspc` command is changing the state of domains and navigating the desktop this way.