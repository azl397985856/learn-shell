# SUDO

Executes a single command as the superuser or another user.

- Run a command as the superuser:

```bash
$ sudo less /var/log/syslog
```

- Edit a file as the superuser with your default editor:

```bash
$ sudo -e /etc/fstab
```

- Run a command as another user and/or group:

```bash
$ sudo -u user -g group -a
```

- Repeat the last command prefixed with "sudo" (only in bash, zsh, etc.):

```bash
$ sudo !!
```

- Launch the default shell with superuser privilege

```bash
$ sudo -i
```
