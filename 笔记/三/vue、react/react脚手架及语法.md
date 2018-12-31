## 一、react脚手架安装步骤

```
$ cnpm install -g create-react-app	//全局安装react
$ create-react-app my-app			//创建脚手架
$ cd my-app/						
$ npm start
```

## 二、react添加取消类名方式

#### 1. 添加取消类名

> 思路：现在上面定义一个变量，例如：isShowSearchBar:true，然后给你要点击的那个东西添加onClick={}事件，然后根据变量的true和false来决定添加取消类名，

```
 className={this.state.isShowSearchBar? "weui-search-bar": "weui-search-bar weui-
search-bar_focusing"}

============定义变量阶段================
 constructor(props){
        super(props);
        this.state = {
            isShowSearchBar:true
        }
    }
    
=============改变变量阶段================
changeSearchBar(){
        this.setState({
            isShowSearchBar:!this.state.isShowSearchBar
        })
 }
 
 ==================绑定事件阶段==========
<a href="javascript:" onClick={this.changeSearchBar.bind(this)} className="weui-search-bar__cancel-btn" id="searchCancel">取消</a>


========================================================



```

#### 2. tab切换形式

> 思路：先定义一个变量为0，以索引的形式切换，把点击事件写给你要点击的东西，当你点击的时候，把索引传给函数，通过函数事件把index赋给你定义的变量，然后在下面根据你的变量等于索引的三元表达式形式，添加类名，例子如下：

```
class Xfooter extends Component {
    constructor(props){
        super(props);
        this.state = {
            tab:0,
            tabs:[{
                title:"微信",
                href:"wechat",
                num:8,
                dot:false
            },{
                title:"通讯录",
                href:"contact",
                num:0,
                dot:true
            },{
                title:"发现",
                href:"research",
                num:0,
                dot:false
            },{
                title:"我",
                href:"mine",
                num:0,
                dot:false
            }]
        }
    }
====================================================
 toggloClass(index,e){
        this.setState({
            tab:index
        })
    }
    
 ===================================================
  <a href="javascript:;" key={index} onClick={this.toggloClass.bind(this,index)} className={this.state.tab==index? "weui-tabbar__item weui-bar__item_on": "weui-tabbar__item"}>

```

## 三、文本框聚焦

> 思路：先给你要聚焦的文本框绑定ref=“变量名”，然后在你的点击事件里面写，this.refs.变量名.focus();既可聚焦

```
==================
this.refs.imput.focus();

==========================================
<input ref="imput" type="search" className="weui-search-bar__input" id="searchInput" placeholder="搜索" required="" />


```

## 四、获取文本框的value方法

> 思路：先给文本框绑定onChange事件，记住要用大括号的形式{}，在上面的事件函数里面传个e，就直接获取e.target.value,然后再上面this.state里面定义一个变量，例如：searchValue:"",然后通过this.setState({})的方法把值赋给那个变量既可。

```
==============定义阶段===============
  constructor(props){
        super(props);
        this.state = {
            isShowSearchBar:true,
            searchValue:""
        }
    }
    
    
    ==========获取文本框值阶段========
    
  getInputValue(e){
       this.setState({
            searchValue:e.target.value
       })
        console.log(e.target.value)
    }

```

## 五、函数式编程

> 思路：能在虚拟dom里任意一地方放{{}}编写逻辑，会在虚拟Dom里渲染return的数据

```
步骤：1.先在上面定义一个数组
	 2.然后在下面写一个自执行的函数，例如：{(()=>{
	 	return this.state.tabs.map((item,index)=>{
                
	 		})
	 	
	 })()}
```

### 六、路由

#### 1. 路由的起步

- 下载路由模块

```
npm install react-router-dom

```

- 在index.js引入

```
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

```

- 在index.js外面包上`<Router></Router>`

```
ReactDOM.render(
  <Router>
    <div>
      <Xheader />
      <Xsearch />
      <Xpannel />
      <Xfooter />
    </div>
  </Router>,
  document.getElementById('root'))

```

#### 2. 路由的跳转实现及步骤

- 建议在index.js页面引入哈希路由

```
import { HashRouter  as Router, Route } from 'react-router-dom'

```

- 在ReactDOM.render下面写上

```
ReactDOM.render(
  <Router>
    <div>
      <Route path="/home/" component={Home} />			//判断路径如果是/home/就去home组件
      <Route path="/Detail/" component={Detail} />		//判断路径如果detail就去detail组件

      {/* <Redirect from="/home" to="/home/wechat" /> */}

    </div>
  </Router>,
  document.getElementById('root'))

```

- 然后在home页面引入路有插件和小组件

```
import { Route } from 'react-router-dom'

import Wechat from '../Wechat/Wechat'
import Contact from '../Contact/Contact'
import Research from '../Research/Research'
import Mine from '../Mine/Mine'

```

- 根据路径判断调到那个路由

```
<Route path="/home/wechat"  component={Wechat} />
<Route path="/home/contact" component={Contact} />
<Route path="/home/research" component={Research} />
<Route path="/home/mine" component={Mine} />

```

- 去Xfooter页面引入路由组件

```
import { Link } from 'react-router-dom'

```

- 把`a`标签改为`Link`，然后在里面写`to{/home/${item.href}}`

```
<Link to={`/home/${item.href}`}></Link>
解释：你的href要在上面就定义好，然后直接调用，例如：
{title:"微信",
href:"wechat",
num:8,
dot:false}

```

#### 3. 设置默认路由

- 进入页面引入时加`Redirect`

```
import { HashRouter  as Router, Route , Redirect ,Switch} from 'react-router-dom'

```

- 下面写默认路由

```bash
ReactDOM.render(
    <Provider store={store}>
        <Router>
            <div className="container iphonex_padding">
                <Switch>
                    <Route path="/home/" component={Home} />
                    <Redirect from="/" exact  to="/home/HomeIndex" />
                </Switch>
            </div>
        </Router>
  </Provider>, document.getElementById('root'));
  
  ======================
 <Link to={ {pathname:`/home/${item.href}` }}  replace >
 </Link>
```

## 七、redux组件通信

```
npm install --save react-redux
npm install --save redux
```

- 在index.js引入

```
//redux
import {Provider, connect} from 'react-redux';
import {createStore} from 'redux';

```

- 创建仓库

```
const store = createStore(function(state={

},action){})

```

- 在下面用`Provider`包住

```bash
ReactDOM.render(
  <Provider store={store}>		//注入store
  <Router>
    <div>
      <Route path="/home/" component={Home} />
      <Route path="/Detail/" component={Detail} />

      <Redirect from="/home" to="/home/wechat" />

    </div>
  </Router>
  </Provider>,
  document.getElementById('root'))
```

- 在你要用redux的仓库引入

```
import { connect} from 'react-redux';

```

- 在最下面写

```
export default connect((state)=>{
    return state	//把你从仓库拿到的东西return出来
},(dispatch)=>{
    return {
        toggleSheet() {			//把你改的东西return出去
          dispatch({
            type: 'toggleSheet',
            isShowActionSheet: false
          })
        }
      }
})(XactionSheet)


================在结构里面写的=================
 <div className="weui-skin_android" onClick={this.props.toggleSheet} id="androidActionsheet" style={{
            opacity: 1,
            display:this.props.isShowActionSheet ? "block": "none"
         }}>

```

- 在index.js里面接收回你改的东西

```bash
const store = createStore(function(state={
    isShowActionSheet:false		//初始化设置为false
},action){

    switch (action.type) {
      case 'toggleSheet':	//如果类型为 ‘toggleSheet’
        return {		
            ...state,		//展开state
            isShowActionSheet:action.isShowActionSheet	//设置为接收回来的状态
        }
      default:
        return state	//默认返回state的东西
    }
})
```

## 九、组件

- 里面包含html，css，js

- react是把所有的html，css都放进js文件里面
- react定义组件，先创建`xxx.js`，在文件里面引入`react`模块

```js
import React, { Component } from 'react';
```

- 所有组件继承于`Component`

```
class 组件名字 extends Component {}
```

- 导出组件

```js
export default App;
```

```bash
使用redux时，记住一定要把东西在仓库就先return出来，要不然外边拿不到
  switch (action.type) {
    //   case 'toggleSheet':
    //     return {
    //         ...state,
    //         isShowActionSheet:action.isShowActionSheet
    //     }
      default:
        return state
    }
```

#### 3. react路由设置、及重定向

```bash
路由冲定向时会报错，记得要引入	**import { HashRouter  as Router, Route , Redirect ,Switch} from 'react-router-dom'

===========
用switch包住你的路由判断那里
<Switch>
    <Route path="/home/" component={Home} />
    <Redirect from="/" exact  to="/home/HomeIndex" />
</Switch>

===============
在link里面要把普通的`to`改成`to={ {pathname:`/home/${item.href}` }}  replace`

```

#### 4. redux修改仓库中数组的某一项、实现联动效果

```bash
如果你要是想通过点击事件触发仓库中的某一个值，是数组的情况下，你需要遍历仓库中的数组，把你要变得索引传过来，然后让其他的不变，例如：
const store = createStore(function (state = {
    navs: [{
      title: '推荐',
      href: 'recommend',
      isShow:true,
      recommend: []
    }, {
      title: '少儿',
      href: 'children',
      isShow:false,
      children: []
    }, {
      title: '成人',
      href: 'adult',
      isShow:false,
      adult: []
    }, {
      title: '父母',
      href: 'parents ',
      isShow:false,
      parents: []
    }, {
      title: '家庭',
      href: 'family',
      isShow:false,
      family: []
    }, {
      title: '旅行',
      href: 'travel',
      isShow:false,
      travel: []
    }]
  } ,action) {
  switch (action.type) {
      case 'isActive': 
      var  {navs}  = state		 // 把仓库赋值给navs
      for(var i=0;i<navs.length;i++){	 // 遍历navs仓库，找到你要的东西
        navs[i].isShow=false
        navs[action.index].isShow =action.isShow
        console.log(navs[i])
      }
      navs.isShow = action.noShow
        return {
            ...state,
            isShow:false
        }
    default:
      return state
  }
})
===============触发那边==============

export default connect((state)=>{
    return state    
} , (dispatch) => {
    return {
        isActive(index){
            console.log(this.props)
            this.setState({
                isActive:index		//修改本地的内容
            })
            dispatch({
                type:"isActive",
                index: index,	//传索引`index`
                isShow:true		//传状态
              })
        }
    }
})(Xnav);
```



#### 6. 路由嵌套问题

> 在哪个页面的二级路由，就写在哪个页面，例如：你要在首页写二级路由，你就把二级路由写在首页，
>
> 然后一级路由会基于你二级路由跳转的路径跳转，所以你要加个斜杠`/`在一级路由那里`/${item.href}` 

```bash
 ===================二级路由home写法=====================
 <Route path='/home/Xrecommend' component={Xrecommend} />
 <Route path="/home/Xchildren"  component={Xchildren} />
 <Route path="/home/Xadult" component={Xadult} />
 <Route path="/home/Xparents" component={Xparents} />
 <Route path="/home/Xfamily" component={Xfamily} />
 <Route path="/home/Xtravel" component={Xtravel} />
 
 =============一级路由跳转=============
  <Link to={ {pathname:`/${item.href}` }}  replace key={index} onClick={this.toggleClass.bind(this,index)}  className={this.state.tab===index? "public_tab_item active" : "public_tab_item"} id={item.dataId}>
  <div className="public_tab_info">
  <p className={`public_tab_icon ${item.dataClass}`}></p>
  <p>{item.title}</p>
  </div>	
  </Link>
```

#### 7. 导航高亮刷新保持

> `window.location.hash.slice(2) `[参考链接](http://www.cnblogs.com/icaihua/p/9869846.html)

```bash
 switch (window.location.hash.slice(2)) {
        case "/home/Xrecommend":
          this.state.tab=0
          break;
          case "bestchoice":
          this.state.tab=1
          break;
          case "search":
          this.state.tab=2
          break;
          case "mine":
          this.state.tab=3
          break;
        default: this.state.tab=0
          break;
      }
  }
  **然后下面根据路径变化打类名
  
 =============正常方法================
 // 根据路径给togoleclass赋值
     switch (props.location.pathname) {
      case "/home/Xrecommend":
      this.state.togolleClass=0
        break;
        case "/home/Xchildren":
      this.state.togolleClass=1
        break;
        case "/home/Xadult":
      this.state.togolleClass=2
        break;
        case "/home/Xparents":
      this.state.togolleClass=3
        break;
    case "/home/Xfamily":
      this.state.togolleClass=4
        break;
    case "/home/Xtravel":
      this.state.togolleClass=5
        break;
      default:
        this.state.togolleClass=0
        break;
    }
    ===========传值给子组件==========
    <Xnav tab={this.state.togolleClass}/>
    ==========接收============
    this.props = props; 
    ===========赋值==============
    this.state = {
        isActive:this.props.tab
       
    }
  //然后下面根据三元正常判断即可  
```

#### 9.邮箱验证码步骤及思路

> 思路：当你点击发送验证码时，发起ajax请求，后端生成验证码，发送到你上面`注册`的邮箱，后端缓存验证码，留到用户拿到验证码输入时进行比对，正确，则插入数据库，失败不插入

- 先下载模块`nodemailer`

```bash
cnpm install nodemailer --save-dev
```

- 引入模块

```bash
const nodemailer = require('nodemailer');	//引入模块
let transporter = nodemailer.createTransport({
    service: 'qq',	//类型qq邮箱
    port: 465,
    secure: true, // true for 465, false for other ports
    auth: {
        user:'854453495@qq.com', // 发送方的邮箱
        pass: 'vrtjembbhfcmbegj' // smtp 的授权码
    }
});


function sendMail(mail,code,call){
    // 发送的配置项
    let mailOptions = {
        from: '"Fred Foo 👻" <854453495@qq.com>', // 发送方
        to: mail, // 接收方
        subject: '欢迎注册“小雨伞”保险！', // 标题
        text: 'Hello world?', // 文本内容
        html: `<h1>您的验证码是:${code},请注意安全性，该验证码有效期为 5分钟</h1>`//页面内容
    };

   //发送函数
    transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
       call(-1)
    }
     call(0)//因为是异步 所有需要回调函数通知成功结果

    });

}

module.exports={sendMail}
```

- 接收前端路由处

```bash
var express = require('express');
var router = express.Router();
var db = require('../lib/db.js');
var email = require('./sendEmail.js');	//引入封装好的函数
console.log(email)
//解决跨域问题
router.all('*', function (req, res, next) {
  res.header('Access-Control-Allow-Origin', '*');
  //Access-Control-Allow-Headers ,可根据浏览器的F12查看,把对应的粘贴在这里就行
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  res.header('Access-Control-Allow-Methods', '*');
  res.header('Content-Type', 'application/json;charset=utf-8');
  next();
});

/* GET users listing. */
router.get('/', function(req, res, next) {
  res.send('respond with a resource');
});


let check={}	//声明一个对象缓存邮箱和验证码，留着
router.post('/email', function(req, res, next) {
    console.log(req.body.params)
    let mail=req.body.params.email
    if (!mail) {return res.send('参数错误')}	//email出错时或者为空时
    let code = parseInt(Math.random(0,1)*10000)	//生成随机验证码
    check[mail]=code
    //发送邮件
     email.sendMail(mail,code,(state)=>{
            if (state) {
                res.send('验证码发送成功')
            }else{
               res.send('验证码发送失败')
            }
            
      })
   
  
});
router.post('/login', function(req, res, next) {
    console.log(req.body.params)
     db.query(function(db) { //这里要用函数
        db.collection("login").insertMany([req.body.params], function(err, result) {

            res.send('succees');
        });
    })

});
module.exports = router;




```

#### 10.路由获取方法

> 思路：在最大的组件获取到路由，通过props方法传到需要的子组件去
>
> 备注：因为小组件拿不到props

```bash
var url = this.props.loction.pathname
<Xheader url={url}/>
```

#### 11.路由跳转的两种方式

> 备注：如果不是需要注册登录那种判断，用Link即可

- Link方式

```bash
import { Link  } from 'react-router-dom'

<Link to={ {pathname:`/${item.href}` }}  replace > </Link>
<Link to={ {`/home`}}  replace > </Link>
```

- withRouter 方式

应用场景说明:

```js
 <Route exact path="/Home" component={Home}/>

目的就是让被修饰的组件可以从属性中获取history,location,match,
路由组件可以直接获取这些属性，而非路由组件就必须通过withRouter修饰后才能获取这些属性了
1.只有包裹在Route组件里的才能使用`this.props.location`，
2.假如有个需求，是面包屑或者导航组件里需要拿到`this.props.location`（导航组件或者面包屑一般不会包裹在`Route`里吧），那么直接这么写显然就不行了。必须通过withRouter修饰后才能获取到。
```

```bash
import { withRouter   } from 'react-router-dom'
===========React-Router 2.4.0版本以上=========
import { withRouter } from 'react-router';
clsss ABC extends Component {
}
module.exports = withRouter(ABC);

===========React-Router 3.0.0版本以上=========
this.props.router.push('/home/Xrecommend')

===========React-Router 4.0版本以上===========
this.props.history.push('/home/Xrecommend')
```

> 稳稳的写法

```bash
 import { withRouter   } from 'react-router-dom'
 =============================================
 goCar(){
    this.props.history.push('/carOrder')
  }
 ============================================= 
  export default withRouter(Xorder)
```



#### 12.参数的获取

```bash
使用`this.props.match.params.xxx` 可以获取到当前路由的参数
```

#### 13.react `cookie`用法

- 先下载模块

```bash
cnpm install  react-cookie --save-dev
```

- 引入

```
import cookie from 'react-cookies'

```

- 存入`cookie`

```visual basic
cookie.save('userId', this.state.value)；
```

- 删除`cookie`

```
cookie.remove('userId')

```

- 获取`cookie`

```
select([regex])
this.state =  { userId: cookie.load('userId') };

```

#### 14.React的Sass配置

- 先下载

```bash
npm install sass-loader node-sass --save-dev
```

- 找到配置文件，

```bash
node_modules/react-scripts/config/webpack.config.dev.js
```

- 找到module下的rules，然后找到最后一个配置，修改成如下的样子 

```bash
{

    exclude: [/\.js$/,/\.html$/,/\.json$/,/\.scss$/],

    loader: require.resolve('file-loader'),

    options: {

            name: 'static/media/[name].[hash:8].[ext]',

        },

},

{

    test:/\.scss$/,

    loaders:['style-loader','css-loader','sass-loader']

}

备注：如果不行的话，再把`webpack.config.prod.js`也变成同样的配置
```

#### 15.loading效果

> veu、react通用

- 下载、引入axios

```bash
========react=========
cnpm install axios --save-dev
import axios from 'axios'
=========vue==========
cnpm install mint-ui --save-dev
import Mint from 'mint-ui';
Vue.use(Mint);
```

- 下载引入antd-mobile 

```bash
=========react==========
import { Toast } from 'antd-mobile';
import './assets/antd-mobile.css'
==========vue===========
```

- 引入样式

```bash
备注：样式在node-modues里面，可自行找路径，或复制过来
import './assets/antd-mobile.css'
*vue如需引用样式，同理
import 'mint-ui/lib/style.css';
```

- 在index.js写如下代码

```bash
=============请求之前loading==============
axios.interceptors.request.use((config) => {
  Toast.loading('', 3,true);
	return config;
}, (err) => {
	return Promise.reject(err)

})
===========请求成功之后取消loading=======
axios.interceptors.response.use((response) => {
	Toast.hide(); //关闭loading
	return response;
}, (err) => {
	return Promise.reject(err);

})
```

- 在vue的main.js中

```bash
============请求之前loading==============
Axios.interceptors.request.use((config) => {
	Mint.Indicator.open({ //打开loading
		text: '加载中...',
		spinnerType: 'fading-circle'
	});
	return config;
}, (err) => {
	return Promise.reject(err)

})
==============请求成功之后取消loading=======
Axios.interceptors.response.use((response) => {
	Mint.Indicator.close(); //关闭loading
	return response;
}, (err) => {
	return Promise.reject(err);

})
```

#### 16.回退`goback()`用法

```bash
import {createHashHistory} from 'history';//组件引入
const history = createHashHistory();
===========后退=========
goback(){
      this.props.history.goBack()  
  }
===========前进========
 push(){
      this.props.history.push()  
  }
```

#### 切换路由回退顶部

```
class ScrollToTop extends Component {
  componentDidUpdate(prevProps) {
    if (this.props.location !== prevProps.location) {
      window.scrollTo(0, 0);
    }
  }

  render() {
    return this.props.children;
  }
}
export default withRouter(ScrollToTop);
//Route包裹 传入location 监听其变化新旧location不相等则执行window.scrollTo(0, 0);回顶部
<Route history={history}  render={({ location }) => (
    <ScrollToTop location={location}>
        <div style={{position: 'absolute',width:'100%',height:'100%'}}>
            <Switch location={location}>
                    <Route  path="/home/" component={Home} />
                    <Route  path="/detail/" component={Detail} />
                    <Route  path="/param/" component={Param} /> 
                    <Route  path="/comment/" component={Comment} /> 
                    <Route  path="/mine/" component={Mine} />
                    <Route  path="/list" component={List}/>
                    <Route  history={history}  path="/login" component={Login}/>
                    <Route  history={history} path="/registe" component={Registe}/>
                    <Route  path="/phone" component={Phone}/>
                    <Route path="/exchangeRate" component={ExchangeRate}/>
                    <Route path="/cart/" component={Cart}/>
                    <Route path="/personal/" component={Personal}/>
                    <Redirect history={history} from="/" exact to="/home/mainPage1" />
                </Switch> 
        </div>
    </ScrollToTop>
)}/>

```

