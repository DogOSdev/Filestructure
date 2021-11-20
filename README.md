# DogOS Filesystem

The filesystem will have 2 main drives: `0` and `1`

The `0` drive will hold critical files needed by the system, like user information and system files.

The `1` drive will hold all the main files, this is the directory that the user will be able to access.

## Drive `0`
Drive `0` has the following system files:
- `system.ini` : System Information and Config
- `users.ini` : User Information

These files will be explained below...

### `system.ini`
`system.ini` holds critical system information like paths, roles, versions, etc. Without it, we wouldn't be able to find stuff.

Here is a example file:
```ini
[SYSTEM]
OS=DOGOS_DEBUG|DEBUG|0.0.1
PATH=1:/dogos
TEMP=1:/dogos/temp
TMP=1:/dogos/temp
DIR=1:/dogos
INSETUP=0
ROLES=SYSTEM-0:ROOT-1:ADMIN-2:USER-3:GUEST-4
```

- `OS` - Operating System Name and Version
- `PATH` - System Path's
- `TEMP`:`TMP` - System Temporary Variables
- `DIR` - DogOS Directory
- `INSETUP` - Is the Operating System inside setup?
- `ROLES` - System Roles

### `users.ini`
`users.ini` holds user information needed for system processes, root access, and users on the system.

Here is a example file:
```ini
[:USERS]
SYSTEM=
ROOT=
USEREXAMPLE=5f4dcc3b5aa765d61d8327deb882cf99

[SYSTEM]
USERNAME=SYSTEM
ROLE=0:1:2:3

[ROOT]
USERNAME=root
ROLE=1:2:3

[USEREXAMPLE]
USERNAME=UserExample
ROLE=3
```

Note how `ROLES` only use the roles id from `system.ini`. This is so if a role gets renamed for some reason, it does not need to be updated here.

- `:USERS`
    - The `:USERS` key follows a key value pair.
    - Keys are the username in all caps
    - Values are passwords, hashed and salted with SHA-256. This is for user security.
    - There are two users already made that are needed to run the system
        - SYSTEM
        - ROOT
- Username Keys
    - Username keys are just extra information about the user.
        - `USERNAME` : Case Sensitive username, mostly for displaying purposes.
        - `ROLE`: The user's role, saved as a role id.

## Drive `1`
Drive `1` holds other system files like user directories, applications, config files, etc. This could be compared to the Windows `C` drive.

### `config`
Holds config files for applications globally. This could be compared to the Unix `etc` folder.

### `dogos`
Holds system files, apps, and other information about the Operating System. This could be compared to the `Windows` folder.

### `home`
This holds user's files. This could be compared to the Unix `home` folder or the Window's `Users` folder. View the `1/home` folder to check out how that directory tree is formed.

## Final Thoughts
That's the planned filesystem for DogOS. Any improvements are welcome, just make a fork and pull request.