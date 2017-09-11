---
title: watch解决Propertychange
date: 2017-09-11 15:52:17
tags: Vue之搭建自己的博客
---
在写一个实时搜索的input时，发现change事件必须失焦才能触发，这样又达不到实时搜索的目的，网上查了下，watch监听数据源有没有变化
实现；

<pre><code>
  export default {
    name: 'app',
    data(){
      return{
          name:'1',
          imgUrl:'1',
          content:'1',
        articleLenght:'1',
        CategoryLenght:'',
        fileLength:'',
        search:""
      }
  
    },
    mounted(){
      this.getUser();
      this.getAriticle();
      this.getCategory();
      this.getLable();
    },
    watch:{
      "search"(curVal,oldVal){
        console.log(curVal,oldVal);
      },
  
    },}
  		
</code></pre>

又特地去网上查了下watch ；
Vue.js 提供了一个方法 watch，它用于观察Vue实例上的数据变动。对应一个对象，键是观察表达式，值是对应回调。值也可以是方法名，或者是对象，包含选项。具体的用法可以直接看下面的示例，简单直接。
>普通的watch
<pre><code>
  data() {
      return {
          frontPoints: 0    
      }
  },
  watch: {
      frontPoints(newValue, oldValue) {
          console.log(newValue)
      }
  }
</code></pre>
>数组的watch

<pre><code>
 data() {
     return {
         winChips: new Array(11).fill(0)   
     }
 },
 watch: {
 　　winChips: {
 　　　　handler(newValue, oldValue) {
 　　　　　　for (let i = 0; i < newValue.length; i++) {
 　　　　　　　　if (oldValue[i] != newValue[i]) {
 　　　　　　　　　　console.log(newValue)
 　　　　　　　　}
 　　　　　　}
 　　　　},
 　　　　deep: true
 　　}
 }
</code></pre>
>对象的watchtips: 只要bet中的属性发生变化（可被监测到的），便会执行handler函数；
<pre><code>
data() {
　　return {
　　　　bet: {
　　　　　　pokerState: 53,
　　　　　　pokerHistory: 'local'
　　　　}   
    }
},
watch: {
　　bet: {
　　　　handler(newValue, oldValue) {
　　　　　　console.log(newValue)
　　　　},
　　　　deep: true
　　}
}
</code></pre>

>   如果想监测具体的属性变化，如pokerHistory变化时，才执行handler函数，则可以利用计算属性computed做中间层。
事例如下：
<pre><code>
data() {
　　return {
　　　　bet: {
　　　　　　pokerState: 53,
　　　　　　pokerHistory: 'local'
　　　　}   
    }
},
computed: {
　　pokerHistory() {
　　　　return this.bet.pokerHistory
　　}
},
watch: {
　　pokerHistory(newValue, oldValue) {
　　　　console.log(newValue)
　　}
}
</code></pre>
或者是这样
<pre><code>
data() {
　　return {
　　　　bet: {
　　　　　　pokerState: 53,
　　　　　　pokerHistory: 'local'
　　　　}   
    }
},
watch: {
　　bet.pokerHistory(newValue, oldValue) {
　　　　console.log(newValue)
　　}
}
</code></pre>
          
