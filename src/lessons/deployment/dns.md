# Domains and DNS

## Domain Names

To give your site a custom URL, you need to know more about **Domain Names.** Domain Names are how your browser finds the server to talk to.

## IP Addresses & DNS

<aside>

🎥 Check out this Code.org video to learn more about DNS

</aside>

<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.youtube.com/embed/5o8CwafCxnU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

To recap:

- The Domain Name System (DNS) is how your computer finds the address (like 162.159.135.42) like for a name (like kibo.school)
- DNS uses a *distributed hierarchy* of DNS servers. When one DNS server doesn’t know the answer, it asks another “higher” DNS server.
- 👑  “Root” DNS servers manage the *top level domains,* like .com and .org

### Further Reading: MDN on Domain Names

See the MDN page [What is a Domain Name?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_domain_name) for more

## What does it mean to own a domain name?

When someone buys a domain name, they get to decide which IP address the name points to. When Ope bought the [kibo.school](http://kibo.school) domain, she set the address to **162.159.135.42**. That’s the address of the Kibo server.

### Website building and publishing steps:

Making [kibo.school](http://kibo.school) involves these steps:

- Build the site (using HTML, CSS, and JS)
- Publish the site on a server
- Use DNS to make the [kibo.school](http://kibo.school) point to the server’s IP address

### How does your browser load kibo.school?

When you type [kibo.school](http://kibo.school) into your browser:

1. Your browser asks DNS for the address of [kibo.school](http://kibo.school), and gets back **162.159.135.42**
2. Your browser asks **162.159.135.42** for the actual webpage
3. The server at that address sends back the files that make up the site you see (HTML, CSS, and JS, plus images and videos)

![DNS lookup for Kibo School](/images/dns-lookup.png)

## DNS Records

Now that we know what DNS is for, let’s talk a tiny bit about what it actually looks like. The graphic above showed the record like this:

![Kibo's IP Address](/images/dns-kibo.png)

At its heart, DNS is really simple: it matches a name and a value. In this case, the name `kibo.school` is matched with the value `162.159.135.42`

The actual DNS record looks like this:

```txt
kibo.school.		3600	IN	A	162.159.135.42
```

This says that `kibo.school` points to `162.159.135.42`. It’s also got some extra info:

- There’s an extra `.` after `kibo.school`
- There’s a **TTL** of `3600`
- It’s an `A` record

The extra dot means that it’s an *absolute* domain name. You can basically ignore this. (If it bugs you, you can read an explanation [here](http://www.dns-sd.org/trailingdotsindomainnames.html).)

**TTL** stands for “time to live” and it says how long a DNS server should keep a copy of this record before it checks again. If it’s shorter, updates to the DNS record will show up faster, but the website might load slower for users.

**`A`** is the *type* of record.

**`IN`** means it's an INternet record. All DNS records are IN.

## Types of DNS Records

There are lots of different types of DNS records. Different types tell different kinds of information, like:

- The email server is located at this address (`MX` type records)
- This name points to a different name (`CNAME` type records)

`A` records match a domain name to an IP address. For matching the domain `[kibo.school](http://kibo.school)` to the address `162.159.135.42`, we use an `A` record.

As noted in the video, IP addresses like `162.159.135.42` are version 4 addresses. `AAAA` records are for IP version 6.

### Further Reading: DNS

Cloudflare is a popular service for DNS management, among other services and tools. 
Their help center has great explanations on [What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/) and [DNS records](https://www.cloudflare.com/learning/dns/dns-records/).

## Try it: Mess with DNS

Get hands-on practice creating DNS records to tell browsers where to find different websites.

1. Go to [https://messwithdns.net/](https://messwithdns.net/)
2. Follow the three tutorial experiments to learn how to use the tool.
3. Do as many other experiments as you like, to explore creating different kinds of DNS records. Don’t be afraid to use Google to learn more as you explore.
4. Make sure you do the “**Set up a website**” experiment under the “**Useful experiments**” section

## Questions about DNS

🤔 You’ve probably learned some pieces about DNS, but not everything.

Check your understanding of DNS and learn some more facts about DNS with this interactive game. 

Visit [https://questions.wizardzines.com/dns.html](https://questions.wizardzines.com/dns.html) and try to guess for each question. You might know some of the answers, and you’ll probably learn something too!

## Further Reading: Julia Evans, creator of Mess with DNS and DNS Questions

Julia makes tons of awesome comics, like this one on [How to be a Wizard Programmer](https://wizardzines.com/zines/wizard/).

You can find more of her work online at [https://wizardzines.com/](https://wizardzines.com/). 

Julia’s [blog post about the process of creating the Mess with DNS tool](https://jvns.ca/blog/2021/12/15/mess-with-dns/) is a really fun read!
