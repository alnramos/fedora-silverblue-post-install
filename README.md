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

## 4. Layer System Packages

```
rpm-ostree install gnome-tweaks libvirt-client virt-manager
```

## 5. Installing a Password Manager and a 2FA Authenticator Application

I like to use [Proton Pass](https://proton.me/pass) as Password Manager and [Ente](https://ente.com/auth/) as 2FA Authenticator.

You can install Proton Pass as a Flatpak or install it inside a toolbox. I prefer using it inside a toolbox and create the .desktop shortcut. Here are the steps:

```bash
toolbox create -c proton-pass-box
toolbox enter proton-pass-box
sudo dnf update && sudo dnf install -y webkit2gtk4.1
```

You can verify if the Proton Pass is working inside the toolbox through the following command:

```bash
proton-pass
```

And to create the .desktop shortcut:

```bash
cd ~/.local/share/applications
touch proton-pass.desktop
vi proton-pass.desktop
```

```
[Desktop Entry]
Type=Application
Name=Proton Pass
Exec=toolbox run -c proton-pass-box proton-pass %f
Icon=/path/to/proton-pass-icon.svg
Terminal=false
Categories=Utility;
```

```bash
update-desktop-database ~/.local/share/applications
```

## 6. Installing Anki

You can also use [Anki](https://apps.ankiweb.net/) inside a toolbox.

```bash
toolbox create -c anki-box
toolbox enter anki-box
sudo dnf install -y zstd qt6-qtwayland libXcomposite libXcursor libXi libXtst libXrandr libxcrypt-compat xdg-utils libatomic libxkbfile mpv
```
```
cd ~/.local/share/applications
touch anki.desktop
vi anki.desktop
```

```                      
[Desktop Entry]
Type=Application
Name=Anki
Exec=toolbox run -c anki-box anki %f
Icon=/path/to/anki-icon.svg
Terminal=false
Categories=Utility;
```

```bash
update-desktop-database ~/.local/share/applications
```

## References

[Fedora Atomic Desktops User Guide](https://docs.fedoraproject.org/en-US/atomic-desktops/)
