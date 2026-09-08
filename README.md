<h1 align="center">

🐧

Mango Dotfiles

<img alt="Arch" src="https://img.shields.io/badge/Arch-0064b5?logo=arch-linux&logoColor=fff&style=for-the-badge" height="40"/><img alt="Linux" src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" height="40"/>

<br>

<img src="screen/1.png" alt="Preview" width="50%" max-width="800px"><img src="screen/2.png" alt="Preview" width="50%" max-width="800px">
<img src="screen/3.png" alt="Preview" width="50%" max-width="800px"><img src="screen/4.png" alt="Preview" width="50%" max-width="800px">

</h1>

### Astro Theme

<img alt="Linux" src="https://img.shields.io/badge/Linux-ffc425?style=for-the-badge&logo=linux&logoColor=black" height="24"/><img alt="Gentoo" src="https://img.shields.io/badge/Gentoo-6c5ce7?style=for-the-badge&logo=gentoo&logoColor=white" height="24"/><img alt="Debian" src="https://img.shields.io/badge/Debian-de324c?style=for-the-badge&logo=debian&logoColor=white" height="24"/><img alt="Suse" src="https://img.shields.io/badge/Suse-6ab04c?logo=opensuse&logoColor=fff&style=for-the-badge" height="24"/><img alt="Arch" src="https://img.shields.io/badge/Arch-0064b5?logo=arch-linux&logoColor=fff&style=for-the-badge" height="24"/><img alt="Alma" src="https://img.shields.io/badge/Alma-74b9ff?style=for-the-badge&logo=almalinux&logoColor=white" height="24"/>

| **Window Manager** <img width="60"/> | `mango` <img width="140"/> |
| :----------------------------------- | :------------------------ |
| **Status bar**                       | `waybar`                  |
| **Terminal**                         | `foot`                    |
| **Launcher**                         | `fuzzel`                  |
| **Wallpaper**                        | `swaybg`                  |
| **Compositor**                       | `wayland`                 |
| **Screenshot**                       | `grim`                    |
| **Viewer**                           | `imv`                     |
| **Logout menu**                      | `wlogout`                 |

#### Fonts / Theme

**Symbols Nerd Font** - icons, interface, development.  
**JetBrains Mono** - system font and interface.

**Clear Sans 10** - System Font  
**Osaka-Dark-Solarized** - Theme  
**Gruvbox** - Icons

### Installation

#### 1. Boot to the Arch iso

```
archinstall

on the step - profile - select > desktop > sway
```

#### 2. After installing - Reboot and update system

```
sudo pacman -Syu

sudo pacman -S \
      xorg-xwayland \
      seatd \
      polkit
```

> sudo systemctl enable --now seatd
> sudo usermod -aG seat $USER

#### 3. Installing Mango

```
sudo pacman -S --needed base-devel git
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si

paru -Syu \
mangowm-git \      
      waybar-git \
      swaybg \
      swaylock-effects-git \
      swaync \
      sway-audio-idle-inhibit-git \
      swayidle \
      wlogout \
      foot \
      xdg-desktop-portal-wlr \
      wl-clip-persist \
      cliphist \
      wl-clipboard \
      wlsunset \
      xfce-polkit \
      pamixer \
      wlr-dpms \
      dimland-git \
      brightnessctl \
      swayosd \
      wlr-randr \
      grim \
      slurp
```

#### 4. Installing Pkgs

```
paru -S \

alacritty \
   foot \
   micro \
   mousepad \
   firefox

thunar \
   thunar-archive-plugin \
   thunar-volman \
   xfce4-screenshooter

fastfetch \
   mc \
   xarchiver \
   tumbler \
   btop

p7zip \
   unzip \
   zip \
   tar \
   atool

wget \
   git \
   curl \
   gvfs \
   udisks2 \
   ntfs-3g

xdg-utils \
   ripgrep \
   zoxide \
   eza \
   fzf \
   fd

imv \
   celluloid \
   rhythmbox \
   imagemagick \
   ffmpeg
```

#### 5. Installing FISH

```
paru -S fish 

chsh -s $(command -v fish)
```

#### Home Structure

```text
~/
├── Pictures/
├── Screen/
├── icons/
├── themes/
├── .local/share/fonts/
└── .config/
    ├── mango/
    ├── waybar/
    ├── fuzzel/
    └── foot/
```

#### Used Dots, Icons, Themes, Wallpapers

> [yojeero/config_linux](https://github.com/yojeero/config_linux)

#### Folder for screenshots

> Create folder **Screen** for saving screenshots via grim.

### Login TTY

> ### Mango > use Bash or ZSH or FISH

#### .bash_profile

```
if [[ -z $DISPLAY && $XDG_VTNR -eq 1 ]]; then
  exec mango
fi
```

#### .zprofile

```
if [ -z "${DISPLAY}" ] && [ "${XDG_VTNR}" -eq 1 ]; then
  exec mango
fi
```

#### config.fish

```
if status is-login
    if test (tty) = /dev/tty1

         set -gx XDG_CURRENT_DESKTOP mango
            set -gx XDG_SESSION_DESKTOP mango
            set -gx XDG_SESSION_TYPE wayland
            set -gx MOZ_ENABLE_WAYLAND 1
            set -gx QT_QPA_PLATFORM wayland
            
            exec mango
    end
end
```

#### Login to Mango

> Arch Linux > login > pass


> ### Mango + Sway 

#### config.fish

> Interactive session selection when logging into TTY1

```
if status is-interactive; and test (tty) = "/dev/tty1"
    echo "==================================="
    echo " Run Mango or Sway:   "
    echo " [1] Mango (Wayland)              "
    echo " [2] Sway (Wayland)              "
    echo " [3] Stay in TTY      "
    echo "==================================="
    
    # Read the user's choice
    read -P "Select [1-3]: " choice

    switch $choice
        case 1
            echo "Start Mango (Wayland)..."    
            set -gx XDG_CURRENT_DESKTOP mango
            set -gx XDG_SESSION_DESKTOP mango
            set -gx XDG_SESSION_TYPE wayland
            set -gx MOZ_ENABLE_WAYLAND 1
            set -gx QT_QPA_PLATFORM wayland
            
            exec mango

        case 2
            echo "Start Sway (Wayland)..."
            set -gx XDG_CURRENT_DESKTOP sway
            set -gx XDG_SESSION_DESKTOP sway
            set -gx XDG_SESSION_TYPE wayland
            set -gx MOZ_ENABLE_WAYLAND 1
            set -gx QT_QPA_PLATFORM wayland
            
            exec sway

        case 3
            echo "Enter to TTY!"
            
        case '*'
            echo "Bad step. Stay in TTY."
    end
end
```

#### Login to Mango or Sway

    ├── [1] Mango (Wayland)
    ├── [2] Sway (Wayland)
    └── [3] Stay in TTY
