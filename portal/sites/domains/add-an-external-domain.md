# Add an External Domain

{% hint style="warning" %}
We strongly recommend Fully Delegating your domain for best results and to avoid additional steps redirecting the non-www to www.
{% endhint %}

If you have a domain that is managed in GoDaddy or another registrar and would like to point it to a Siteglide website you can use our External Domain feature. This means that you can continue to manage your DNS through GoDaddy/other registrar.

## Step 1: Add a Domain

Navigate to the Domains tab on the Site and click Add Domain:

<figure><img src="../../../.gitbook/assets/Siteglide-Site-Domains-None.png" alt=""><figcaption></figcaption></figure>

## Step 2: Choose External

<figure><img src="../../../.gitbook/assets/Siteglide-Site-Domains-Add-External.png" alt=""><figcaption></figcaption></figure>



## Step 3: Enter Domain Details

Type in the root domain without www and you'll likely want to set it as the Default Domain and Enable WWW Redirect. Then click Add Domain:

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domain-External-Add.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Important Note:** _Your domain can take up to a few minutes to be fully added to the system. Please check back and refresh the page shortly._
{% endhint %}

## Step 4: Add SSL Verification CNAME

Once your domain has finished creating in the system, it's status will change to "Ownership Verification Pending" which means it is now ready.

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domain-External-Verify-SSL.png" alt=""><figcaption></figcaption></figure>

Add the generated CNAME record to in your DNS control panel to verify ownership, generate an SSL certificate and automatically apply it to your site during the next step.

### GoDaddy example:

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/fc70b36dfbcfe3696b886456b64583f8b636d658356a1fc1bc8c65040f4c4e7135e9327e-5fa5-4d74-b88d-fc9d49\_12o0sfv.jpeg)

Once you have saved the record in your registrar, allow some time for propagation, check back and refresh the page.

{% hint style="warning" %}
**Important Note:** _The CNAME verification record must NOT be deleted at any point otherwise the SSL certificate will not renew._
{% endhint %}

## Step 5: Add WWW CNAME Record

Once the verification CNAME record has propagated the WWW CNAME Record needs to be added in your DNS Control Panel (GoDaddy example):

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domain-External-WWW-CNAME.png" alt=""><figcaption></figcaption></figure>

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/675766690a2105effba6c541fa9042718196bc0aca64a984869352884ea916b720f847b9-5e47-4982-aaea-e44bff\_w8y6cl.jpeg)

The site will now be live via WWW (https://www.domain.com) but not via the root domain (https://domain.com). Complete Step 5 to fully setup the domain correctly. The domain should show as 'Live' under the Status column in Siteglide:

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domain-External-Live.png" alt=""><figcaption></figcaption></figure>

## Step 5: Forward the Root/@ to the www (with SSL)

Most DNS Control Panels cannot correctly redirect the root traffic to the WWW over SSL so we recommend using an external service called Redirect.Pizza.

Just follow these steps to redirect your **non-www** to the **www** variant. The non-www is also sometimes called naked record or "apex" (screenshots below):

1. Create a [redirect.pizza](https://redirect.pizza/register) account.
2. Add your source. This should be the domain without www. For instance, enter **example.com** as your source.
3. Set the destination to the variant with www. Example: **www.example.com**
4. Press "Create redirect"
5. The required DNS change pops up. Go to your domain registrar to make this DNS change for the **A** record. This record may already exists '@'. Press 'edit' to edit it to the required DNS setting for redirect.pizza. For more info, see [What are these DNS changes?](https://redirect.pizza/support/what-are-these-dns-changes)
6. The DNS change is made! It may take up to 24 hours before the DNS is fully propagated.

<div>

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domains-External-Redirect-Pizza-Verified.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domains-External-Redirect-Pizza-Checking.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domains-External-Redirect-Pizza-Create.png" alt=""><figcaption></figcaption></figure>

</div>

These Steps can also be found here: [https://redirect.pizza/support/redirecting-non-www-to-www](https://redirect.pizza/support/redirecting-non-www-to-www)
