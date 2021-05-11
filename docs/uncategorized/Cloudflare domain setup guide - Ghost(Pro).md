Cloudflare is a DNS management service and content delivery network (CDN). Ghost(Pro) users commonly route their DNS through Cloudflare for its support of root level CNAMEs and flexible redirects, known as page rules.

The following steps will walk you through how to setup a root domain or subdomain with your Ghost(Pro) publication, using Cloudflare to manage your domain's DNS records.

Regardless of how a user enters your publication's URL in their browser, they'll always be directed to the correct site.

## Step 1: Connect Your Domain to Cloudflare

The first step for both types of configuration is to create a [free Cloudflare account](https://dash.cloudflare.com/sign-up) and follow a few steps. There are paid options available but you only need a free account to setup a custom domain with Ghost.

Enter your domain name when creating your new Cloudflare account and it will query your existing DNS records and port them over. Review these records and port any over that are required.

![](https://ghost.org/help/content/images/2019/08/cf-add-your-site.png)

Update your Nameserver (NS) with your domain provider to the NS records that Cloudflare requests during the setup process. If you're unsure where to update this you may need to contact your domain provider directly:

![](https://ghost.org/help/content/images/2021/01/cloudflare-update-nameservers_o.png)

When your Cloudflare Overview shows a status of "Active" you are ready to configure your domain's DNS to point to your Ghost(Pro) publication - this can take a few minutes:

![](https://ghost.org/help/content/images/2021/01/cloudflare-overview_o.png)

## Step 2: Create a CNAME record

Before configuring a custom domain with your publication, decide whether you want to use a subdomain or root domain as the default URL for your site.

**What is a Subdomain?**  
A subdomain is a subdivision of your domain name. For example, if you want to use Ghost(Pro) at blog.ghost.org, “`blog`,” would be a subdomain of [ghost.org](https://ghost.org/). The most common subdomain is “`www`” e.g. `www.ghost.org`.

**What is a Root Domain?**  
A root domain, also known as a “naked domain,” is a domain without a subdomain in front, e.g. `ghost.org` is a root domain.

Whether you use a root domain or subdomain with your publication is a matter of personal preference, however there are different setup steps for each that must be followed.

### Subdomain Setup

To use a subdomain with your publication (e.g. `www.domain.com`) go to your DNS settings in Cloudflare and create the following DNS records, ensuring the Proxy Status is set to **DNS Only**:

Subdomain DNS Configuration

Record Type

Host

Value

`CNAME`

`www`

`<subdomain>.ghost.io`

`A`

`@`

`178.128.137.126`

### Root Domain Setup

If you'd prefer to use a root domain (e.g. `domain.com`), go to your DNS settings in Cloudflare and create the following DNS records, ensuring the Proxy Status is set to **DNS Only**:

Root Domain DNS Configuration

Record Type

Host

Value

`CNAME`

`@`

`<subdomain>.ghost.io`

`A`

`www`

`178.128.137.126`

## Step 3: Activate the Custom Domain

Login to your publication's Ghost Admin area, and go to the **Ghost(Pro) > Domain** settings.

Click the “Setup” button and follow the prompts to activate your custom domain.