# 🏗️ Tailwind CSS - Preview Build

{% hint style="info" %}
Preview Mode is not recommended for Live Sites. We recommend only using CLI to compile Tailwind which will load the minimum CSS possible and maximise performance.
{% endhint %}

Our Preview Mode is designed to keep the convenience of Tailwind code which "just works out of the box" without the drawbacks of needing to recalculate the Tailwind CSS every time you view the Page.

Preview Mode is designed so it can be used on its own, or in combination with the recommended CLI method. See below!

#### Why is it needed?

Options such as the [Tailwind Play CDN ](https://tailwindcss.com/docs/installation/play-cdn)(or our now deprecated JIT method) generate CSS at runtime, so they cannot see classes which are needed for different states of Liquid logic, for example if you log in or out of a secure zone.

## Page Template Level Control

In the past, we used SiteBuilder module settings to let you pick your preferred build method. Now this can also be set on the Page Template level. This allows you to, use a CLI method for faster live pages, and a Preview method for pages which are still in development.

You can set Preview Mode on a Page Template either when you create a Page Template in SiteBuilder:

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Or, by editing the Page Template code:

### Preview Mode On

```liquid

{% raw %}
{% include 'modules/module_86/tailwind/head', template_build_method: 'preview', optional_path_to_cli_css: 'css/tailwind.min.css' %}
{% endraw %}
```

### CLI build only

```liquid
{% raw %}
{% include 'modules/module_86/tailwind/head', optional_path_to_cli_css: 'css/tailwind.min.css' %}
{% endraw %}
```

{% hint style="info" %}
SiteBuilder automatically checks if a custom Tailwind CLI build exists. If you have one, providing a path, even to the default location, you can improve page speed, whether preview mode is on or off.
{% endhint %}

If no custom CLI build can be found and no path is provided, preview mode will be used automatically, even if CLI build is selected as a preference.

## How does it work? A custom build with fallbacks

The Preview mode starts by adding two CSS files from CDNs to your Page Template's `<head>:`

1. A CSS file distributed by Flowbite containing Tailwind classes to support the vast majority of their blocks and components [https://cdnjs.cloudflare.com/ajax/libs/flowbite/flowbite.min.css](https://cdnjs.cloudflare.com/ajax/libs/flowbite/flowbite.min.css) (will always load latest version of Flowbite)
2. A CSS file from the SiteBuilder Module containing Tailwind classes used by our version of the Tailwind blocks - this may differ slightly from Flowbite's as we support Liquid logic, meaning we may need to support both a login button's logged in and logged out states for example. This also supports "primary" colour variables which we use instead of "blue".&#x20;

Together these CSS files create a set of fallbacks which allow Flowbite Layouts to look how Flowbite and SiteBuilder intended out of the box, should these classes not be included elsewhere. However, they won't have any of your branded variables set, like colours or fonts. The extra load time for these CSS files is also the reason why it's not generally recommended to use Preview Page for pages in Production.

3. To get a more consistent look and to apply your brand variables, Preview mode can also pull in a custom CLI Tailwind build underneath the other two. Where this 3rd CSS file contains the same class as one of the other 2 files, e.g. \`bg-blue-700\` it will overwrite it with the correct variables e.g. the correct shade of blue. Where the custom build does not yet support a class, the original Flowbite variables will be used as a fallback.  Unlike a purely CLI-based approach, you don't need to spin up the CLI every time you make a change to the HTML, as you can use the fallbacks while developing and rebuild the custom CSS later, e.g. when you finish a page.&#x20;

### Safelist

If you know you wish to support more classes using your brand variables in future, you can consider adding them to the [safelist](https://tailwindcss.com/docs/content-configuration#safelisting-classes) in your custom CLI Tailwind Config. Just bear in mind that this can make a template which is only using the CLI CSS less efficient as it can use less tree-shaking.

## Use Cases

### Clients working in Studio

If you are building a site where you want clients to be able to build out Pages themselves using the Studio tab, you could consider creating a Page Template for them with Preview Mode enabled. \
\
This allows clients to drag in blocks from SiteBuilder and to use them out of the box.&#x20;

However, you can support them by running a CLI Tailwind build as well, either:

1. At the end of each day or week, to tidy up inconsistencies and add brand variables to Pages still using Preview Mode which may be missing them. Clients can continue using Preview mode but every time you rebuild the Tailwind, more and more common classes are covered by consistent variables.&#x20;
2. When the Client finishes a Page or set of Pages and are ready to put them live and they let you know they are ready to "publish". You run a Tailwind CLI build and switch the Page Template to one with preview mode turned off, giving site visitors a faster experience. Note that by default preview mode templates are **still visible to site visitors.** If using this workflow, you may wish to add Liquid logic to the Page Template which either requires a visitor to be viewing in the Studio tab or to enter a \`?preview=true\` at the end of the URL in the browser:

```liquid
{% raw %}
{% if context.headers.HTTP_USER_AGENT contains "node-fetch" or context.params.preview == true %}
    {{content_for_layout}}
{% else %}
    {% response_status 404 %}
    {% redirect_to '/404' %}
{% endif %}
{% endraw %}
```
