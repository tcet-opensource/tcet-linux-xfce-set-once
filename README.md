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

**xed.dconf**
```bash
[org/x/editor/preferences/editor]
bracket-matching=false
display-line-numbers=true
prefer-dark-theme=true
scheme='cobalt'
wrap-mode='none'
```

- This script when executed will load the xed text editor's configuration from [*xed.dconf*](https://github.com/tcet-opensource/tcet-linux-set-once/blob/main/etc/skel/xed.dconf) . These configurations include things like line count , theme , etc.

- It will mark *calamares.desktop* as a trusted file by adding its sha256sum to the *calamares.desktop's* metadata.

- And finally it will remove the xed.dconf , set_once_xfce4.sh and set_once_xfce4.desktop from their respective locations.

## Credits

We would like to give our sincere thanks to the [*EOS Project*](https://github.com/endeavouros-team) . This package was inspired by a package similar to one made by Endeavour OS.