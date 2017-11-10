---
title: vue全局注册方法
date: 2017-11-10 10:11:04
tags: Vue之搭建自己的博客
---
Vue.js 插件应该暴露一个 install 方法。此方法在调用时，将 Vue 构造函数作为第一个参数传入，以及将一个可选的选项作为第二个参数传入;

<pre><code>
  export default{
    install:function(Vue,options)
    {
      var obj=Vue.prototype;
      obj.getData = function () {
        console.log('我是插件中的方法');
      }
      obj.url='/api/';

    }
  }
</code></pre>

入口函数引入
<pre><code>
 import util from './util' //你对应的js；
 Vue.use(util);
</code></pre>

