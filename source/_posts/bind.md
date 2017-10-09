---
title: bind
date: 2017-09-28 16:08:15
tags:
---
<pre><code>
if (!Function.prototype.bind) {
Function.prototype.bind = function(oThis) {
if (typeof this !== "function") {
// 与 ECMAScript 5 最接近的
// 内部 IsCallable 函数
throw new TypeError(
"Function.prototype.bind - what is trying " +
"to be bound is not callable
);
}
var aArgs = Array.prototype.slice.call( arguments, 1 ),
fToBind = this,
fNOP = function(){},
fBound = function(){
return fToBind.apply(
(
this instanceof fNOP &&
oThis ? this : oThis
),
aArgs.concat(
Array.prototype.slice.call( arguments )
);
}
;
fNOP.prototype = this.prototype;
fBound.prototype = new fNOP();
return fBound;
};
}
</code></pre>