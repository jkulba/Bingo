# Bingo
.NET Blazor WAS Pwa &amp; RESTful Services


## pre-requisites

- wasm-tools
```shell
dotnet workload install wasm-tools
```

## Blazor configuration for hosting under a subpath (/bingo)

(1) Set the `<base href>` in wwwroot/index.html
```html
<base href="/bingo/">
```
_Make sure to include the trailing '/'._

(2) Configure the PWA service worker (if using)

Blazor PWA apps use a service-worker.published.js file that also must respect the base path.

In wwwroot/service-worker.published.js, modify asset paths accordingly or use the official workaround by ensuring you're publishing with a base path (see Step 3).

(3) Use the --base-path flag when publishing

```shell
dotnet publish -c Release -p:StaticWebAssetBasePath=/bingo
```

(4) Update csproj with AOTCompilation flag

```xml
  <PropertyGroup>
    <RunAOTCompilation>true</RunAOTCompilation>
  </PropertyGroup>
```

(5) Deploy to NGINX (mention only for context)

Place the contents of wwwroot (after publish) into the appropriate NGINX location (/var/www/html/myapp or similar).