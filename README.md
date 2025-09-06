# auto run any software in the background in gamescope-steam-game-mode/gamescope-session
This is a short yet full guide about how to run any software in the background as soon as gamescope steam session start

I have tested thhis on CachyOS Handheld edition, Nobara Deck/HTPC edition, Bazzite Deck/HTPC edition, which covers almost every deck/htpc distro.

Note: This method should work with cachyos-hendheld, nobara-handheld or any other non-immutable handheld edition distro, for immutable distro might work if systemd can use per user services(which is possible, because this method create systemd service in users home directory). And this method somehow also launch sunshine in the background even when you go to the desktop mode(which is possible, because systemd is handling this task rather then desktop environment, which is a plus point).

-> First install sunshine and configure it and test it if it is working from desktop mode.

-> If it is working in desktop mode switch back to steam game mode and press Ctrl+Alt+F3 or Ctrl+Alt+F2 or Ctrl+Alt+F1 on keyboard to enter tty3 or tty2 or tty1 terminal and login with your username and password(Note: you can also do following inside desktop session, but going to steam game mode is recommanded). Now type this command(without double qoutation mark) in the terminal and press enter where (user) is your user name "loginctl show-session $(loginctl | grep $(whoami) | awk '{print $1}') -p Type -p Desktop -p Id" It should show gamescope in this line "Desktop=gamescope".

-> Now switch back to desktop mode open this directory in any file manager "/home/(user)/.config/systemd/user/" where (user) is your username, if systemd/user does not exist create it first.

-> Now open terminal in the same directory where you copied/created service file and type these commands and press enter
Note: in "systemctl --user enable sunshine-gamescope.service" use the name you used while creating service file file

A. To enable sunshine system package
systemctl --user enable sunshine-system-gamescope.service

B. To enable sunshine flatpak
systemctl --user enable sunshine-flatpak-gamescope.service

C. To enable Heroic Games Launcher system package
systemctl --user enable hgl-system-gamescope.service

D. To enable Heroic Games Launcher flatpak
systemctl --user enable hgl-flatpak-gamescope.service

-> Now reboot and as soon as gamescope-session launch sunshine will run in the background

-> If you want to disable any of these service then go to the desktop mode, open the same directory where you copied/created .service file and type this command "systemctl --user disable sunshine-system-gamescope.service" simply replace the service file name whichever service you want to disable.
