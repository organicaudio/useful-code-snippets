# not enough files watchers

Jetbrains and VS Code complain about problems with the file watchers on Deepin. [Info from jetbrains](https://confluence.jetbrains.com/display/IDEADEV/Inotify+Watches+Limit)

To solve this issue do:

```shell
sudo nano /etc/sysctl.conf
# and add: fs.inotify.max_user_watches = 524288

# to load it afterwards.
sudo sysctl -p --system
```