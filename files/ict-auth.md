# 登录网络

```
(base) hs@2024rt4230:~/disk1$ ict_auth login
[INFO] Preparing the runtime...
[INFO] Starting login process...
=============================
ICT Username: sunwenhao2024
ICT Password: 
=============================
[INFO] Login succeeded.
[INFO] Username: sunwenhao2024
[INFO] Used flow: 153.67 GB
[INFO] Used time: 572小时28分56秒
```

# 退出登录

```
(base) hs@2024rt4230:~/disk1$ ict_auth logout 
[INFO] Preparing the runtime...
[INFO] Logout succeeded
```

# 使用选项

```
(base) hs@2024rt4230:~/disk1$ ict_auth -h
Usage: ict_auth [OPTIONS] COMMAND

A command-line tool for ICT network authentication.

Options:
  -h, --help          Show this help message and exit
  -V, --version       Show version information and exit

Commands:
  login               Log in to the ICT network
  logout              Log out and terminate the session
  status              Show the current login status
  enable              Enable and start the persistent connection service
  disable             Disable the persistent connection service
  logs                Show logs for the persistent connection service
  upgrade             Check for updates and install the latest version
  uninstall           Uninstall ict_auth from the system
```

