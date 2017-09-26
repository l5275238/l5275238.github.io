---
title: inputDisabled没有颜色的问题
date: 2017-09-26 15:17:10
tags:CSS
---
今天遇到一个问题 就是苹果电脑上 input  Disabled没有禁用的颜色 手动增加一个样式
<pre><code>
  textarea:disabled, 
  input:not([type]):disabled, 
  input[type="color"]:disabled,
  input[type="date"]:disabled,
  input[type="datetime" ]:disabled,
  input[type="datetime-local" ]:disabled,
  input[type="email" ]:disabled,
  input[type="month" ]:disabled, 
  input[type="password" ]:disabled, 
  input[type="number" ]:disabled, 
  input[type="search" ]:disabled,
  input[type="tel" ]:disabled,
  input[type="text" ]:disabled,
  input[type="time" ]:disabled, 
  input[type="url" ]:disabled, 
  input[type="week" ]:disabled {
      background: #Ebebe4;
  }

  		
</code></pre>