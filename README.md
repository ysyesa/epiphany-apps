# epiphany-apps
This is a collection of web applications, "packaged" in a more-friendly and nicer way, which can be launched from GNOME desktop, thanks to [Epiphany](https://wiki.gnome.org/Apps/Web). `Epiphany` needs to be installed at the first place.

# How to run?
1. Add the application into `config.yaml` and put the required icon in `icons` directory.
2. Run `./x-build` to generate the desktop entries and icons of various sizes.
3. Run `./x-install` to copy the desktop entries and the icons to `/usr/share/applications` and `/usr/share/icons` respectively.

# Epiphany Issue with StartupWMClass
Not really an issue though, just a bit more towards perfection.

After the application is installed, yes it will appear on the desktop application lists, also with the correct name and icon. However, when the application is opened, the name and the icon displayed in the Task Switcher (`Alt + Tab`) is wrong. Based on what I know, this is because there is no relation specified between the window shown and the application.

To fix that, we need to map the application to the window by specifying the `StartupWMClass` in the desktop entry to the WM Class of the window. How to find out the WM Class?

In X server, run `xprop`, navigate to the window, and click. This will list all the properties of the window, including `WM_CLASS`.

In Wayland, click `Alt + F2`, type `lg`, and then go to tab `Windows`. This will show all the windows opened, together with the WM Class.

Put the value WM Class value in the `StartupWMClass` field in the desktop entry and run `sudo update-desktop-database` to update.

This issue happens because we are unable to pre-determine the WM Class in Epiphany application. The WM Class is generated randomly.
