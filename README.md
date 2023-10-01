# TCET Linux Set Once

TCET Linux Set Once is a package in the [*tcet-linux-repo*](https://github.com/tcet-opensource/tcet-linux-repo) which is used to set certain configurations in [*TCET Linux*](https://github.com/tcet-opensource/tcet-linux).


## Working 

When the package is installed it will copy the [*set_once_xfce4.desktop*](https://github.com/tcet-opensource/tcet-linux-set-once/blob/main/etc/skel/.config/autostart/set_once_xfce4.desktop) to the ~/.config/autostart folder which will execute the  [*set_once_xfce4.sh*](https://github.com/tcet-opensource/tcet-linux-set-once/blob/main/etc/skel/set_once_xfce4.sh)


**set_once_xfce4.sh**
```bash
#!/bin/sh

# For xed line count
dbus-launch dconf load / < ~/xed.dconf

# For setting calamares.desktop as trusted
for f in ~/Desktop/calamares.desktop; do chmod +x "$f"; gio set -t string "$f" metadata::xfce-exe-checksum "$(sha256sum "$f" | awk '{print $1}')"; done

# Removing script and set_once_xfce4.desktop
rm ~/xed.dconf ~/.config/autostart/set_once_xfce4.desktop ~/set_once_xfce4.sh 
```

## Credits

We would like to give our sincere thanks to the [*EOS Project*](https://github.com/endeavouros-team) . This package was inspired by a package similar to one made by Endeavour OS.