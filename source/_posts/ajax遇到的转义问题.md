---
title: ajax遇到的转义问题
date: 2017-09-21 11:30:15
tags: javaScript
---
工作中遇到一个问题 ajax 当遇到参数为&'#@的时候这是执行AJAX的时候就会出问题,因为所传的参数变了.网上查询
使用 escape(encodeURIComponent())进行转码即可

<pre><code>
var value='&';
var url='/api/xxxx/xxx?name='+escape(encodeURIComponent(value));
</code></pre>