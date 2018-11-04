---
title: Auto-resize Shiny Apps in iframes
author: Paul Campbell
date: '2018-03-14'
slug: auto-resize-shiny-apps-in-iframes
categories:
  - Shiny
tags: []
draft: true
---

Add this to your shiny app `UI`:

```{r}
tags$head(
      tags$script(src="https://cdnjs.cloudflare.com/ajax/libs/iframe-resizer/3.5.16/iframeResizer.contentWindow.min.js",
                  type="text/javascript")
      ),
```

Add this to the parent HTML page you are embedding the shiny app in:

```{html}
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/iframe-resizer/3.5.16/iframeResizer.min.js"></script>
<style>
  iframe {
    width: 1px;
    min-width: 100%;
  }
</style>
<iframe id="myIframe" src="YOUR_SHINYAPP_URL" scrolling="no" frameborder="no"></iframe>
<script>
  iFrameResize({
    log:true,
    inPageLinks:true,
    heightCalculationMethod: 'lowestElement'
  });
</script>
```

Example (try resizing the browser):

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/iframe-resizer/3.5.16/iframeResizer.min.js"></script>
<style>
  iframe {
    width: 1px;
    min-width: 100%;
  }
</style>
<iframe id="myIframe" src="https://cultureofinsight.shinyapps.io/module_example/" scrolling="no" frameborder="no"></iframe>
<script>
  iFrameResize({
    log:true,
    inPageLinks:true,
    heightCalculationMethod: 'documentElementScroll'
  });
</script>

There's a slight glitch in that if you force an increase in iframe height by narrowing the browser but then widen it again, the iframe height remains at the longer length despite the all the elements in the app returning to 1 row. If anyone knows how to fix this, let me know!

P.