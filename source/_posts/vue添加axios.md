---
title: vue添加axios
date: 2017-09-02 16:26:46
tags: Vue之搭建自己的博客
---
vue中引入axios;
>npm install axios --save 安装成功后在 main.js里引入;
 
<pre><code>
  	import Vue from 'vue'
    import App from './App'
    import axios from 'axios';   //引入 
    import router from './router'
    import $ from 'jquery'
    import 'bootstrap/js/bootstrap.min.js'
    import 'bootstrap/css/bootstrap.min.css'
    
    Vue.config.productionTip = false
    Vue.prototype.$ajax = axios   //给vue添加$ajax 
    
    /* eslint-disable no-new */
    new Vue({
      el: '#app',
      router,
      template: '<App/>',
      components: { App }
    })
    // 添加一个响应拦截器  过滤掉一些不需要的信息
    axios.interceptors.response.use(function (response) {
    
      return response.data;
    }, function (error) {
    
      return Promise.reject(error);
    });;
    

  		
</code></pre>
>然后就可以这么使用了 

 <pre><code>
    getUser(){
        var that=this;
        this.$ajax.get('/api/user',{
        })
        this.$ajax.get('/api/findArticleLenght',{})
          .then(function(data){
            console.log(data);
            var obj=data.data[0];
  
            that.content=obj.text;
            that.name=obj.name;
            that.imgUrl=obj.url;
          })
          .catch(function(err){
  //          console.log(err);
          });
  
      }
 </code></pre>
