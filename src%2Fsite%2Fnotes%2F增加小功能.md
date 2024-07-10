---
{"dg-publish":true,"permalink":"/增加小功能/","tags":["数字花园","功能"],"noteIcon":""}
---


就是[利用obsidian构建个人博客 (zytomorrow.top)](https://zytomorrow.top/%E6%8A%80%E6%9C%AF%E6%8A%98%E8%85%BE/%E5%88%A9%E7%94%A8obsidian%E6%9E%84%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/#github)教程结尾部分提到的，复制粘贴保留一下。

## 自定义

digtial garden目前提供了许多的插件项，可以根据官方文档自定义设置。

### 字体美化

目前中文字体个人最喜欢的是霞骛文楷，所以博客也要用上。  
在github库 `/src/site/_includes/components/user/common/head` 路径下，新建font.njk文件（文件名随意），内容如下：

```html
<link rel="stylesheet" href="https://cdn.staticfile.org/lxgw-wenkai-screen-webfont/1.6.0/style.css" />
```

在github库 `/src/site/styles/user/` 路径下，新建font.scss文件（文件名随意），内容如下：

```scss
body {
--font-default: "LXGW WenKai Screen", sans-serif;
}
```

以上，即完成了字体美化工作。

### 增加评论系统

一个博客没有评论系统那就不完美了，所以自己也需要加上评论，我目前采用的是自建WALINE，比其他的评论系统都快，主要是可以自维护，免去审查。

在github库 `/site/_includes/components/user/common/footer/` 路径下，新建comment.njk文件（文件名随意），内容如下：

```html
<hr class="content">
<div class="content" id="waline"></div>
<link rel="stylesheet" href="https://unpkg.com/@waline/client@v2/dist/waline.css"/>
<script type="module">
import { init } from 'https://unpkg.com/@waline/client@v2/dist/waline.mjs';
init({
el: '#waline',
serverURL: 'https://comment.zytomorrow.top',
});
</script>
```

以上，即完成了评论系统的设置。

### 增加网站、文件访问统计

虽然没啥用，但是喜欢这个功能，所以还是加上了。

在github库 `/src/site/_includes/components/user/common/footer/` 路径下，新建comment.njk文件（没错，和上面同一个文件，可以合并到一起），内容如下：

```html
<hr class="content">
<div class="content" id="waline"></div>
<link rel="stylesheet" href="https://unpkg.com/@waline/client@v2/dist/waline.css"/>
    <script type="module">
        import { init } from 'https://unpkg.com/@waline/client@v2/dist/waline.mjs';
        init({
            el: '#waline',
            serverURL: 'https://comment.zytomorrow.top',
            });
</script>
<hr>
<div class="content" align="center">
<div class="content">2017–2023 ZyTomorrow</div>
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>
</div>

```

在github库 `/src/site/_includes/components/user/notes/header/` 路径下，新建busuanzi.njk文件（文件名随意），内容如下：

```html
<hr>
    <div align="center">
        <span id="busuanzi_container_page_pv">本文总阅读量<span id="busuanzi_value_page_pv"></span>次</span>
    </div>
<hr>
```

以上，即可完成统计计数。

总的来收，根据个人需要可以完成各式各样的定制，并且难度都不高。可以[参考文档](https://dg-docs.ole.dev/).
