# 🔧 Assets Troubleshooting

## Diagnosing issues

If you cannot see the asset on your page then you can check the following common issues:

* Check the string you used for a path does not start with a forward slash or "assets".

e.g. these will **fail** because the "/" or "assets/" beginning of the path will end up being added twice.

```liquid
{{'assets/images/SG-Logo-White.svg' | asset_url }}
{{'/images/SG-Logo-White.svg' | asset_url }}
```

* Check the file manager or code editor shows the correct path for your asset, including any folders.
* You should include the file extension for your asset in the path e.g. ".jpg"

e.g. this will fail because an asset's full name has not been included:

`{{'images/SG-Logo-White' | asset_url }}`

* Make sure you wrap your path in quotes as it is a string:

e.g. here a string was forgotten and validation on Admin or Siteglide CLI should not accept it:

`{{images/SG-Logo-White | asset_url }}`

### Special Characters and Spaces

Ideally, try not to upload files which contain special characters or spaces. However, if this is unavoidable, there are ways to fix the "access denied" errors you may see when you follow a link to an image like this.&#x20;

Dashes '-' and forward slashes '/' are not counted as special characters for this purpose.  \
\
When uploaded to AWS, any special characters or spaces will be URL encoded automatically. But to access the file, you will need to encode the path and then replace the % signs in the encoded string with the encoded version of the % sign "%25".

```liquid
{{'images/example image with spaces!.jpg' | url_encode | replace: "%", "%25" | asset_url }}
```

\
If you're experiencing this issue and need further guidance, contact support.&#x20;
