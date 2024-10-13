# Domain names

As you've seen, if you own a domain name, you can configure DNS records, so that internet traffic will be sent to the server you choose. This page shows how you actually get a domain and configure DNS.

## Getting a Domain

Okay, how do you actually get a domain like kibo.school, so that you can set up a website?

For most websites, you buy a domain. Some are expensive, and others are relatively cheap. There are also some services that offer free domains, which we’ll talk about too.

## Paid Domains

When you buy a domain, you are registered as the owner, usually for some number of years.

That gives you the ability to configure the DNS records, usually through a *registrar.* Often, the same companies that sell the domains will act as the registrar and allow you to configure DNS records.

Domains usually start at **$5-$10 USD**. There are often discounts for the first year of owning a domain. Some domains are more expensive: popular sites, business addresses, and short or memorable domain names sometimes cost thousands or millions of dollars!

### Further reading: Domain pricing

The price often depends on the **top level domain (TLD).** TLDs are like `.com` or `.org` or `.gh`. Depending on the TLD, the price for a similar name might be very different.

There are lots of tools for searching and buying domains. [Google Domains](https://domains.google/) is a relatively high-quality tool. In the past, folks from our team have also used [Hover](https://www.hover.com/domains), [NameCheap](https://www.namecheap.com/), [Vercel](https://vercel.com), and others.

We recommend using [Google Domains](https://domains.google/) if you are searching for or buying a domain. You may find a better price elsewhere, though!

<aside>

⚠️ **You do not have to buy a domain for this class.**

We want you to know how, in case you ever want to buy a domain for a site.

</aside>

## Free Domains

There are lots of hosting providers that will give you a free domain if you pay to host your site with their service. It’s usually not worth it, because their hosting is usually pretty bad.

There are some actually free domains available too (though registration is still required):

- [Replit](https://replit.com/) and [Github Pages](https://pages.github.com/) offer domains that have `.repl.co` and `.github.io` at the end, for free.
- Sites like [Neocities](https://neocities.org/) let you make your own website and host it on a `.neocities.org` domain for free. You can pay for a different domain name.
- [Co.vu](https://codotvu.co/) offers free `.co.vu` domains
- [Freenom](https://www.freenom.com/) offers free .TK, .ML, .GA, .CF, and .GQ domains, but reviewers say that it often doesn’t work.

The free domains are typically not as nice as domains you pay for.

## Github Student Developer Pack Services

Through the [Student Developer Pack](https://education.github.com/pack), you can access a lot of services for free. Namecheap, Name.com, and .tech domains offer free .me, .live, and .tech domains to students.

## Walkthrough: Configuring DNS for a real domain

<aside>

🎥 In this walkthrough, Rob configures DNS for a real site using Github Pages and Google Domains.

See the live site at [http://recipe.kibo-demo.club/](http://recipe.kibo-demo.club/). 

</aside>

<div class="embed"><iframe src="https://www.youtube.com/embed/A7K7QnxE2ms" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>

Video Recap:

1. Starting point:
    - Already bought a domain using Google Domains
    - Already have a site published using Github Pages
2. Add a Custom Domain on the Github Settings page
3. Follow the instructions in the Github error message
    1. In Google Domains, click to DNS in the sidebar navigation
    2. Add a CNAME record
    3. With host name that matches your Custom Domain on the Replit side (`recipe.kibo-demo.club` in the video)
    4. And data that match the [github.io](http://github.io) domain that you can copy from the error message (`kiboschool.github.io` in the video)
4. Be patient
    1. Wait for a while, since it might take a few minutes.
    2. It’s easy to mess things up, so take your time and be patient with yourself.

If you have deployed to a cloud host, there will likely be some differences in the configuration between your app and this video, but not by that much. Your host will likely have an IP address that you will point the A or CNAME record to.

## Practice: Configure your own domain

1. Using the Github Student Pack, get a free domain from one of the providers.
2. Configure the domain so that it points to the hosted application you deployed using one of the cloud providers.
