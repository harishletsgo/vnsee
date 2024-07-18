# Setup as a Second Screen on Linux with Sway

## Create a Headless Output

First up we’ll create a _headless_ output, i.e. a space to run applications that’s not visible on any of your screens and that can be made accessible over a VNC connection.
Run `swaymsg create_output` in a terminal to create a new output called `HEADLESS-1`.
This output will need to be recreated each time you start Sway, so you might want to add the command in your session startup script.

## Setup the Output

Set the size of the new output to exactly 1404x1872 and place it where you’d like relative to your other (real) screens.
This can be done interactively with [wdisplays](https://github.com/cyclopsian/wdisplays) or using the [command line](https://man.archlinux.org/man/sway-output.5).
You can make the output configuration permanent by editing your Sway config file (located in `~/.config/sway/config`).

## Start the VNC Server

Any Wayland-compatible VNC server can be used for this task.
We recommend [wayvnc](https://github.com/any1/wayvnc) which you can start with the following command line:

```console
$ wayvnc --output=HEADLESS-1 --max-fps=10 10.11.99.2 5900
```

It may happen that your computer isn’t assigned the 10.11.99.2 IP by the reMarkable DHCP server. In this case, replace this IP with the one that’s been assigned.

## Start VNSee

If you installed VNSee through [Toltec](https://toltec-dev.org) and you’re using a launcher such as [Oxide](https://github.com/Eeems/oxide) or [remux](https://github.com/rmkit-dev/rmkit/tree/master/src/remux) (which is the recommended setup), VNSee should show up in the list of available apps on the tablet.
Starting the VNSee app will bring up a screen listing the available VNC servers, in which you should see a server listening on `10.11.99.2:5900`.
Tap on that server and you should see your computer’s screen appear on the reMarkable after a few seconds.

Otherwise, you can also start VNSee manually through SSH. Don’t forget to stop the main UI app first (`systemctl stop xochitl`) and start it again afterwards (`systemctl start xochitl`).
