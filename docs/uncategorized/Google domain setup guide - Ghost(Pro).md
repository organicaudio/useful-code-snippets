Using a custom domain with Ghost(Pro) not only makes your site memorable, but also establishes your publication as a professional brand.

You can connect any domain or subdomain you've purchased from Google Domains to your Ghost(Pro) publication by adding a CNAME record to your domain's DNS settings. SSL certificates are automatically provisioned  (and renewed each year) for you.

Regardless of how a user enters your publication's URL in their browser, they'll always be directed to the correct site.

If you own a domain through Google Domains, the following steps explain how you can map your custom domain to your Ghost(Pro) publication.

## **Step 1: ****Access Domain DNS Settings******

The first step in setting up your custom domain is to sign into your [Google Domains](https://domains.google/) account and head over to your domain's DNS settings.

## Step 2: Create CNAME Records

In the "Custom resource records" section of your DNS settings, create the following DNS records:

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

**Note:** The `A` record will automatically redirect the `http` and `https` root domain to the subdomain you configure.

**Root Domain Configuration**  
Google Domains **does not support `CNAME` root domain configurations** and using an `A` record to achieve a root domain is not supported. To setup a root domain configuration, we recommend that you consider using [Cloudflare](https://ghost.org/help/cloudflare-domain-setup/) for additional flexibility.

## Step 3: Activate the Custom Domain

Login to your publication's Ghost Admin area, and go to the **Ghost(Pro) > Domain** settings.

Click the “Setup” button and follow the prompts to activate your custom domain.