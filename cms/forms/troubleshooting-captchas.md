# ❔ Troubleshooting

If you are building or working on a site and your reCaptcha is now continually failing you can follow the three steps below to get it working again.

Please note that there might be a slight variation depending on which browser you use, however the process remains the same.

### reCaptcha Fix Steps

#### Step 1: Open the Network Tab

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/338162fc7da703a5ec6b0a868ec1eb82389cf2dc6a20b4568d3d8396f1f54724fb5cbb47-3ddd-4f0f-840b-6d1a78\_sewdjj.png)

Open up inspect element, go to the Network tab, filter by XHR and select "Persist Logs" also known as "Preserve Log"

#### Step 2: Submit the form

Now that you have the network tab open, submit the form to generate activity.

#### Step 3: Check the Network Tab

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/88f6c32f87a0beff59304cd7d2c8b1c2f0ba2092cf3134c5f2eb65065c858a148a632732-ee5e-4fff-89a8-ea7b9b\_1stmmd9.png)

Inside the Network Tab, look for a network request to the file 'recaptcha.json'.

Click the recaptcha.json request file to open up a pane to the right with a 'Response' tab.

The response area you have just opened, shows the response received from Google for you reCaptcha request. Be sure that `success: true` and that the value for `score` is equal to or above the value that you have set in your form configuration (see below).

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/3c8ef704b086170a6cfc854653011f2d5d462168217213de697da4c98cf8db5ccf1df3cc-b062-47e8-921e-7369bb\_1pfh52t.png)

If both one of those are not true, then although you may get a message that says "recaptcha failed", what it actually means is that your submission did not meet your request levels. This is not an error with the form, but recaptcha doing its job correctly and blocking what seemed like a suspicious attempt.

You may see this happen if you are testing the form with the same email address in quick succession. If this does happen you may want to lower your minimum score so that the requests are allowed, then you can raise it again later before going live.
