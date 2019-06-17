# SERVICES MANAGEMENT

## INIT/RC

- Legacy UNIX startup system
- Located in /etc/init.d and /etc/rc.d
- Controlled (start/stop/restart) via 'service' command line utility 
- Configuration tools ...
    - rcconf
    - Service Configuration Tool

## SYSTEM DAEMON

- Replacement for init 
- Located in /etc/systemd
- Controlled via 'sysctl' command line utility
- Configuration tools ...
    - KDE system config
    - systemadm
    - systemd-manager

# IMPROVE BATTERY LIFETIME

- tlp (tlp-stat): power management tool
- powertop: tooll to monitor battery usage
- indicator-cpufreq: CPU frequency monitor allowing setting power mode
- Diable bluetooth
- Reduce screen luminosity as much as possible

# DEBUG BOOT TIME

- Check high level information about boot time
    > systemd-analyze
- Dig into the longest boot step
    > systemd-analyze critical-chain
- Check boot logs: /var/log/syslog & /var/log/boot.log

# TWEAK INPUT SETTINGS (synclient)

- Create a new file in usr/share/X11/xorg.conf.d/ with an number greater than 50 e.g. 51-touchpad-config.conf
- Enter your settings ...
    Section "InputClass"
        Identifier "desensitize horizontal scrolling so it doesn't trigger when vertically scrolling."
        MatchIsTouchpad "on"
        Option "HorizScrollDelta" "650"
    EndSection

# INVESTIGATE RESOURCES USAGE

- 'top' command displays current processes resource usage

# CHANGE DEFAULT PROGRAM

sudo update-alternatives --config c++

# PACKAGE MANAGEMENT

- Update linux ubuntu packages
    > sudo apt-get update
    > sudo apt-get full-upgrade
