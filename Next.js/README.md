---
description: >-
  https://nextjs.org/docs/pages/building-your-application/upgrading/version-13#v13-summary
---

# Next 13

#### [v13 Summary](https://nextjs.org/docs/pages/building-your-application/upgrading/version-13#v13-summary) <a href="#v13-summary" id="v13-summary"></a>

* The [Supported Browsers](https://nextjs.org/docs/architecture/supported-browsers) have been changed to drop Internet Explorer and target modern browsers.
* The minimum Node.js version has been bumped from 12.22.0 to 14.18.0, since 12.x has reached end-of-life.
* The minimum React version has been bumped from 17.0.2 to 18.2.0.
* The `swcMinify` configuration property was changed from `false` to `true`. See [Next.js Compiler](https://nextjs.org/docs/architecture/nextjs-compiler) for more info.
* The `next/image` import was renamed to `next/legacy/image`. The `next/future/image` import was renamed to `next/image`. A [codemod is available](https://nextjs.org/docs/pages/building-your-application/upgrading/codemods#next-image-to-legacy-image) to safely and automatically rename your imports.
* The `next/link` child can no longer be `<a>`. Add the `legacyBehavior` prop to use the legacy behavior or remove the `<a>` to upgrade. A [codemod is available](https://nextjs.org/docs/pages/building-your-application/upgrading/codemods#new-link) to automatically upgrade your code.
* The `target` configuration property has been removed and superseded by [Output File Tracing](https://nextjs.org/docs/pages/api-reference/next-config-js/output).
