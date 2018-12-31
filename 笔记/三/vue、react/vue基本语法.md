#  vue

#### 1. 直接在html引入`vue.js`

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>
//中间的网址即为下载地址
```

#### 2.jquery与vue的异同

- `jquery.js`提供`$或者jquery`全局变量
- `vue.js`提供`vue`全局变量
- Vue的核心库只关注视图层，读音`view`
- 双向数据绑定，data里数据改变视图也改变
- 如果页面注重操作节点，用jquery
- 如果页面数据比较多，建议用vue

## 二、开发工具

#### 1.用git下载谷歌浏览器工具，然后方便我们开发vue项目

```bash
git clone https://github.com/vuejs/vue-devtools.git
```

- 此时你会看到文件中多了一个`vue-devtools`文件
- 进入到这个文件npm install，安装依赖包； 
- 安装成功之后npm run build 
- 若不执行以上命令会报错，无法加载背景脚本"build/background.js"   //......
- 打开shells>chrome>manifest.json并把json文件里的"persistent":false改成true  //........
- 打开chrome浏览器，打开更多工具>扩展程序； 
- 再点击加载已解压的扩展程序，然后把shells>chrome文件夹放入 

## 三、helloworld

#### 1.先实例化`Vue`,里面允许我们放很多选项(https://cn.vuejs.org/v2/api/),可以放**数据，DOM，生命钩子，资源和组合**

```js
var vm = new Vue({
  // 选项
})
```

#### 2.你用jQ，第一要有数据，第二要有节点，没节点，数据没意义

```js
$.ajax()//
$(el).html(data)
//寻找节点，然后放数据
```

#### 3.放入必要的选项，el和data是必须要有的

el就是寻找节点（找作用域），data就是配合`{{}}`来渲染数据

```js
var vm = new Vue({
    // 选项
    data:{
        name:"lemon1"
    },
    el:"#demo"
})
```

#### 4.在view层的`id`为`demo`的作用域里面配合`{{}}`绑定数据

```html
<div id="demo">
    <p>{{num+1+'1'}}</p>
</div>
```

## 四、jQuery和Vue的表达式和指令

#### 1.文本值

```
jq写法
$().text();

vue写法
<p>{{name}}</p>
<p v-text="name"></p>

```

#### 2.属性值

- `:style`和`:class`是必须接受一个对象

  ```
   <style>
          .red{
              color:red
          }
          .bg{
              background-color:yellow
          }
          .size{
              font-size:28px
          }
      </style>
      <div id="demo">
          <p :name="name" :id="name+'&laoxie'">属性</p>
          <p :style="style1">样式1</p>
          
          ===========================================
          <p :style="{
              color:'red',
              fontSize:'14px',
              backgroundColor:'yellow'
          }">样式2</p>
          <p :class="class1">样式1</p>
      </div>
      =====================================================
      <script src="../../js/vue.js"></script>
   
   var vm = new Vue({
              // 选项
              // 数据选项
              data:{
                  name:"lemon",
                  style1:{
                      color:'red',
                      fontSize:'14px',
                      backgroundColor:'yellow'
                  },
                  class1:{
                      red:true,
                      bg:false,
                      size:true
                  }
              },
              el:"#demo"
          })
    
    解释：就是你要是写style样式，或者是要以类名的方式添加样式，就要在下面写成对象的方式，然后再给上面添加变量即可
  
  ```

- `:xxx`都可以接受任何变量

```
jq写法
$().attr();
$().css();
$().addClass();

vue写法
<p :name="name"></p>

```

- 插入html结构

```
$().html()

<div v-html="html"></div>

```

- 显示或者隐藏，本质是控制css，节点一直存在的，频繁切换（选项卡，加载的动画）

```
jq写法
$().show()
$().hide()

vue写法
<div v-show="!bool">你好</div>

```

- 对节点增加或者删除，节点要不存在或者不存在

```
jq写法
$().append()
$().remove()

vue写法
<div v-if="!bool">你好</div>
<div v-else>假的</div>

```

- v-for放哪里，那个节点就跟着遍历对应的数组,支持嵌套其他指令`v-for,v-if和v-show`

```html
jq写法
$().each()

vue写法
<div v-for="item in arr" v-text="item.name"></div>

备注：
v-for 指令需要以 site in sites 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。
v-for 可以绑定数据到数组来渲染一个列表
```

- `v-on:click`简写为`@click`，就是把原生的onmousedown->@mousedown，把on改为@，把事件监听函数方法选项的`methods`里面

```html
jq写法
$().on()
$().click()

vue写法
<button @click="loadMore">查看更多</button>
```

- `v-bind:xxx`简写为`:xxx`

```html
<p v-bind:name="name">测试</p>
==============================
<p :name="name">测试</p>
备注：两种写法为一个意思
```

- `v-model`是把视图的值，带回选项`data`里面，只能用在这三个标签里面
- 视图层影响数据层`v-model`或者`v-on:click`

```
<input v-model="name" />
<select>
<textarea>

备注：v-model链接data中定义的数据
```

## 五、data、methods、{{}}

- data用于定义属性

```
例如：
data:{
    name:"lemon",
    style1:{
    color:'red',
    fontSize:'14px',
    backgroundColor:'yellow'
},
```

- methods 用于定义的函数，可以通过 return 来返回函数值。 

```
methods: {
    testClick: function () {
    console.log("你触发了点击事件")
    },
    testKeyup() {
    console.log("你触发了输入事件")
    },
    loadMore() {
    this.arr.push({
    name: 'laotian',
    age: 16,
    skill: ['xmind']
    })
    }
}

```

- {{ }} 用于输出对象属性和函数返回值。 

```
<div id="demo">
        <p>{{name}}</p>
        <p>{{arr}}</p>
        <p>{{arr[0]}}</p>
    </div>

```

## 六、模板语法

- 使用v-html指令用于输出html代码

```
<div id="demo">
        <div v-html="html"></div>
    </div>
    <script src="../../js/vue.js"></script>
    <script>
        new Vue({
            el: "#demo",
            data: {
                html: "<p>123<span>456</span>789</p>"
            }
        })
    </script>

备注：v-html一般用于输出HTML结构
```