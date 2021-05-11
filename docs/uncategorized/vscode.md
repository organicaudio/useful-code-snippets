# VS Code

## Remote SSH and SCP

[Official documentation](https://code.visualstudio.com/docs/remote/ssh)

- Install 'Remote - SSH' Extension
- Open config via the gear symbol which appears next to the 'ssh targets' batch when your mouse hovers over it over
- Edit this configureation text file
- Connect to it. First time vscode might  prompt two times for your password. (Once for the ssh login and once for the start of the vs code server)

Use vscode as usual. **Open Folder** and the **integrated terminal** will connect to the remote server not your local one.

One for each connection:
```
Host alias
    HostName hostname
    User user
    IdentityFile privateKey
```

trouble shooting:

- you can restart the vs code server on the remote server with prompt `> Remote-SSH: Kill VS Code SErver on Host...` (CTRL + SHIFT+P). This might be necessary if you add a user to a new group.