---
title: 'Ionic Standalone Javascript Overview'
sidebar_label: Overview
---

<head>
  <title>Ionic Standalone JavaScript Overview | Standalone Javascript Documentation</title>
  <meta
    name="description"
    content="Read this overview to learn how to incorporate Ionic in your Web Development projects, without installing any frameworks."
  />
</head>

import DocsCard from '@components/global/DocsCard';
import DocsCards from '@components/global/DocsCards';

`@ionic/core` brings the Ionic Experience to any project — no framework, no CLI.

## Ionic Framework CDN

Ionic Framework can be included from a CDN for quick testing in a [Plunker](https://plnkr.co/), [Codepen](https://codepen.io), or any other online code editor!

It's recommended to use [jsdelivr](https://www.jsdelivr.com/) to access the Framework from a CDN. To get the latest version, add the following inside the `<head>` element in an HTML file, or where external assets are included in the online code editor:

```html
<script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
<script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
```

 The CSS bundle will include all of the Ionic [Global Stylesheets](../layout/global-stylesheets).


## Using Components
To use Ionic Components, you can browse our [UI Components Library](../docs/components) and copy the `JavaScript` sample code. This code can then be modified for your purposes.