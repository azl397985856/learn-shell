# SSH

Secure Shell is a protocol used to securely log onto remote systems.
It can be used for logging or executing commands on a remote server.

> All commands listed below are sorted by frequency of use

## SSH config

3 different locations:

- command line arguments
- `~/.ssh/config`
- `/etc/ssh/ssh_config`

### Common Settings

- HostName: IP address. note: '%h' will be replaced by the ip specified at commond line.
- IdentityFile
- GlobalKnownHostsFile: global hosts you trusted
- UserKnownHostsFile: personal hosts you trusted
- Port
- User

eg:

```
Host host1
    HostName 192.168.1.1
    User root
Host host2
    HostName 192.168.1.2
    User root
```

## SSH Command

- connect to a remote server:

```bash
$ ssh username@remote_host
```

- connect to a remote server with private key

```bash
$ ssh -i path/to/key_file username@remote_host
```

## SSH-COPY-ID command

Install your public key in a remote machine's authorized_keys.

- Copy your keys to the remote machine:

```bash
$ ssh-copy-id username@remote_host
```

- Copy the given public key to the remote:

```bash
$ ssh-copy-id -i path/to/certificate username@remote_host
```

- Copy the given public key to the remote with specific port:

```bash
$ ssh-copy-id -i path/to/certificate -p port username@remote_host
```

## Example

identify by password:

```bash
$ ssh -p 1003 -i ~/.ssh/id_rsa_test user@192.168.1.1
```

identify by public key:

```bash
$ ssh-copy-id -i ~/.ssh/id_rsa_test user@192.168.1.1
```

identify by config file:

assume that you have a `~/.ssh/config`:

```
Host host1
    HostName 192.168.1.1
    User root
    Port 1003
    IdentityFile ~/.ssh/id_rsa_test
```

now you can :

```bash
$ ssh host1
```
