#### Vue-cli 3.0版本与2.X版本比较

##### 3.0版本创建的目录	 (vue create my-project)

![vue-cli3.0](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0.png?raw=true)

##### 2.X版本创建的目录  	 (创建命令 vue init webpack my-project)

![vue-cli2.x](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli2.x.png?raw=true)

#### 二者区别：主要是配置webpack的区别2.x版本里会帮你以webpack的模板创建好各类文件都有默认的参数，只需要改就行了。而3.0版本开始，目录结构相比2.0有很大的改变，之前的`build`和`config`文件夹没有了，如果要像以前那样配置`webpack`的参数，只需要在项目的根目录下新建`vue.config.js 文件`注意是根目录，不是`src`目录。



#### vue-cli 3 创建项目步骤：

![vue-cli-1](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0img/vue-cli-1.png?raw=true)

#### 第一个是默认模板；第二个是自定义选择；第一个会默认安装基本模板、选择第二个进入以下选择

![vue-cli-2](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0img/vue-cli-2.png?raw=true)

#### 方向键控制空格选择 Enter进入下一步

![vue-cli-3](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0img/vue-cli-3.png?raw=true)

#### 路由是否选择history模式否的话是哈希路由，选择css预处理器 sass和less

![vue-cli-4](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0img/vue-cli-4.png?raw=true)

#### 选择代码规范配置

![vue-cli-5](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0img/vue-cli-5.png?raw=true)

#### 选择保存时候进行代码检测，在后面也可以关闭检测

![vue-cli-6](https://github.com/PandoraSB0X/record/blob/master/note/img/vue-cli3.0img/vue-cli-6.png?raw=true)

#### 会保存在根目录下，然后会有一步是否保存本次配置，可以选择保存此次配置作为下次开发的模板。

#### vue-cli 3.x需要在根目录也就是与src同级的目录创建一个vue.config.js用来配置webpack，代理等参数。

```js
// vue.config.js 配置说明
// 这里只列一部分，具体配置惨考文档
module.exports = {
    // baseUrl  type:{string} default:'/'  从 Vue CLI 3.3 起已弃用，请使用publicPath
    // 将部署应用程序的基本URL
    // 默认情况下，Vue CLI假设您的应用程序将部署在域的根目录下。
    // https://www.my-app.com/。如果应用程序部署在子路径上，则需要使用此选项指定子路径。例如，如果您的应用程序部署在https://www.foobar.com/my-app/，集baseUrl到'/my-app/'.
//这个值也可以被设置为空字符串 ('') 或是相对路径 ('./') 修改这个 那么打包出来的index.html里的路径也是根据这个改变
    publicPath: "./",


    // outputDir: 在npm run build时 生成文件的目录 type:string, default:'dist'

     outputDir: 'dist',

    // pages:{ type:Object,Default:undfind } 
/*
  构建多页面模式的应用程序.每个“页面”都应该有一个相应的JavaScript条目文件。该值应该是一
  个对象，其中键是条目的名称，而该值要么是指定其条目、模板和文件名的对象，要么是指定其条目
  的字符串，
  详情请看下面多页面配置
  注意：请保证pages里配置的路径和文件名 在你的文档目录都存在 否则启动服务会报错的
*/
     pages: {
         //此处如果打包后打开显示空白那就直写 entry  其他不写
          console: {
            // 应用入口配置，相当于单页面应用的main.js，必需项
            entry: 'src/modules/console/console.js',

            // 应用的模版，相当于单页面应用的public/index.html，可选项，省略时默认与模块名一致
            // template: 'public/console.html',

            // 编译后在dist目录的输出文件名，可选项，省略时默认与模块名一致
            // filename: 'console.html',

            // 标题，可选项，一般情况不使用，通常是在路由切换时设置title
            // 需要注意的是使用title属性template 中的 title 标签需要是 <title><%=htmlWebpackPlugin.options.title %></title>
            // title: 'console page',

            // 包含的模块，可选项
            // chunks: ['console']
        },
        // 只有entry属性时，直接用字符串表示模块入口
        client: 'src/modules/client/client.js'
   	 },

    //   lintOnSave：{ type:Boolean default:true } 问你是否使用eslint
    lintOnSave: true,
    // productionSourceMap：{ type:Bollean,default:true } 生产源映射
    // 如果您不需要生产时的源映射，那么将此设置为false可以加速生产构建
    productionSourceMap: false,
    // devServer:{type:Object} 3个属性host,port,https
    // 它支持webPack-dev-server的所有选项

    devServer: {
        port: 8085, // 端口号
        host: 'localhost',
        https: false, // https:{type:Boolean}
        open: true, //配置自动启动浏览器
        // proxy: 'http://localhost:4000' // 配置跨域处理,只有一个代理
        proxy: {
            '/api': {
                target: '<url>',
                ws: true,
                changeOrigin: true
            },
            '/foo': {
                target: '<other_url>'
            }
        },  // 配置多个代理
    }
}
```

#### 基本上以上的vue.config.js配置能解决大部分的问题如果还需要修改就根据具体的业务进行修改。

#### Vue cli 3 多页面配置

##### 创建多页面应用

首先，安装两个插件，vue-router和vue-wechat-title。vue-router不解释了，vue-wechat-title为单页面应用修改标题的插件.(就是标签页的名字)

##### 创建模块

在src下创建目录modules，在modules下创建两个模块console和client；

在public下添加模版console.html和clien.html(直接复制原有的index.html即可)

##### 应用路由配置

通过vue-router为应用配置路由，以console模块为例，在router.js中添加路由配置：

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const routes = [
    { path: '/', name: 'login', component: r => { require(['./login/Login'], r) }, meta: { title: 'console 登录' }}
]

export default new VueRouter({
    routes: routes
})
```

##### 应用title跟随路由切换

```js
import Vue from 'vue'
import Console from './Console.vue'
import router from './router'

Vue.use(require('vue-wechat-title'))

new Vue({
    router,
    render: h => h(Console)
}).$mount('#console')
```

在console.vue中添加`v-wechat-title`指令，console.vue内容为：

```vue
<template>
    <div id="console" v-wechat-title="$route.meta.title">
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name: "console"
    }
</script>

<style scoped>

</style>
```

至此，针对console模块的配置完成，对client模块做相同配置即可。

项目结构图

#### axios踩坑记录+拦截器使用+vue cli代理跨域proxy+webpack打包部署到服务器

https://www.cnblogs.com/goloving/p/8901960.html

#### 使用预处理语言less

npm install  less less-loader --save-dev

```HTML
<style lang="less" scoped>
//lang 声明编译语言  
//scoped 声明css样式的作用范围只限于该页面中的元素。
</style>
```

```less
新建less文件
//相关的混合操作
.w(@px){
    width: unit(@px/37.5,rem);
}
.padding(@top,@right,@bottom,@left){
    padding-top:unit(@top/37.5,rem);
    padding-bottom:unit(@bottom/37.5,rem);
    padding-left:unit(@left/37.5,rem);
    padding-right:unit(@right/37.5,rem);
}
局部引入
style下面  如
@import url("../../../styls/main.less");引入
然后可以使用.w(375);.padding(1,1,1,1);
全局引入
main.js   import "./styls/reset.less"
```



###### 打包  （开发、生产环境？） api统一管理

在src文件夹里新建api文件夹 里面新建api.js

内容

```
let baseURL = "/api";//直接npm run dev 运行项目用这个
//let baseURL = "http://192.168.0.43:8080";//打包时用这个	http://192.168.0.43:8080为开启后端服务我网址

export default function DISTRIBUTE(){
    return{
        "login":`${baseURL}/sys/auth/login`,  //登录
        "register":`${baseURL}/sys/auth/register` //注册
    }
}


//后端接口为http://192.168.0.43:8080/sys/auth/register
//这样写的好处   当IP发生变化时，只需改变一个  后端接口改变时，不要翻看代码
```

使用 

​		main.js引入

```
import API from './api/api.js'
Vue.prototype.API=API
```

​		要与后端交互发起请求

```
var params = new URLSearchParams();
params.append('us',this.val);
params.append('ps',this.pas);
this.$axios.post(this.API().login,params)
.then((res)=>{
	console.log(res);
})
//this.API().login相当于http://192.168.0.43:8080/sys/auth/login
```

