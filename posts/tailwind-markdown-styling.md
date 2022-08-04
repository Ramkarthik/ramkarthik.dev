---
title: Style Markdown with Tailwind CSS
description: The quick and easy steps to style markdown content using Tailwind CSS
date: 2022-08-04
tags:
  - tailwind
layout: layouts/post.njk
---
1. Install @tailwindcss/typography from the project directory

```
npm install @tailwindcss/typography
```

2. Add the plugin to the Tailwind config

```
// tailwind.config.js
module.exports = {
  content: [
    // ...   
  ],
  theme: {
    // ...
  },
  plugins: [
    require('@tailwindcss/typography'),
    // ...
  ],
}
```

3. Wrap the HTML content generated by markdown using the `prose` class

```
<div class="prose">
	// HTML generated by markdown
</div>
```

4. To further configure the styling, use the extend option in the Tailwind config file

```
module.exports: {
  theme: {
    extend: {
      typography: {
        excerpt: {
          css: {
            p: {
              fontFamily: `${theme('fontFamily.display')}`,
              fontSize: theme('fontSize.2xl'),
              lineHeight: theme('lineHeight.8'),
            }
          }
        },
      },
    },
  },
}
```