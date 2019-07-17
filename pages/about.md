---
layout: page
title: About
description: 自律给我自由
keywords: 李玉祥
comments: true
menu: 关于
permalink: /about/
---

我是李玉祥，程序猿一枚。

仰慕「优雅编码的艺术」。

向往「随遇而安，平心静气」。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
