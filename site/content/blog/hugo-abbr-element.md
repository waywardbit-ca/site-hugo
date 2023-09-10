---
title: "How to use abbreviation element in Hugo?"
date: 2023-08-09T18:06:00-04:00
draft: false
tags: [Hugo, Shortcode, Markdown, abbr, HTML]
---
The problem of being unable to use {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} markup in [Markdown](https://www.markdownguide.org/) files is a common frustration when seeking a balance between the simplicity of [Markdown](https://www.markdownguide.org/)'s plain-text formatting and the flexibility of {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}}'s rich content structure. [Markdown](https://www.markdownguide.org/) is favored for its ease of use and readability, but it lacks the finer control and customizability of {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}}. When {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} markup is disallowed or improperly parsed within [Markdown](https://www.markdownguide.org/), it restricts from incorporating advanced formatting, multimedia elements, or specific styling choices, forcing a compromise on design and functionality.

<!--more--> 

[Hugo](https://gohugo.io/) [shortcodes](https://gohugo.io/content-management/shortcodes/) are essential for handling {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} limitations in [Markdown](https://www.markdownguide.org/) because they provide a powerful and flexible way to seamlessly integrate {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} code and custom functionalities within [Markdown](https://www.markdownguide.org/) documents. [Shortcodes](https://gohugo.io/content-management/shortcodes/) act as a bridge, allowing users to inject {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} or other dynamic content into [Markdown](https://www.markdownguide.org/) without compromising its ease of use maintaining the core benefits of [Markdown](https://www.markdownguide.org/)'s simplicity and portability.  This makes [Hugo](https://gohugo.io/) [shortcodes](https://gohugo.io/content-management/shortcodes/) a valuable tool for web developers seeking to enhance the functionality and aesthetics of their content.

By default, [Hugo](https://gohugo.io/) is designed to omit {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} that is written into the [Markdown](https://www.markdownguide.org/) file.  For example, writing an {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} abbreviation tag into the file will not result in the expected output.

| [Markdown](https://www.markdownguide.org/) Content | Expected Result | Actual Result |
|---|---|---|
| `<abbr title="hypertext markup language">HTML</abbr>` | {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} | HTML |

Investigating the rendered markup in the web browser reveals what is happening behind the scene:

{{< code lang="html" >}}<!-- raw HTML omitted -->
HTML
<!-- raw HTML omitted -->{{< /code >}}

This output is a result of the {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} supression that is working to reduce the injection of harmful markup into the rendered webpage.  This is, in general, a good feature however it is restricting the usage of the `abbr` tag in the output which has value to clarify the definition of accronyms.  To provide a work around to this a [shortcode](https://gohugo.io/content-management/shortcodes/) may be used to define the content of the {{< abbr title="hypertext markup langugage" >}}HTML{{< /abbr >}} desired.

In the `layouts` folder of the theme being used in the [Hugo](https://gohugo.io/) site, a folder called `shortcodes` needs to be created to hold the new [shortcode](https://gohugo.io/content-management/shortcodes/) for our abbreviation tag.

{{< code lang="cmd" >}}/<site name>/layouts/shortcodes   
{{< /code >}}

Within the folder, create a file called `abbr.html` which will be used to put the markup that will be used when the [shortcode](https://gohugo.io/content-management/shortcodes/) is referenced in [Markdown](https://www.markdownguide.org/).  Within the file will be the markup to render when the shortcode is used.

{{< code lang="html" >}}<abbr title='{{ .Get "title" }}'>{{ .Inner }}</abbr>{{< /code >}}

This [shortcode](https://gohugo.io/content-management/shortcodes/) utilizes a parameter called title, leveraged by the `.Get` function, to get the value of title supplied in the [Markdown](https://www.markdownguide.org/) and injects it into the attribute on the `abbr` element.  Meanwhile the inner HTML of the `abbr` element will be provided by the content supplied into the shortcode's inner content and retrieved by the `.Inner` property.

With this [shortcode](https://gohugo.io/content-management/shortcodes/) having been configured, the `abbr` element may be used in the [Markdown](https://www.markdownguide.org/) file with the following [shortcode](https://gohugo.io/content-management/shortcodes/) syntax:

{{< code lang="md" >}}{{</* abbr title="hypertext markup language" */>}}HTML{{</* /abbr */>}}{{< /code >}}

With this capability unlocked the ability to leverage this [shortcode](https://gohugo.io/content-management/shortcodes/) expands the accessibility of the site while still enjoying the simplicity and readability of [Markdown](https://www.markdownguide.org/).