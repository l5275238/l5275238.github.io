---
title: vuex store
date: 2017-11-13 14:54:58
tags: Vue
---
Vuex 理解；官网上说 Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化个人理解的Vuex相当于一个全局变量的一个管理，所有的子页面都可以取到；
你可以理解整个store 是个对象;而state是这个这个对象的属性; 这里我写了这个 name属性；
<pre><code>
  import vue from 'vue';
  import vuex from 'vuex';
  vue.use(vuex);
  const store=new vuex.Store({
    state:{
     name:'你好',

    },
    mutations:{
      setName(state,n){

          state.name=n;

      }
    },
    actions: {
      setName ({ commit },n) {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            commit('setName',n);
            resolve()
          }, 1000)
        })
      }
    },

    getters:{
      getName:function (state) {
        return state.name
      }
    }

  })
  export default store;
</code></pre>
getters  相当于一个读取的方法  你可以读取里面的数据 进行筛选 但是不能操作state; 页面引用
<pre><code>
    getters:{
         getName:function (state) {
           return state.name
         }
       }
</code></pre>

<pre><code>
   mounted(){
        console.log(this.$store.getters.getName); //‘你好’
  }
</code></pre>

mutations 相当于设置和更改 state；
<pre><code>
    mutations:{
         setName(state,n){

             state.name=n;

         }
       },
</code></pre>

<pre><code>
   mounted(){
   this.$store.commit('setName','哈哈');
        console.log(this.$store.getters.getName); //‘哈哈’
  }
</code></pre>
actions 对比mutations 个人觉得他是重新包装处理了，最直白的就是他的异步处理 提供了异步的回调；
<pre><code>
    mutations:{
         setName(state,n){

             state.name=n;

         }
       },
</code></pre>

<pre><code>
    actions: {
      setName ({ commit },n) {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            commit('setName',n);
            resolve()
          }, 1000)
        })
      }
    },
</code></pre>
<pre><code>
      mounted(){
        this.$store.dispatch('setName','嘻嘻').then(() => {
          console.log(this.$store.getters.getName); //嘻嘻
        })
      },
</code></pre>

Module 大家看官网应该也可以明白;
<pre><code>
  const moduleA = {
    state: { ... },
    mutations: { ... },
    actions: { ... },
    getters: { ... }
  }

  const moduleB = {
    state: { ... },
    mutations: { ... },
    actions: { ... }
  }

  const store = new Vuex.Store({
    modules: {
      a: moduleA,
      b: moduleB
    }
  })

</code></pre>
你可以每个模块写到 对应的JS里
<pre><code>
 import moduleA from "./../store/modules/moduleA";
 import moduleB from "./../store/modules/moduleB";
 const  vuex_store = new Vuex.Store({
     modules:{
         users:moduleA,
         news:moduleB
     }
 })

</code></pre>



