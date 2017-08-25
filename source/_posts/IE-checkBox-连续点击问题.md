---
title: IE checkBox 连续点击问题
date: 2017-08-25 14:27:05
tags: IE CheckBox
---
>在 IE 你如果快速点击checkBox 会导致点击没有反应 解决方法

<pre><code>
  	$("input[type='checkbox']").attr('ondblclick', 'this.click()'); 	
</code></pre>
