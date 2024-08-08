# ℹ️ Explained - Preventing Spam Form Submissions and Captchas

Siteglide offers Spam protection called hCaptcha on forms, which is already fully baked in to the platform for you.

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/bd16a63ca791723e24fbf264242c0623ee6dad191af3508c6d4418999c3c7076hcaptcha-frontend-1\_1902qi.png)

hCaptcha is the world's most widely used independent CAPTCHA service with a focus on performance, privacy and security.

From today, both Siteglide and platformOS teams recommend that you use the integrated hCaptcha option instead of the now deprecated reCAPTCHA offering, to minimise risk of spam attacks and increase control of usage on your sites.

Please remember that Siteglide is usage-based and it's important to use to hCaptcha spam protection to avoid unwanted increases in usage and charges.

#### A better CAPTCHA

We reviewed a number of other CAPTCHA solutions, but in the end we selected hCaptcha for a number of reasons including: cost, performance, security and user experience.

**Cost**

As hCaptcha is fully built into our platform, there are no API calls needed for verification which contribute to your site usage, unlike reCAPTCHA which requires one API call per form submission as it is a 3rd party API integration.

**Performance**

In the battle against malicious bots, hCaptcha takes an entirely different approach, designed with scalability, accuracy, and performance in mind without relying on historic data or the personal information of users.

hCaptcha only needs to be integrated on pages you want to protect, not on every page of your site like reCAPTCHA v3. It can be implemented with just one line of liquid, which outputs only 3 lines of code.

**Security**

hCaptcha adapts to threats automatically thanks to built in advanced machine learning capabilities. It adapts and learns, constantly providing a better experience and reducing the likelihood of a false positive, penalising users.

In addition, hCaptcha provides heightened protection against spam by re-checking the challenge result at every stage of the form submission process.

**User Experience**

hCaptcha is totally device and browser agnostic, providing a low friction experience to all end users alike. reCaptcha on the other hand requires the presence of Google cookies and personal information to provide a similar low friction experience, which means it will often penalise legitimate users if they are not logged into a google account.

hCaptcha is also specifically designed to protect user privacy and complies with GDPR, CCPA, LGPD, PIPL, and other mandates.

#### Using hCaptcha

Head over to your Site Admin today and Edit Form Structure on one of your existing forms to make the switch. Look for the renamed “Spam Protection” tab to select and save the new hCaptcha option.

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/42fe52de0bec0d548b4fa851386171ff5f0c9d01917f5c7fb510a8b5e60a18ddhcaptcha-form-1\_1btiwv3.png)

For those of you using custom Form layouts, once you have edited and applied hCaptcha to your form, checkout the Default layout to copy the latest CAPTCHA liquid tag across to your custom layout and replace the previous version.

If you’re looking to create a new form in your Siteglide site, hCaptcha will automatically be selected in the Spam Protection tab for you so that you will be fully protected by default.
