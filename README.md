# Fedora Silverblue Post-Installation

These are my Fedora Silverblue post-installation steps for my use case.

## 1. System Upgrade

You can update the system through GNOME Software or using the following command:

```bash
rpm-ostree upgrade
```

## 2. Enable Flathub

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

## 3. Installing Extension

These are my favorite extensions:

- [Alphabetical App Grid](https://github.com/stuarthayhurst/alphabetical-grid-extension)

- [Battery Health Charging](https://github.com/maniacx/Battery-Health-Charging)

- [Caffeine](https://github.com/eonpatapon/gnome-shell-extension-caffeine)

- [Hot Edge](https://github.com/jdoda/hotedge)

When using the Hot Edge extension I like to disable the Hot Corner in Multitasking inside Settings.


