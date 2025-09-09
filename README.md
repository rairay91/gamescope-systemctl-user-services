# auto run any software in the background in gamescope-steam-game-mode/gamescope-session
This is a short yet full guide about how to run any software in the background as soon as gamescope steam session start

I have tested thhis on CachyOS Handheld edition, Nobara Deck/HTPC edition, Bazzite Deck/HTPC edition, which covers almost every deck/htpc distro.

-> First install sunshine/heroic-games-launcher and configure it and test it if it is working from desktop mode.

-> If it is working in desktop mode switch back to steam game mode and press Ctrl+Alt+F3 or Ctrl+Alt+F2 or Ctrl+Alt+F1 on keyboard to enter tty3 or tty2 or tty1 terminal and login with your username and password. And type command in this file on your terminal https://github.com/rairay91/gamescope-systemctl-user-services/blob/main/whoami.txt

-> It should give output something like this(notice Desktop=gamescope)
Id=1
Desktop=gamescope
Type=wayland

Id=2
Desktop=
Type=unspecified


-> Now switch back to desktop mode open this directory in any file manager "/home/(user)/.config/systemd/user/" where (user) is your username, if systemd/user does not exist create it first.

-> Download any .service file from this repo and copy .service file in directory mentioned above.

-> Now open terminal in the same directory where you copied/created service file and type these commands(without double qoute) and press enter.

A. To enable sunshine system package
"systemctl --user enable sunshine-system-gamescope.service"

B. To enable sunshine flatpak
"systemctl --user enable sunshine-flatpak-gamescope.service"

C. To enable Heroic Games Launcher system package
"systemctl --user enable hgl-system-gamescope.service"

D. To enable Heroic Games Launcher flatpak
"systemctl --user enable hgl-flatpak-gamescope.service"

-> Now reboot and as soon as gamescope-session launch service file will be triggered automatically in the background.

-> If you want to disable any of these service then go to the desktop mode, open the same directory where you copied/created .service file and type this command "systemctl --user disable sunshine-system-gamescope.service" simply replace the service file name with whichever service you want to disable.
