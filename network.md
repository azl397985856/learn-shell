# NetWork Management

## IfConfig

TODO

## Dig

Dig is yet another command line tool, which is much similar to Linux `Nslook`.Dig is short for `Domain Information Groper`, It's a network tool for querying DNS(Domain Name System) info which is avaliable in marjor Linux distributions. When you have trouble with DNS, it's a good choice to use it.

## Syntax

`dig - DNS lookup utility`

## Simple Usage

1. dig hostname

The Simplest way to use Dig is `dig hostname` without extra arguments. If So you will See the output below: (eg: `dig lucifer.ren`)

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g9dyxwboq8j30u01ds7bv.jpg)

The output is carefully commented， splited into six parts by new line. What we really care about is the "ANSWER SECTION". There are five fields of the ANSWER SECTION in dig query, Let me explain that for you.

- The First field is domain name.
- The second one is TTL(Time To Alive)
- The third one is class(In for internet)
- And the Record Type filed.

The Record Type such as "CNAME", "A", "NS".

- A for "pointing to a IP addr"
- CNAME for "pointing to another domain"
- NS for "pointing to anoter DNS Server"

for more, please visite [DNS Record types](https://simpledns.com/help/dns-record-types)

- Last One is IP Addr.

2. dig -x ip to Querying DNS Reverse Look-up.

eg:

```bash
dig -x 216.239.34.10 +short
# Output: ns2.google.com.
```

3. +short

As I Claimed, Usaully what we really care about the "ANSWER SECTION", "+short" rocks.

## Advanced Usage

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

## Trick

- lookup ipv4 addr

```bash
ifconfig | grep 'inet\b'
```

## Reference

- [10-linux-dig-domain-information-groper-commands-to-query-dns](https://www.tecmint.com/10-linux-dig-domain-information-groper-commands-to-query-dns/)
