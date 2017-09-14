---
title: endsWith startsWith(转记录)
date: 2017-09-14 17:10:01
tags: javaScript
---
老大分享的一遍文章上看到的;觉得挺好的，就记下来，(*^__^*) 嘻嘻。
在操作字符串（String）类型的时候，startsWith(anotherString)和endsWith(anotherString)是非常好用的方法。其中startsWith判断当前字符串是否以anotherString作为开头，而endsWith则是判断是否作为结尾。举例：


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
   
   
   if (typeof String.prototype.endsWith != 'function') {
    String.prototype.endsWith = function(suffix) {
     return this.indexOf(suffix, this.length - suffix.length) !== -1;
    };
   }
</code></pre>


<pre><code>
 if (typeof String.prototype.startsWith != 'function') {
  String.prototype.startsWith = function (prefix){
   return this.slice(0, prefix.length) === prefix;
  };
 }
</code></pre>