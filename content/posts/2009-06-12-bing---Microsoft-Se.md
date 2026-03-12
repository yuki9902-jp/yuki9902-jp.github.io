---
title: "bing - Microsoft Search Engine"
date: 2009-06-12T11:29:23+09:00
archives: ["2009-06"]

categories: ['COLUMN']
---

ようやく bing にこのサイトが掲載されました。

クローラーが毎日検索していたことを考えると、サイトの存在性のチェック、更新頻度のチェック、外部リンクのチェックなどを行い、期間と基準を満たしたときに掲載されるのでしょう。

サイト登録をしてからちょうど1週間で掲載です。

robots.txt
```
User-agent: *

SiteMap: http://your_site_URL/sitemap.xml

Disallow:

```

sitemap.xml (UTF-8)
```
&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;urlset

      xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"

      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

      xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9

            http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"&gt;

&lt;!-- created with Free Online Sitemap Generator www.xml-sitemaps.com --&gt;

&lt;url&gt;

  &lt;loc&gt;http://your_site_URL/&lt;/loc&gt;

  &lt;priority&gt;1.00&lt;/priority&gt;

  &lt;lastmod&gt;2009-06-05T00:51:04+00:00&lt;/lastmod&gt;

  &lt;changefreq&gt;hourly&lt;/changefreq&gt;

&lt;/url&gt;

&lt;url&gt;

 :

 :

&lt;/url&gt;

&lt;/urlset&gt;

```

設置した robots.txt と sitemap.xml のサンプルです。

登録した後は我慢して待つのみ。
