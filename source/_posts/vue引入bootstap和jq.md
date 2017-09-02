---
title: vue引入bootstap和jq
date: 2017-09-02 15:39:27
tags: Vue
---
看了下vue的ui框架很少有自适应的，自己写CSS又觉得麻烦,网上看了下方法把bootstrap和jq
>1,npm install jquery --save-dev 引入jq  打开package.json 看devDependencies里有没有JQ 有的话便是成功安装

 <pre><code>
 "devDependencies": {
     "autoprefixer": "^6.7.2",
     "babel-core": "^6.22.1",
     "babel-loader": "^6.2.10",
     "babel-plugin-transform-runtime": "^6.22.0",
     "babel-preset-env": "^1.3.2",
     "babel-preset-stage-2": "^6.22.0",
     "babel-register": "^6.22.0",
     "chalk": "^1.1.3",
     "connect-history-api-fallback": "^1.3.0",
     "copy-webpack-plugin": "^4.0.1",
     "css-loader": "^0.28.0",
     "eventsource-polyfill": "^0.9.6",
     "express": "^4.14.1",
     "extract-text-webpack-plugin": "^2.0.0",
     "file-loader": "^0.11.1",
     "friendly-errors-webpack-plugin": "^1.1.3",
     "html-webpack-plugin": "^2.28.0",
     "http-proxy-middleware": "^0.17.3",
     "jquery": "^3.2.1",   //在这里
     "jsonwebtoken": "^7.4.3",
     "opn": "^4.0.2",
     "optimize-css-assets-webpack-plugin": "^1.3.0",
     "ora": "^1.2.0",
     "rimraf": "^2.6.0",
     "semver": "^5.3.0",
     "shelljs": "^0.7.6",
     "url-loader": "^0.5.8",
     "vue-loader": "^12.1.0",
     "vue-style-loader": "^3.0.1",
     "vue-template-compiler": "^2.3.3",
     "webpack": "^2.6.1",
     "webpack-bundle-analyzer": "^2.2.1",
     "webpack-dev-middleware": "^1.10.0",
     "webpack-hot-middleware": "^2.18.0",
     "webpack-merge": "^4.1.0"
   },
 </code></pre>
 
>修改然后修改webpack.base.conf.js两个地方：

>1,加入var webpack = require("webpack")；
 <pre><code>
 var path = require('path')
 var utils = require('./utils')
 var config = require('../config')
 var vueLoaderConfig = require('./vue-loader.conf')
 var webpack = require("webpack")  //加入
 </code></pre>
>2,在module.exports的里面加入 在最面加入即可
 <pre><code>
  plugins: [
     new webpack.optimize.CommonsChunkPlugin('common.js'),
     new webpack.ProvidePlugin({
       jQuery: "jquery",
       $: "jquery"
     })
   ]
 </code></pre>
 >因为本人在安装的时候会报错，后面发现的 如果你的rules 有我注释的代码，请把他注释，否则会报错;因为这个一个貌似是校验的
  <pre><code>
   module: {
      rules: [
        // {
        //   test: /\.(js|vue)$/,
        //   loader: 'eslint-loader',
        //   enforce: 'pre',
        //   include: [resolve('src'), resolve('test')],
        //   options: {
        //     formatter: require('eslint-friendly-formatter')
        //   }
        // },
        {
          test: /\.vue$/,
          loader: 'vue-loader',
          options: vueLoaderConfig
        },
        {
          test: /\.js$/,
          loader: 'babel-loader',
          include: [resolve('src'), resolve('test')]
        },
        {
          test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
          loader: 'url-loader',
          options: {
            limit: 10000,
            name: utils.assetsPath('img/[name].[hash:7].[ext]')
          }
        },
        {
          test: /\.(mp4|webm|ogg|mp3|wav|flac|aac)(\?.*)?$/,
          loader: 'url-loader',
          options: {
            limit: 10000,
            name: utils.assetsPath('media/[name].[hash:7].[ext]')
          }
        },
        {
          test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
          loader: 'url-loader',
          options: {
            limit: 10000,
            name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
          }
        }
      ]
    },
  </code></pre>

>完成以上的 最后在main.js中加入import $ from 'jquery' 完成jQuery的引入。

<pre><code>
import Vue from 'vue'
import App from './App'
import axios from 'axios';
import router from './router'
import $ from 'jquery'
import 'bootstrap/js/bootstrap.min.js'
import 'bootstrap/css/bootstrap.min.css'
 </code></pre>
 
>再将bootstap放入assets目录下即可
![bootstap储存位置](http://ou94rogzn.bkt.clouddn.com/bootstap.png)