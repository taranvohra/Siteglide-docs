# 💻 Assets with CLI

### Deploying Assets

This will deploy assets all at once along with the entire code base. The -w flag is necessary to include assets.

```
siteglide-cli deploy env -w
```

### Syncing Assets

```
siteglide-cli sync env
```

Watches for changes in the assets folder and syncs changed files one by one. This is not always recommended for large files.&#x20;
