---
title: Vue 分页组件
date: 2017-09-07 16:09:19
tags: Vue之搭建自己的博客
---
因为文章前台显示要用到分页，为了一个分页引入一个Ui框架又觉得不划算；所以就自己写了一个分页组件也是借鉴了网上别人demo；
下面是代码
 <pre><code>
 &lt;template&gt
   &lt;div id="app"&gt
     &lt;ul class="pagination"&gt
       &lt;li&gt&lt;a href="javascript:void(0)" @click="next(current-1)" :class="{'disabled':page==1}"&gt&laquo;&lt;/a&gt&lt;/li&gt
       &lt;li v-for="p in grouplist"  @click="next(p)"&gt&lt;a :class="{'active':current==p }" href="javascript:void(0)"&gt {{ p }}&lt;/a&gt&lt;/li&gt
       &lt;li&gt&lt;a href="javascript:void(0)" @click="next(current+1)" :class="{'disabled':page==1}"&gt&raquo;&lt;/a&gt&lt;/li&gt
     &lt;/ul&gt
   &lt;/div&gt
 &lt;/template&gt
 
 &lt;script&gt
 
   export default {
     data(){
       return {
         current: this.currentPage
       }
     },
     props: {       //props 把数据传给子组件 以下属性是组件数据的一个字段，期望从父作用域传下来。子组件需要显式地用 props 选项 声明
       total: {// 数据总条数
         type: Number, //数据类型 验证
         default: 0  //默认值
       },
       showPage: {// 每页显示条数
         type: Number,
         default: 10
       },
       currentPage: {// 当前页码
         type: Number,
         default: 1
       },
       pagegroup: {// 分页条数
         type: Number,
         default: 5,
         coerce: function (v) {     //  验证 将数据处理在返回 如果是偶数则+1
           v = v &gt 0 ? v : 5;
           return v % 2 === 1 ? v : v + 1;
         }
       }
     },
     computed: {
       page: function () { // 总页数
         return Math.ceil(this.total / this.showPage);
       },
       grouplist: function () { // 获取分页页码
         var len = this.page, temp = [], list = [], count = Math.floor(this.pagegroup / 2)+1, center =this.current; var pagegroup=this.pagegroup-1;
         if (len &lt;= this.pagegroup) {
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
           if(index&lt;=count){
               var deleIndex=this.page-this.pagegroup;
              temp.splice(pagegroup,deleIndex,"...");
           }
           else {
             if(index&lt;=this.page-count){
                 var deleIndex1=index-1-1;
                 var deleIndex2=(this.page-count-index)&gt0?(this.page-count-index):0;
               if(deleIndex2&gt0){
                 temp.splice(index+count-1 ,deleIndex2,"...");
               }
               temp.splice(1,deleIndex1,"...");
 
 
             }
             else {
                 var deleIndex=this.page-this.pagegroup;
               temp.splice(-pagegroup,deleIndex,'...')
             }
           }
           return temp;
         }
 
       }
     },
     methods: {
       next: function (idx) {
        if(idx&gt0&&idx&lt;=this.page){
          this.current=idx;
          this.$emit('pagechange', this.current);
        }
       }
     }
 
   }
 &lt;/script&gt
 
 
 &lt;style&gt
   .pagination&gtli&gt.active{
     background: #dddddd!important;
   }
   .pagination&gtli&gta:focus, .pagination&gtli&gta:hover, .pagination&gtli&gtspan:focus, .pagination&gtli&gtspan:hover{
     background: none;
   }
   .disabled{
     cursor: not-allowed;
   }
 
 &lt;/style&gt

 </code></pre>
 以上是组件代码 然后 在main.js注册组件即可
  <pre><code>
import pagination from '@/components/pagination'  //引入组件


Vue.component('pagination',pagination)  //注册

  </code></pre>
  
  页面调用
  <pre><code>
 &lt;pagination :total="total" :current-page='current' @pagechange="pagechange"&gt&lt;/pagination&gt
  export default {
     name: 'hello',
     data () {
       return {
         msg: 'Welcome to Your Vue.js App',
         articleList:[],
         articleLenght:'',
         total: 150,     // 记录总条数
         showPage: 10,   // 每页显示条数
         current: 1,   // 当前的页数
         row:1,
       }
 
     },
      methods:{
           pagechange:function (val) {
            this.row=val;
             getListAritic();
     
           },}
     }

  </code></pre>