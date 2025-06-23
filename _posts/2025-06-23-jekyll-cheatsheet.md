---
title: "Jekyll cheatsheet"
categories:
  - Cheatsheet
tags:
  - Markdown
  - Jekyll
excerpt_separator: "<!--more-->"
toc: true
toc_sticky: true
---

This article is composed based default configuration of Minimal Theme (the one theme, used for this website, obviously).

<!--more-->

## Frontmatter

```md
---
title: "Title of this post"
last_modified_at: 2016-03-09T16:20:02-05:00 - can be skipped
categories: - list of categories for article
  - Blog
tags: - list of tags for article
  - Post Formats
  - readability
  - standard
excerpt_separator: "<!--more-->" - optional, separator

link: https://github.com - optional, link to some page

toc: true - optional, table of contents
toc_sticky: true - optional, sticky table of contents

---
```

## More

This post has a manual excerpt `<!--more-->` set after the first paragraph. The following YAML Front Matter has also to be applied:

```yaml
excerpt_separator: "<!--more-->"
```

## Tables

Tables are the same is in regular Markdown

| Item | Description | Price |
| --- | --- | ---: |
| item1 | item1 description | 1.00 |
| item2 | item2 description | 100.00 |


## Example of embedded JavaScript

<!-- Embedded DVD Bouncing Text -->
<div id="dvd-bounce-container" style="position:relative; width:100%; max-width:700px; height:200px; margin:2em auto; border-radius:16px; background:transparent;">
  <div id="dvd-window-embedded" style="
    position:absolute;
    left:40px; top:30px;
    width:120px; height:60px;
    color:#000;
    font-family:monospace; font-size:2em;
    display:flex; align-items:center; justify-content:center;
    user-select:none; pointer-events:none;
  ">DVD</div>
</div>
<script>
(function() {
  const container = document.getElementById('dvd-bounce-container');
  const dvd = document.getElementById('dvd-window-embedded');
  let x = 40, y = 30;
  let dx = 1, dy = 1;
  const w = 120, h = 60;
  function move() {
    const cw = container.clientWidth, ch = container.clientHeight;
    x += dx; y += dy;
    if (x <= 0 || x + w >= cw) dx = -dx;
    if (y <= 0 || y + h >= ch) dy = -dy;
    dvd.style.left = x + 'px';
    dvd.style.top = y + 'px';
    requestAnimationFrame(move);
  }
  move();
})();
</script>


## Notices

Notices are alternative to callouts (in Obsidian, for example).

When using Kramdown `{: .notice}` can be added after a sentence to assign the `.notice` to the `<p></p>` element.

**Changes in Service:** We just updated our [privacy policy](#) here to better service our customers. We recommend reviewing the changes.
{: .notice}

**Primary Notice:** Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. [Praesent libero](#). Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--primary}

**Info Notice:** Lorem ipsum dolor sit amet, [consectetur adipiscing elit](#). Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--info}

**Warning Notice:** Lorem ipsum dolor sit amet, consectetur adipiscing elit. [Integer nec odio](#). Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--warning}

**Danger Notice:** Lorem ipsum dolor sit amet, [consectetur adipiscing](#) elit. Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--danger}

**Success Notice:** Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at [nibh elementum](#) imperdiet.
{: .notice--success}

Want to wrap several paragraphs or other elements in a notice? Using Liquid to capture the content and then filter it with `markdownify` is a good way to go.

```html
{% raw %}{% capture notice-2 %}
#### New Site Features

* You can now have cover images on blog pages
* Drafts will now auto-save while writing
{% endcapture %}{% endraw %}

<div class="notice">{% raw %}{{ notice-2 | markdownify }}{% endraw %}</div>
```

{% capture notice-2 %}

### New Site Features

* You can now have cover images on blog pages
* Drafts will now auto-save while writing
{% endcapture %}

<div class="notice">
  {{ notice-2 | markdownify }}
</div>

## Quotes

> Only one thing is impossible for God: To find any sense in any copyright law on the planet.

> <cite><a href="http://www.brainyquote.com/quotes/quotes/m/marktwain163473.html">Mark Twain</a></cite>
