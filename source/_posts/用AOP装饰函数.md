---
title: 用AOP装饰函数 切面
date: 2017-09-25 15:45:14
tags: JavaScript
---
观书有感，看了JavaScript设计模式 装饰者模式这一篇; 看到个有用的函数;

<pre><code>
   Function.prototype.before = function( beforefn ){
   var __self = this; // 保存原函数的引用
   return function(){ // 返回包含了原函数和新函数的"代理"函数
   beforefn.apply( this, arguments ); // 执行新函数，且保证 this 不被劫持，新函数接受的参数
                                        // 也会被原封不动地传入原函数，新函数在原函数之前执行
   return __self.apply( this, arguments ); // 执行原函数并返回原函数的执行结果，
   // 并且保证 this 不被劫持
   }
   }
   Function.prototype.after = function( afterfn ){
   var __self = this;
   return function(){
   var ret = __self.apply( this, arguments );
   afterfn.apply( this, arguments );
   return ret;
   }
   };
</code></pre>
before扩展 
<pre><code>
   Function.prototype.before = function( beforefn ){
   var __self = this; 
   return function(){ 
   if(beforefn.apply( this, arguments )=="false")
   {   
    return
    }                                    
   return __self.apply( this, arguments ); 
  
   }
   }
 
</code></pre>


<pre><code>
  var before = function( fn, beforefn ){
  return function(){
  beforefn.apply( this, arguments );
  return fn.apply( this, arguments );
  }
  }
  var a = before(
  function(){alert (3)},
  function(){alert (2)}
  );
  a = before( a, function(){alert (1);} );
  a();
</code></pre>



