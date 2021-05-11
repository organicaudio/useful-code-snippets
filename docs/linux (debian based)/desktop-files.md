# Application Interface

## create .desktop files

``.desktop`` files put applications in the desktop menu. The files are placed in ``/usr/share/applications`` and ``~/.local/share/applications``. 

If the path to executable contains spaces it needs to be put in double quotes. Single quotes do not work.

A nice tool to edit and create such files is [MenuLibre](https://wiki.ubuntuusers.de/MenuLibre/):

Install via `sudo apt-get install menulibre ` afterwards just launch it from command line `menulibre` and create e new entry for menulibre itself so it will appear in Applauncher.

## default application

The MimeType field in the .desktop file tells the os which files the application can handle. The default application for a MimeType are configured in ~/.config/mimeapps.list

## vs code issue (super+e)

Vs code opens when you press super+e instead of the file browser. To resolve the issue add `inode/directory = dde-file-manager.desktop;code.desktop;` to ~/.config/mimeapps.list.
