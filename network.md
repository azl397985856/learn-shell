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

The output is carefully commented， splited into six parts by new line. What we really care about is the "ANSWER SECTION".

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
3. custom your own output format

## Reference

### Dimain Record Type

The Record Type such as "CNAME", "A", "NS".

- A for "pointing to a IP addr"
- CNAME for "pointing to another domain"
- NS for "pointing to anoter DNS Server"

for more, please visite [DNS Record types](https://simpledns.com/help/dns-record-types)

## Trick

- lookup ipv4 addr

```bash
ifconfig | grep 'inet\b'
```

## Read More

- [10-linux-dig-domain-information-groper-commands-to-query-dns](https://www.tecmint.com/10-linux-dig-domain-information-groper-commands-to-query-dns/)
