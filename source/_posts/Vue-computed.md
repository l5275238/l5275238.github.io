---
title: Vue computed
date: 2017-09-07 15:29:04
tags: Vue
---
Vue computed的理解;今天写了分页中 看到别人的例子里用到 computed，后来查了发现
computed相当于属性的一个实时计算，如果实时计算里关联了对象，那么
当对象的某个值改变的时候，会出发实时计算。以下是代码;
 <pre><code>
  computed: {
      page: function () { // 总页数
        return Math.ceil(this.total / this.display);
      },
      grouplist: function () { // 获取分页页码
        var len = this.page, temp = [], list = [], count = Math.floor(this.pagegroup / 2), center = this.current;
        if (len <= this.pagegroup) {
          while (len--) {
            temp.push(this.page - len);
          }
          ;
          return temp;
        }
        else {
          while (len--) {
            temp.push(this.page - len);
          }
          var index=temp.indexOf(center);
          if(index<=count){
              var deleIndex=this.page-this.pagegroup;
             temp.splice(4,deleIndex,"...");
          }
          else {
            if(index<=this.page-3){
                var deleIndex1=index-1-1;
                var deleIndex2=(this.page-3-index)>0?(this.page-3-index):0;
              temp.splice(1,deleIndex1,"...");
              if(deleIndex2>0){
                temp.splice(index+2 ,deleIndex2,"...");
              }

            }
            else {
                var deleIndex=this.page-this.pagegroup;
              temp.splice(-4,deleIndex,'...')
            }
          }
          return temp;
        }

      }
    },
    methods: {
      next: function (idx) {
       if(idx>0&&idx<=this.page){
         this.current=idx;
       }
      }
    }
 </code></pre>
 
 >当你调用next()函数时 改变了 current此时 grouplist会重新计算;