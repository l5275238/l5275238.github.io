---
title: IE 火狐 Select 样式问题
date: 2017-08-25 14:20:53
tags: CSS
---
> IE 火狐的SELECT 标签样式 丑陋的解决方案 

<pre><code>
  select  {
      -moz-appearance:none!important;
      -webkit-appearance:none!important;
      -ms-appearance:none!important;
      appearance: none!important;
      background-image: url("../../images/common/select.png")!important;
      background-repeat: no-repeat!important;
      background-position: calc(100% - 7px) 50%!important;
  
      border-radius:3px!important;
      /*padding:0!important;*/
  }
  select::-ms-expand {
      display: none;
  }
  		
</code></pre>


>IE只能兼容到IE10  IE10以下不行  background-image 后面的图片可以自己去找个小三角的图片就可以了实现的方法主要是清除默认的属性给标签设置背景图片