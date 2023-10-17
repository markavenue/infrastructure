# Configuration

The following configuration has been done:

 1. Changed NS DNS records for markavenue.sk and markavenueagency.com to Cloudflare.
 2. Enabled DNSSEC for markavenue.sk and markavenueagency.com in Cloudflare and configured the public keys in Websupport.

    > **_NOTE:_** Removing Websupport-generated keys disables DNSSEC in Websupport.
 3. Enabled Email Security for both domains in website DNS settings in Cloudflare.
 4. Created `markavenue` project in Cloudflare Pages and:

     1. Connected [website] repository to the project via Cloudflare Pages GitHub app.

        (At the time of setting it up, it looked like Cloudflare API didn't provide fine-grained access controls, which would allow us to grand an identity access to a single project. That's why GitHub Actions is not used for deployment.)
     2. Modified Build configurations and enabled Preview deployments.
     3. Set up `www.markavenue.sk` as custom domain.

 5. Configured Email Routing for markavenue.sk in Cloudflare.

     1. Added custom address `info@markavenue.sk` to send emails to `markawenue@gmail.com`.
     2. Set up `markawenue@gmail.com` as catch-all address.

 6. Set up `info@markavenue.sk` for sending outbound messages.

     1. Created `info@markavenue.sk` mailbox in Websupport with only SMTP allowed.
     2. Updated SPF DNS record to include `_spf.m1.websupport.sk`.
     3. Set up DKIM DNS record in Cloudflare based on the value from Websupport.
     4. Configured Websupport SMTP server in `markawenue@gmail.com` Gmail to send messages as `info@markavenue.sk`.

 7. Configured a Page Rule to redirect https://markavenue.sk to https://www.markavenue.sk according to [Redirect example.com to www.example.com].
 8. Configured SSL/TLS for markavenue.sk in Cloudflare by:

     1. Setting encryption mode to Full (strict) in Overview.
     2. Setting up HTTP Strict Transport Security in Edge Certificates.
     3. Setting Minimum TLS Version to 1.2 in Edge Certificates.
     4. Enabled Certificate Transparency Monitoring in Edge Certificates.

 9. Set up `0 issue ;` CAA DNS record for markavenue.sk, which forces Cloudflare to publish their own CAA records as well.
10. Set up MTA-STS for markavenue.sk.

     1. Set up [mta-sts] repository.
     2. Gave Cloudflare Pages GitHub app access to the repository.
     3. Created `mta-sts-markavenue` Cloudflare Pages project and disabled preview deployments.
     4. Set up `mta-sts.markavenue.sk` as custom domain.
     5. Set up `_mta-sts.markavenue.sk` TXT DNS record.

    > **_NOTE:_** Using a Cloudflare R2 bucket would have been a better choice, but at the time of setting it up, R2 required a plan purchase (which required us to enter a credit/debit card) even on the free plan.

11. Set up TLS-RPT for markavenue.sk.

     1. Created `mark-avenue-tls-reports@googlegroups.com` and allow anyone on the internet to post and attach files.
     2. Added `markawenue@gmail.com` and set their subscription to `No email`.
     3. Set up forwarding from `tls-reports@markavenue.sk` to `mark-avenue-tls-reports@googlegroups.com`.
     4. Created `v=TLSRPTv1; rua=mailto:tls-reports@markavenue.sk` TXT record for `_smtp._tls.markavenue.sk`.

12. Set up DMARC reporting for markavenue.sk.

     1. Created `mark-avenue-dmarc-reports@googlegroups.com` and allow anyone on the internet to post and attach files.
     2. Added `markawenue@gmail.com` and set their subscription to `No email`.
     3. Added `rua=mailto:dmarc-reports@markavenue.sk` to DMARC DNS record.

13. Verified markavenue.sk on GitHub by adding `_github-challenge-markavenue-org.markavenue.sk` and `_github-challenge-markavenue-org.www.markavenue.sk` TXT DNS records.
14. Enabled DMARC Management for markavenue.sk in Cloudflare and appended `,bae43f485fca44fab749cd5780b41997@dmarc-reports.cloudflare.net` to RUA attribute of the DMARC DNS record.
15. Pointed `www.markavenue.sk` to `37.9.175.181` and `2a00:4b40:aaaa:2007:0000:0000:0000:0005` with proxying enabled. These IP addresses came from Websupport DNS configuration for markavenue.sk.
16. Created `www.markavenue.sk` TLS certificate in Websupport.
17. Removed `www.markavenue.sk` custom domain from `markavenue` project in Cloudflare Pages as per certificate renewal email from Cloudflare, which told us to remove the unused hostname.

[mta-sts]: https://github.com/markavenue/mta-sts
[Redirect example.com to www.example.com]: https://community.cloudflare.com/t/redirect-example-com-to-www-example-com/78348
[website]: https://github.com/markavenue/website
