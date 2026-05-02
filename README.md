# Fedora Silverblue Post-Installation

These are my personal Fedora Silverblue post-installation steps tailored for my use case.

## 1. System Upgrade

You can update the system through GNOME Software or using the following command:

```bash
rpm-ostree upgrade
```

## 2. Change Hostname

```bash
sudo hostnamectl set-hostname <new-name>
```

## 3. Enable Flathub

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

## 4. Installing Extension

These are my favorite extensions:

- [Alphabetical App Grid](https://github.com/stuarthayhurst/alphabetical-grid-extension)

- [Battery Health Charging](https://github.com/maniacx/Battery-Health-Charging)

- [Caffeine](https://github.com/eonpatapon/gnome-shell-extension-caffeine)

- [Hot Edge](https://github.com/jdoda/hotedge)

- **Note:** When using the Hot Edge extension, I recommend disabling the Hot Corner in the Multitasking section of GNOME Settings.

## 5. Layer System Packages

```
rpm-ostree install gnome-tweaks libvirt-client virt-manager
```

## 6. Installing a Password Manager and a 2FA Authenticator Application

I like to use [Proton Pass](https://proton.me/pass) as my password manager and [Ente](https://ente.com/auth/) as my 2FA Authenticator.

While you can install Proton Pass as a Flatpak, I prefer using it inside a toolbox and creating a .desktop shortcut.


**Setting up the Proton Pass Toolbox**

```bash
toolbox create -c proton-pass-box
toolbox enter proton-pass-box
sudo dnf update && sudo dnf install -y webkit2gtk4.1
```

You can verify if Proton Pass is working inside the toolbox with the following command:

```bash
proton-pass
```

**Creating the Desktop Shortcut**

```bash
cd ~/.local/share/applications
touch proton-pass.desktop
vi proton-pass.desktop
```

Add the following configuration:

```
[Desktop Entry]
Type=Application
Name=Proton Pass
Exec=toolbox run -c proton-pass-box proton-pass %f
Icon=/path/to/proton-pass-icon.svg
Terminal=false
Categories=Utility;
```

Update the application database:

```bash
update-desktop-database ~/.local/share/applications
```

## 7. Installing Anki

You can also use [Anki](https://apps.ankiweb.net/) inside a toolbox.

**Setting up the Anki Toolbox**

```bash
toolbox create -c anki-box
toolbox enter anki-box
sudo dnf install -y zstd qt6-qtwayland libXcomposite libXcursor libXi libXtst libXrandr libxcrypt-compat xdg-utils libatomic libxkbfile mpv
```

**Creating the Desktop Shortcut**

```
cd ~/.local/share/applications
touch anki.desktop
vi anki.desktop
```

Add the following configuration:

```                      
[Desktop Entry]
Type=Application
Name=Anki
Exec=toolbox run -c anki-box anki %f
Icon=/path/to/anki-icon.svg
Terminal=false
Categories=Utility;
```

Update the application database:

```bash
update-desktop-database ~/.local/share/applications
```

## (Optional) Toolbox DNF Configuration (Fastest Mirrors and Max Parallel Downloads)

Open the DNF configuration file:

```bash
sudo nano /etc/dnf/dnf.conf
```

Add or modify the following lines:

```bash
fastestmirror=True
max_parallel_downloads=10
```

```bash
sudo dnf update --refresh
```

## 8. .NET Development Toolbox

Set up an isolated environment for .NET development:

```bash
toolbox create -c dotnet-dev
toolbox enter dotnet-dev
sudo dnf install -y dotnet-sdk-10.0 aspnetcore-runtime-10.0 dotnet-runtime-10.0
```

**Optional:** Fedora Rawhide Toolbox If you want to use a toolbox with Fedora Rawhide:

```bash
toolbox create -c dotnet-rawhide --image registry.fedoraproject.org/fedora-toolbox:rawhide
toolbox enter dotnet-rawhide
```

## 9. Hiding the default browser (Firefox)

As mentioned in the Docs:

```bash
sudo mkdir -p /usr/local/share/applications
sudo cp /usr/share/applications/org.mozilla.firefox.desktop /usr/local/share/applications/
sudo sed -i "2a\\NotShowIn=GNOME;KDE" /usr/local/share/applications/org.mozilla.firefox.desktop
sudo update-desktop-database /usr/local/share/applications/
```

```bash
flatpak install flathub org.mozilla.firefox
```

## 10. Install 7zip to Encrypt Backup Files

Once a week, I like to compress and encrypt my backup files to store in the cloud.

```bash
sudo dnf install p7zip p7zip-plugins
7z a -tzip -p -mem=AES256 backup.zip backup/
```

## References

[Fedora Atomic Desktops User Guide](https://docs.fedoraproject.org/en-US/atomic-desktops/)
