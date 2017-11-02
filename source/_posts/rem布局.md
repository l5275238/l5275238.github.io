---
title: rem布局
date: 2017-10-30 18:02:38
tags: 移动端
---
rem布局的实现
CSS 通过媒体查询设置font-size大小 实现方法

<pre>
<code>
html {
    font-size : 20px;
}
@media only screen and (min-width: 401px){
    html {
        font-size: 25px !important;
    }
}
@media only screen and (min-width: 428px){
    html {
        font-size: 26.75px !important;
    }
}
@media only screen and (min-width: 481px){
    html {
        font-size: 30px !important;
    }
}
@media only screen and (min-width: 569px){
    html {
        font-size: 35px !important;
    }
}
@media only screen and (min-width: 641px){
    html {
        font-size: 40px !important;
    }
}
</code>
</pre>
font-size:40px,此时1rem=40px；CSS就是通过媒体查询动态的控制font-size的大小也是1rem的实际大小，让页面进行适当缩放;
也可以用js进行设置rem 如果你的ui设计图为640 ; 你可以在按下面Js操作也就是你在640宽的时候为100px; 假设你的div为100px标注为1rem即可；
如果屏幕缩小了 你 div也会缩小到50px 但是你实际写CSS里的只有1rem！
<pre>
<code>
(function (doc, win) {
        var docEl = doc.documentElement,
            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
            recalc = function () {
                var clientWidth = docEl.clientWidth;
                if (!clientWidth) return;
                if(clientWidth>=640){
                    docEl.style.fontSize = '100px';
                }else{
                    docEl.style.fontSize = 100 * (clientWidth / 640) + 'px';
                }
            };

        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);
        doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);

</code>
</pre>
