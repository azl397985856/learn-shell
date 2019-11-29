# NetWork Management

## IfConfig

IfConfig is a command line tool used to configure network interfaces.

### Usage

Generally, It can be used for:

#### View NetWork data

The Simplest way to use `ifconfig` is `ifconfig` itself without any parameters. It will show you details of the network interfaces which are running in your computer. Also, i's the major part of the `ifconfig` command.

eg:

```
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	options=1203<RXCSUM,TXCSUM,TXSTATUS,SW_TIMESTAMP>
	inet 127.0.0.1 netmask 0xff000000
	inet6 ::1 prefixlen 128
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
	nd6 options=201<PERFORMNUD,DAD>
gif0: flags=8010<POINTOPOINT,MULTICAST> mtu 1280
stf0: flags=0<> mtu 1280
...
```

Here are the mostly seen interfaces:

```
lo = loopback
gif = Software Network Interface
stf = 6to4 tunnel interface
en = Ethernet
fw = Firewire
en = Ethernet
vmnet = Virtual Interface
```

My Machine info:

```bash
$ sw_vers
# ProductName:	Mac OS X
# ProductVersion:	10.15.1
# BuildVersion:	19B2106

$ uname
# Darwin
```

forthermore, let me explain the frequently used fields for you.

- `inet addr` - IP address
- `Bcast` - broadcast addr
- `UP` - means Ethernet interface has been loaded
- `RUNNING` - means the interface is ready to accept data
- `MTU` - short for 'Maximum Transmission Unit' which is the size of each packet received by the Ethernet card, default is 1500, you can change it which cover at next section.

for more info, please visite: [ifconfig-dissected-and-demystified](http://www.aboutlinux.info/2006/11/ifconfig-dissected-and-demystified.html)

#### Configure Network interfaces

The values of almost all the options listed above can be modified.But please don't do that if you know what you are doing.

for example, you want to change the MTU to 5000:

```bash
/sbin/ifconfig eth0 mtu 5000 up
```

> Actually, there [a lot of way to change the MTU](https://www.cyberciti.biz/faq/centos-rhel-redhat-fedora-debian-linux-mtu-size/)

### Trick

- lookup ipv4 addr

```bash
ifconfig | grep 'inet\b'
```

## Dig

Dig is yet another command line tool, which is much similar to Linux `Nslook`.Dig is short for `Domain Information Groper`, It's a network tool for querying DNS(Domain Name System) info which is avaliable in marjor Linux distributions. When you have trouble with DNS, it's a good choice to use it.

### Simple Usage

#### dig hostname

The Simplest way to use Dig is `dig hostname` without extra arguments. If So you will See the output below: (eg: `dig lucifer.ren`)

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g9dyxwboq8j30u01ds7bv.jpg)

The output is carefully commented， splited into six parts by new line. What we really care about is the "ANSWER SECTION". There are five fields of the ANSWER SECTION in dig query, Let me explain that for you.

1. The First field is domain name.
2. The second one is TTL(Time To Alive)
3. The third one is class(In for internet)
4. And the Record Type filed.

The Record Type such as "CNAME", "A", "NS".

- A for "pointing to a IP addr"
- CNAME for "pointing to another domain"
- NS for "pointing to anoter DNS Server"

for more, please visite [DNS Record types](https://simpledns.com/help/dns-record-types)

5. Last One is IP Addr.

#### dig -x ip to Querying DNS Reverse Look-up.

eg:

```bash
dig -x 216.239.34.10 +short
# Output: ns2.google.com.
```

#### "+short" for brief info

As I Claimed, Usaully what we really care about the "ANSWER SECTION", "+short" can help.

### Advanced Usage

1. trace
2. specify DNS Server

if not specified, It will read the dns server specified at `/etc/resolv.conf` line by line.

my file `/etc/resolv.conf`:

```
nameserver 192.168.2.5
nameserver 202.101.172.35
```

You can explicitly specify the dns sever by inputing the dns server ip startingwith @ symbol. like this:

```bash
dig @114.114.114.144 lucifer.ren
```

### Reference

- [10-linux-dig-domain-information-groper-commands-to-query-dns](https://www.tecmint.com/10-linux-dig-domain-information-groper-commands-to-query-dns/)
