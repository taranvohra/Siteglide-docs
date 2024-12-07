# 🏗️ Tailwind CSS Themes - Choosing a Build Method

![Choosing a Build Method](https://res.cloudinary.com/sitegurus/image/upload/v1656591688/modules/module\_86/admin/library\_thumbs/tailwindui.jpg)

Tailwind CSS is accelerating in popularity with its bold new approach to writing CSS for the web. You’re probably wondering how you can harness this new framework on a Siteglide site?

Tailwind’s approach to performance means it provides a huge range of utility classes, but to prevent it from slowing down your site with classes you don’t need, it builds a smaller CSS file containing just the subset of classes that you’re actually using in your project.

There are a few alternatives to consider when it comes to generating a Tailwind CSS file for your Siteglide site:

1. A Command Line Interface (CLI) Compilation on your machine (recommended)
2. Preview Mode
3. Just In Time (JIT) Compilation in the Browser (deprecated)

### Which one is right for me? <a href="#which-one-is-right-for-me" id="which-one-is-right-for-me"></a>

That depends!

Both methods have their advantages, which we'll look at here, but it also depends on the preference of the developer and the type of project you're working on.

| Question                                                                                       | Tailwind CLI                                                                                              | Preview Mode                                                                                                                             | JIT CDN (deprecated)                                                                                                                                                                                                                                                 |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Will it support CSS classes that sit inside Secure Zones or other Liquid logical statements?   | ✔️                                                                                                        | ✔️ So long as it uses Flowbite blocks or components.                                                                                     | ❌ See [Safelisting classes which are added via user-interaction](/sitebuilder/setup-sitebuilder/styling/tailwinds-jit-compiler-via-cdn-beta-not-recommended-for-production.md#safelisting-classes-which-are-added-via-user-interaction) for possible workarounds and recommendations |
| Can I use the latest version of Tailwind?                                                      | ✔️                                                                                                        | ✔️                                                                                                                                       | Not yet. You can use most features from version 2.0 of Tailwind. We rely on Open Source code to provide the JIT method and it is not possible to keep it fully up to date as Tailwind brings out new versions.                                                       |
| Can I use 3rd party Tailwind Plugins?                                                          | ✔️                                                                                                        | ✔️only when used in combination with a CLI build.                                                                                        | ✔️ See [Beyond Code - Tailwind's JIT Tailwind Compiler Via CDN](https://beyondco.de/blog/tailwind-jit-compiler-via-cdn) for details. The 1st party plugins will work well but we cannot guarantee that all 3rd party plugins will.                                   |
| Can I add Flowbite blocks from the SiteBuilder Module and have them look right out of the box? | ❌ You will need to use CLI to pull your site to your machine, rebuild Tailwind and sync the new CSS file. | ✔️ But if you're changing brand variables, or adding new Tailwind classes not used by Flowbite, you will need to complement with a CLI.  | ✔️                                                                                                                                                                                                                                                                   |
| Is it optimised for performance?                                                               | ✔️ CSS is ready to go before user visits the page.                                                        | ❌While an improvement on JIT or Tailwind Play CDN, extra CSS files will be slower than CLI build only.                                   | ❌ See the [JIT section](https://beyondco.de/blog/tailwind-jit-compiler-via-cdn) for more details on caching to optimise performance.                                                                                                                                 |

In the end, it depends on your preference and the way your clients wish to use your site.&#x20;

If you use the Siteglide-CLI already to take advantage of modern code editing tools, you'll be right at home with our recommended method: Tailwind CLI.

{% content-ref url="../set-up-tailwind-css.md" %}
[set-up-tailwind-css.md](../set-up-tailwind-css.md)
{% endcontent-ref %}

{% content-ref url="../editing-tailwind-css.md" %}
[editing-tailwind-css.md](../editing-tailwind-css.md)
{% endcontent-ref %}

If you, or your client, wish to build and preview your Pages in the Siteglide Admin without frequent use of the Siteglide CLI, Preview Mode may be for you. We still recommend using the Tailwind CLI now and again to set up your brand variables and to set them consistently across all of your pages at once, but this does not need to be done every time you make a change in Admin, allowing for a potentially smoother experience for clients and development.&#x20;

{% content-ref url="../styling/tailwind-css-preview-mode.md" %}
[tailwind-css-preview-mode.md](../styling/tailwind-css-preview-mode.md)
{% endcontent-ref %}
