---
title: this
date: 2017-09-01 11:28:43
tags: javaScript
---
>JavaScript的 this 总是指向一个对象，而具体指向哪个对象是在
 运行时基于函数的执行环境动态绑定的，而非函数被声明时的环境。
>this指向大致可以分以下4种

>1:作为对象的方法调用。

>2:作为普通函数调用。

>3:构造器调用。

>4:Function.prototype.call 或 Function.prototype.apply 调用。

1,当函数作为对象的方法被调用时， this 指向该对象：

<pre><code>
   ar obj = {
   a: 1,
   getA: function(){
   alert ( this.a ); // 输出: 1
   };
   obj.getA();
</code></pre>

2,作为普通函数调用当函数不作为对象的属性被调用时，也就是我们常说的普通函数方式，此时的 this 总是指
         向全局对象。在浏览器的 JavaScript里，这个全局对象是 window 对象。


<pre><code>
 window.name = 'globalName';
 var getName = function(){
 return this.name;
 };
 console.log( getName() ); // 输出：globalName
 
 window.name = 'globalName';
 var myObject = {
 name: 'sven',
 getName: function(){
 return this.name;
 }
 };
 var getName = myObject.getName;
 console.log( getName() ); // globalName
 
</code></pre>

3.构造器调用 通常情况下，构造器里的 this 就指向返回的这个对象。

<pre><code>
  var MyClass = function(){
  this.name = 'sven';
  };
  var obj = new MyClass();
  alert ( obj.name ); // 输出：sven
</code></pre>

>如果构造器显式地返回了一个 object 类型的对
 象，那么此次运算结果最终会返回这个对象，而不是我们之前期待的 this，而是返回的对象
 
 <pre><code>
  var MyClass = function(){
  this.name = 'sven';
  return { // 显式地返回一个对象
  name: 'anne'
  }
  };
  var obj = new MyClass();
  alert ( obj.name ); // 输出：anne
 </code></pre>

4.Function.prototype.call 或 Function.prototype.apply 调用
跟普通的函数调用相比，用 Function.prototype.call 或 Function.prototype.apply 可以动态地
改变传入函数的 this ：

 <pre><code>
  var obj1 = {
  name: 'sven',
  getName: function(){
  return this.name;
  }
  };
  var obj2 = {
  name: 'anne'
  };
  console.log( obj1.getName() ); // 输出: sven
  console.log( obj1.getName.call( obj2 ) ); // 输出：anne
 </code></pre>
