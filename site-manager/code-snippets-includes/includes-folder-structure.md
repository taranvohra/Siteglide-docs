# 🌳 Includes File Structure

## File Structure

Files in the includes folder must be named with a unique number which matches the ID in their Yaml.&#x20;

See the documentation for specific features to see where their layouts sit within the layouts folder. Code Editor in the Siteglide Admin normally starts its folder structure view at "layouts".&#x20;

```plaintext
marketplace_builder/
├── views/
│   └── partials/
│       ├── includes/
│       │   └── code_snippets/
│       │   │   └── 1.liquid
│       │   ├── content_sections/
│       │   │   └── 1.liquid
│       │   ├── headers/
│       │   └── footers/
│       └── layouts
```

When using the "include" tag to include a partial Liquid file, the path should always start relative to the partials folder and it should not include the .liquid extension, as this is assumed.&#x20;
