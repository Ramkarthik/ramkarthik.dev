---
title: Installing Tailwind CSS on .NET Core MVC/Razor
description: Quick step-by-step tutorial on installing Tailwind on .NET Core MVC/Razor.
date: 2022-07-26
tags:
  - dotnet
  - tailwind
layout: layouts/post.njk
---

1. Go to the web project directory

2. Run the following command which will create a package.json file
```
npm init -y
```

3. Install Tailwind
```
npm install -D tailwindcss
```

4. Add the build script to package.json. This will generate the Tailwind CSS output at `/www/css/styles.css` location.
```
"scripts": {
    "css:build": "npx tailwindcss -i ./wwwroot/css/site.css -o ./wwwroot/css/styles.css --minify"
  }
```

5. Generate Tailwind config file (tailwind.config.js) by running the command
```
npx tailwindcss init
```

6. Add the files pattern to the 'content' section of the tailwind.config.js file (note: `./Pages/**/*.cshtml` is for Razor and `./Views/**/*.cshtml` is for MVC)

```
module.exports = {
    content: [
       './Pages/**/*.cshtml',
       './Views/**/*.cshtml'
],
    theme: {
        extend: {},
    },
    plugins: [],
}
```

7. Create `site.css` file under `/wwwroot/css` folder with the following imports
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

8. Edit the web `.csproj` file to ensure that the Tailwind CSS build script is run during build/deploy
```
<ItemGroup>
  <UpToDateCheckBuilt Include="wwwroot/css/site.css" Set="Css" />
  <UpToDateCheckBuilt Include="tailwind.config.js" Set="Css" />
</ItemGroup>

<Target Name="Tailwind" BeforeTargets="Build">
  <Exec Command="npm run css:build"/>
</Target>
```

9. Include the path to the CSS file in the layout file
```
<link rel="stylesheet" href="~/css/styles.css" asp-append-version="true" />
```

That's it!