---
title: Js缓存的解决方案
date: 2017-09-13 20:42:13
tags: javaScript
---
解决js缓存问题;工作中遇到这个问题，网上查阅的方法就是加版本号和时间戳;生产环境使用版本号;开发环境使用时间戳；
恰好同事写了一个解决js缓存的方法，借鉴了一下,自己写了一个；
<pre><code>
  if (!String.prototype.endsWith) //给String添加ensWith方法
      String.prototype.endsWith = function(searchStr, Position) {
          if (!(Position < this.length))
              Position = this.length;
          else
              Position |= 0; // round position
          return this.substr(Position - searchStr.length,
                  searchStr.length) === searchStr;
      };
      
      
  function Loader(obj) {  
      this.VERSION=obj.VERSION;   //版本号
      this.isDevelopment=obj.isDevelopment;  //是否是开发环境
      this.files=obj.files?obj.files:[];   //公共JS CSS；
      this.parameters=this.getParameters(); //时间戳和版本号 ；
      this.loadMeta();头部Meta设置
  }
  //返回参数
  Loader.prototype.getParameters=function () {
      var parameters="?_v"+(this.isDevelopment?this.VERSION+"&_t="+new Date().getTime(): this.VERSION);
      return parameters;
  }
  //;头部Meta设置
  Loader.prototype.loadMeta=function () {
      document.write('<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no"/>');
      document.write('<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>');
      document.write('<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>');
      document.write('<meta http-equiv="Cache-Control" content="no-cache,no-store, must-revalidate"/>');
      document.write('<meta http-equiv="Pragma" content="no-cache"/>');
      document.write('<meta http-equiv="Expires" content="0"/>');
      document.write('<link rel="shortcut icon" href="/static/images/common/favicon.ico" type="image/x-icon"/>');
  }
  //判断是JS还是CSS
  Loader.prototype.type=function (file) {
      var type;
  
      if(file.endsWith('.CSS')||file.endsWith('.css')){
          type="css";
      }
      else if(file.endsWith('.JS')||file.endsWith('.js')){
          type="js";
      }
      else {
          type=null
      }
      return type;
  }
  //添加私有模块的JS CSS
  Loader.prototype.addFiles=function (files) {
  
      this.files=this.files.concat(files);
  }
  //加载JS CSS
  Loader.prototype.loadfile=function () {
      var arr=this.files;
      var len=arr.length;
      for(var i=0;i<len;i++){
          var file=arr[i];
          var type=this.type(file);
          var ele;
          switch(type)
          {
              case "css":
                  ele='<link type="text/css" rel="stylesheet" href="'+file+this.parameters+'"/>';
                  break;
              case "js":
                  ele='<script type="text/javascript" src="'+file+this.parameters+'" charset="UTF-8"></script>'
                  break;
              default:
                  break
          }
          document.write(ele);
      }
  }
</code></pre>
运用方法
<pre>
<code>

var a=new Loader({
    VERSION:1,
    isDevelopment:true,
    files:[
        "app.js",
        "app.js",
        "app.js",
        "app.js",
        "app.js",
    ]

})
</code>
</pre>

