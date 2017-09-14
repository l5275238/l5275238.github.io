---
title: endsWith String类型扩展
date: 2017-09-14 17:10:01
tags: javaScript
---
老大分享的一遍文章上看到的;觉得挺好的，就记下来，(*^__^*) 嘻嘻。一个String的扩展判断是否结尾是另外一个字符串;
<pre><code>
 if (!String.prototype.endsWith)
   String.prototype.endsWith = function(searchStr, Position) {
       // This works much better than >= because
       // it compensates for NaN:
       if (!(Position < this.length))
         Position = this.length;
       else
         Position |= 0; // round position
       return this.substr(Position - searchStr.length,
                          searchStr.length) === searchStr;
   };
</code></pre>

跟lastIndexOf有点类似 lastIndexOf可以是判断 另外一个字符串的位置 从前往后