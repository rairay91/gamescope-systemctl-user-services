# auto run any software in the background in gamescope-steam-game-mode/gamescope-session
This is a short yet full guide about how to run any software in the background as soon as gamescope steam session start

Note: This method should work with cachyos-hendheld, nobara-handheld or any other non-immutable handheld edition distro, for immutable distro might work if systemd can use per user services(which is possible, because this method create systemd service in users home directory). And this method somehow also launch sunshine in the background even when you go to the desktop mode(which is possible, because systemd is handling this task rather then desktop environment, which is a plus point).

Note: For sunshine flatpak version some commands may very

Note: If you want to disable it for some reason, simply type this command in terminal and hit enter "systemctl --user enable sunshine-gamemode.service" command may very as per your choice.




-> First install sunshine and configure it and test it if it is working from desktop mode.




-> If it is working in desktop mode switch back to steam game mode and press Ctrl+Alt+F3 or Ctrl+Alt+F2 or Ctrl+Alt+F1 on keyboard to enter tty3 or tty2 or tty1 terminal and login with your username and password(Note: you can also do following inside desktop session, but going to steam game mode is recommanded)




-> now type this command(without double qoutation mark) in the terminal and press enter where (user) is your user name "loginctl show-session $(loginctl | grep $(whoami) | awk '{print $1}') -p Type -p Desktop -p Id" It should show gamescope in this line "Desktop=gamescope", whatever it shows is your session.




-> now switch back to desktop mode open this directory in any file manager "/home/(user)/.config/systemd/user/" where (user) is your username




-> create a file here with the name "sunshine-gamescope.service" or you can choose any name instead of "sunshine-gamescope"




-> now inside this file type this content
Note: In ExecStart sunshine need to be replaced with proper run command if sunshine is install from flatpak

A. if sunshine is a system package for bazzite, fedora atomic, nobara deck/htpc, cachyos-handheld edition user

[Unit]
Description=Sunshine only in Game Mode
After=graphical-session.target

[Service]
Type=simple
ExecStart=/bin/bash -c 'sunshine'
Restart=on-failure
ExecCondition=/bin/bash -c '[ "$XDG_SESSION_DESKTOP" = "gamescope" ]'

[Install]
WantedBy=graphical-session.target

B. If sunshine is flatpak for SteamOS, Chimera-OS user

[Unit]
Description=Sunshine only in Game Mode
After=graphical-session.target

[Service]
Type=simple
ExecStart=usr/bin/flatpak run dev.lizardbyte.app.Sunshine
Restart=on-failure
ExecCondition=/bin/bash -c '[ "$XDG_SESSION_DESKTOP" = "gamescope" ]'

[Install]
WantedBy=graphical-session.target




-> now open terminal in the same directory where you copied/created service file and type these commands and press enter
Note: in "systemctl --user enable sunshine-gamescope.service" use the name you used while creating service file file

systemctl --user enable sunshine-gamescope.service




-> Now reboot and as soon as gamescope-session launch sunshine will run in the background




-> If you want heroic game launcher to auto launch in the background and keep running in the background even if you close it, create "hgl-gamescope.service" and paste this content in this file

Note: Make sure to enable minimize on close option from heroic game launcher settings

[Unit]
Description=Launch Heroic Game Launcher only in Game Mode
After=graphical-session.target

[Service]
Type=simple
ExecStart=/usr/bin/flatpak run com.heroicgameslauncher.hgl
Restart=on-failure
ExecCondition=/bin/bash -c '[ "$XDG_SESSION_DESKTOP" = "gamescope" ]'

[Install]
WantedBy=graphical-session.target




-> Open the terminal in the same directory where you created this file run this command "systemctl --user enable hgl-gamescope.service" and reboot.



-> If you want to disable/turn off this(disable auto launching) then go to the desktop mode, open the same directory where you copied/created .service file and type this command "systemctl --user disable sunshine-gamescope.service" simply replace the service file name with what you setup or whichever service you want to disable.
