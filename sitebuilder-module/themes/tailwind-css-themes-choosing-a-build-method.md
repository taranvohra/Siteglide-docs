# 🎨 Tailwind CSS Themes - Choosing a Build Method

![Choosing a Build Method](https://res.cloudinary.com/sitegurus/image/upload/v1656591688/modules/module\_86/admin/library\_thumbs/tailwindui.jpg)

Tailwind CSS is accelerating in popularity with its bold new approach to writing CSS for the web. You’re probably wondering how you can harness this new framework on a Siteglide site?

Tailwind’s approach to performance means it provides a huge range of utility classes, but to prevent it from slowing down your site with classes you don’t need, it builds a smaller CSS file containing just the subset of classes that you’re actually using in your project.

There are two main alternatives when it comes to generating an optimised Tailwind CSS file for your site:

1. Just In Time (JIT) Compilation in the Browser
2. A Command Line Interface (CLI) Compilation on your machine

### Which one is right for me? <a href="#which-one-is-right-for-me" id="which-one-is-right-for-me"></a>

That depends!

Both methods have their advantages, which we'll look at here, but it also depends on the preference of the developer and the type of project you're working on.

| Question                                                                                     | Tailwind CLI                                       | Tailwind JIT CDN                                                                                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Will it support CSS classes that sit inside Secure Zones or other Liquid logical statements? | ✔️                                                 | ❌ See [Safelisting classes which are added via user-interaction](https://www.sitegurus.io/documentation/sitebuilder/themes/tailwinds\_jit\_compiler\_via\_cdn#safelisting-classes-which-are-added-via-user-interaction) for possible workarounds and recommendations |
| Can I use the latest version of Tailwind?                                                    | ✔️                                                 | Not yet. You can use most features from version 2.0 of Tailwind. We rely on Open Source code to provide the JIT method and it is not possible to keep it fully up to date as Tailwind brings out new versions.                                                       |
| Can I use 3rd party Tailwind Plugins?                                                        | ✔️                                                 | ✔️ See [Beyond Code - Tailwind's JIT Tailwind Compiler Via CDN](https://beyondco.de/blog/tailwind-jit-compiler-via-cdn) for details. The 1st party plugins will work well but we cannot guarantee that all 3rd party plugins will.                                   |
| Can I regenerate the Tailwind from the Siteglide Admin without using the CLI                 | ❌                                                  | ✔️                                                                                                                                                                                                                                                                   |
| Is it optimised for performance?                                                             | ✔️ CSS is ready to go before user visits the page. | See the [JIT section](https://beyondco.de/blog/tailwind-jit-compiler-via-cdn) for more details on caching to optimise performance.                                                                                                                                   |

In the end, it depends on your preference.

If you use the Siteglide-CLI already to take advantage of modern code editing tools, you'll be right at home with Tailwind CLI. [Using the Tailwind CLI with Siteglide](https://www.sitegurus.io/documentation/sitebuilder/libraries\_and\_frameworks/using\_the\_tailwind\_cli\_with\_siteglide)

If you already work in the Siteglide Admin to keep everything in one place, you'll possibly find JIT compilation more convenient. [Tailwind's JIT Compiler Via CDN](https://www.sitegurus.io/documentation/sitebuilder/libraries\_and\_frameworks/tailwinds\_jit\_compiler\_via\_cdn)
