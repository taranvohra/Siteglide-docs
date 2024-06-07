# Steps to Add Payment to a Module


You can set your Module up to require payment before a user can install it.

All payments are handled through your Stripe account.

Follow the steps below to add this requirement:

1.  You need to link your Stripe account to your Agency in order to take payments. Go to your Agency edit view, and click the 'Marketplace Payment Details' tab. Read the details shown on this screen and then enter your Stripe Secret Key ([found here](https://dashboard.stripe.com/apikeys))

2.  Go to the Module edit view, and click the 'Payment Details' tab. Here you can toggle 'Take Payment?' to 'Yes' if it is required.

3.  Enter the Stripe Product ID for your Module. This Product will need a Price attached to it in Stripe.

4.  Select the Access Type you want to grant. There's 2 options:
    1.  User only - This will grant access to the paying User

    2.  Agency-wide - This will grant access to the entire Agency of the paying User

5.  You can manually manage User/Agency IDs in the 'Access List' field if you need to do so. This field will auto-update when a User pays for your Module.

6.  That's it! Now, when a User sees your Module in the Marketplace they'll be required to pay before they can install the Module.