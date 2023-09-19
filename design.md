# Design Decisions

## Code storage and collaboration

GitHub was chosen for it's generous Free plan, which provides advanced features to public repositories for free.

## DNS

Although Websupport is used for domain name registration and they provide DNS servers out of the box, we switched to Cloudflare because:

- It's easier to use Cloudflare this way
- They're globally distributed and faster
- It will make switching to Infrastructure as Code easier

## Emails

Cloudflare Email Routing was chosen to handle inbound email messages because:

- We need to forward messages to other email addresses
- It's free and readily available based on the rest of the infrastructure

Websupport Webhosting was chosen to handle outbound email messages because:

- There is a very limited amount of free alternatives, which were all rejected:

  - Gmail is able to send emails under a custom domain name, but it cannot sign them using DKIM unless Google Workspace is used
  - Zoho Email was rejected because Jan didn't want to use an Indan company

- It's already used for domain name registration

## Website

The first website was implemented as a static site because that way:

- It can be served for free
- We don't have to worry about server-side issues
- It's overall the simplest solution

Cloudflare was chosen to host the website because:

- Cloudflare Pages provides unlimited static requests and bandwith even on the Free plan, which means we don't have to worry about the bills nor the site being cut off no matter how popular or attacked it gets
- It's global and fast everywhere
- Provides preview deployements
- Provides advanced features like custom HTTP headers and redirects
- Provides Direct Upload for custom Continuous Delivery
- Server-side functionality can be added easily using Pages Functions

The new website is implemented in WordPress on Websupport because that is what the developer that Jan chosen wants to use. This website infrastructure in Websupport is not covered by this documentation as the developer has not shown interest in contributing here.
