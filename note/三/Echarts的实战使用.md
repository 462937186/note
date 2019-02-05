# Echarts+layui+jq数据可视化大屏展示

### Echarts结合vue

```
npm install echarts 
```

### Echarts结合layui

(1)下载layui echarts
(2)可以直接script标签引入，也可以用layui的模块化方案引入(如果要使用地图.js直接script标签引入更直接),修改echarts.js 添加	

##### window.layui && layui.define ? layui.define(function(exports){exports('echarts',factory(exports))}) :

```js
(function (global, factory) {
	typeof exports === 'object' && typeof module !== 'undefined' ? factory(exports) :
	typeof define === 'function' && define.amd ? define(['exports'], factory) :
    window.layui && layui.define ? layui.define(function(exports){exports('echarts',factory(exports))}) :
	(factory((global.echarts = {})));
}(this, (function (exports) { 'use strict';
.....
} 
```

### layui的模块化方案

layui可以自定义一个模块并引入

```js
/**
  @Author: yangjialin
	@Time: 2019-1
	@Tittle: moban
	@Description: 模板管理
 */
//此模块使用了jq先引入jq在进行面向对象编程最后导出模块
//此文件定义在非layui目录下 文件夹命名 /modules/ 
//以下是自定义模块示例
layui.define([
    'jquery',
], function (exports) {
    var $ = layui.jquery;
    var moban = {
        //在此写功能函数
        layout: function (layoutName){
            ...
        }
    // 导出模块
    exports('moban', moban)
});
//将修改后的echarts.js也丢进此  /modules/文件夹    
        
        
//使用的时候规定好目录
layui.config({
  base: '/modules/'
}).use(['jquery', 'http', "moban","echarts"], function () {
  var $ = layui.jquery,
    http = layui.http,
    moban = layui.moban,
     echarts=layui.echarts;
    console.log(moban.layout)
    console.log(echarts)
  
  ｝
        
        
        
```

### Echarts其实就是堆配置项，官方文档的实例也可以复制修改，并没有什么特殊的，只是说大屏的自适应来说echarts在某些特定情况下需要用一些特殊的手段。

### 在layui的框架下基于jq开发的大屏项目使用的是iframe标签将图表引入，布局使用的是百分比+rem+flex布局.（iframe不建议使用但是我就是用了）

### Echarts需要实现自适应大小需要在窗口变化的时候resize

```
 // 图像自适应
  window.onresize = function () {
    myChart.resize();
  }
```

### 除此之外echarts的字体也需要变化因为默认的是px所以需要在窗口变化的时候讲字体也变小

```js
//和rem原理差不多同样是借助了html的根字体大小来改变因为使用的是iframe所以图表都是自己在一个html
function setFontSize() {
        htmlSize = $("html").css("font-size");
        htmlSize = htmlSize.substring(0, htmlSize.indexOf("p"));
        fontSize = htmlSize * 0.13;//字体大小 根据需求自己调整
        labelLineLen = fontSize / 0.13 * 0.2;//线的大小 根据需求自己调整
     	//series(各个系列的的字体大小、线大小、长度)根据配置项及需求自己调整
        option.series[0].labelLine.normal.length = labelLineLen;
        option.series[0].itemStyle.normal.label.textStyle.fontSize = fontSize;
        option.series[1].label.normal.textStyle.fontSize = fontSize;
        option.tooltip.textStyle.fontSize = fontSize;
    	//最后set一下
        myChart.setOption(option);
    }
```

### Echarts引入地图

##### 有两种引入方式**JavaScript 引入示例**

```html
<script src="echarts.js"></script>
<script src="map/js/china.js"></script>
<script>
var chart = echarts.init(document.getElementById('main'));
chart.setOption({
    series: [{
        type: 'map',
        map: 'china'
    }]
});
</script>
```

**JSON 引入示例**（ECharts 使用 [geoJSON](http://geojson.org/) 格式的数据作为地图的轮廓，除了上述数据，你也可以通过其它手段获取地图的 [geoJSON](http://geojson.org/) 数据注册到 ECharts 中，在其他geoJSON工具中画好地图生成json引入也可以生成地图）

```js
$.get('map/json/china.json', function (chinaJson) {
    //JavaScript 方式引入地图，地图已经自动注册 ，json的话需要手动注册
    echarts.registerMap('china', chinaJson);
    var chart = echarts.init(document.getElementById('main'));
    chart.setOption({
        series: [{
            type: 'map',
            map: 'china'
        }]
    });
});
```

##### 我的项目是以JavaScript方式引入地图首先为了方便操作先获取地图的各省份经纬度

```js
var geoCoordMap = {};
var mapFeatures = echarts.getMap('china').geoJson.features;
    mapFeatures.forEach(function (v) {
        // 地区名称
        var name = v.properties.name;
        // 地区经纬度
        geoCoordMap[name] = v.properties.cp;

    });
```

##### 基本思路是将请求回来的数据进行处理 再以省份获取对应地图省份的经纬度从而改变数据 在set一遍 让其重绘

```js
//以省份名字去查询对应经纬度 返回一个数组可以直接替换 series（系列里的）data
//将需呈现在地图上的散点或者系列图省份传入
var convertData = function (data) {
        var res = [];
        for (var i = 0; i < data.length; i++) {
			//geoCoordMap表示上面echarts地图的经纬度集合  判定是否存在此城市的经纬度
            var geoCoord = geoCoordMap[data[i].name];
            if (geoCoord) {
                //传出的数组
                res.push({
                    //名字
                    name: data[i].name,
                    //地图经纬度
                    value: geoCoord.concat(data[i].value),
                    //提示框里的数量
                    serviceCompanyNum: data[i].serviceCompanyNum
                });
            }
        }
        return res;
    };
```

![](https://github.com/PandoraSB0X/record/blob/master/%E7%AC%94%E8%AE%B0/img/2019-02-01_180041.png?raw=true)

上述地图option

```js
var option = {
        color: "#fff",
    //此为左下角的图例 （图上没截到）
        legend: {
            orient: 'vertical',
            y: '74%',
            x: '2%',
            data: ['业务已覆盖区域', '服务项目主要集中地域', '2019将大力拓展区域'],
            textStyle: {
                color: '#fff',
                fontSize: 12,
                padding: 6
            }
        },
    //提示框组件
        tooltip: {
            trigger: 'item',
            formatter: function (res) {
                // console.log(res)  
                if(res.data.name==undefined){return ``}
                //data里的名字 和数量
                var str = res.data.name + ":" + res.data.serviceCompanyNum + "家";
                return str
            },

        },
      
        grid: {
            top: "0%",
            bottom: "50%",
            letf: "0%",
            right: "0%",
            containLabel: false,
        },
       //此处以geo地理坐标系组件直接用为地图不使用 series type：map
    	//series将作为三个散点图
        geo: {
            map: 'china',
            label: {
                emphasis: {
                    show: false
                }
            },
            //初始放大倍数
            zoom: 1.1,
            //是否允许放大缩小拖拉
            roam: true,
            //地图样式
            itemStyle: {
                //默认
                normal: {
                    areaColor: '#4F89C1',
                    borderColor: '#0B152D',
                    borderWidth: 1,
                },
                //高亮
                emphasis: {
                    areaColor: '#7AC8FF'
                }
            },
            //这个是改变地图上某个省份的颜色
            regions: [],
           
        },
        series: [{
                name: '1',
            //type: effectScatter 涟漪特效动画的散点（气泡）图
                type: 'effectScatter',
            //coordinateSystem 该系列使用的坐标系
                coordinateSystem: 'geo',
           	// 暂时为空 将请求回来的数据处理后一并设置
                data: [],
                symbolSize: function (val) {
                    console.log(val);
                    return val[0] / 5;
                },
                showEffectOn: 'render',
            //涟漪的模式  period周期  scale大小层数 brushType 模式
                rippleEffect: {
                    period: 4,
                    scale: 3,
                    brushType: 'fill'
                },
            //鼠标移动上去的动画
                hoverAnimation: true,
            //省份显示 show :false 不显示
                label: {
                    normal: {
                        formatter: '{b}',
                        position: 'right',
                        show: false
                    }
                },
            //itemStyle 每个散点的样式
                itemStyle: {
                    //默认样式
                    normal: {
                        //颜色渐变
                        color: {
                            type: 'radial',
                            x: 0.5,
                            y: 0.5,
                            r: 0.5,
                            colorStops: [{
                                    offset: 0,
                                    color: '#e75050' // 0% 处的颜色
                                },
                                {
                                    offset: 1,
                                    color: '#e75050' // 100% 处的颜色
                                }
                            ],
                            global: false, // 缺省为 false,
                        },
                    }
                },
            },
            {
                name: '2',
                type: 'effectScatter',
                coordinateSystem: 'geo',
                data: [],
                symbolSize: function (val) {
                    console.log(val);
                    return val[0] / 5;
                },
                showEffectOn: 'render',
                rippleEffect: {
                    period: 4,
                    scale: 3,
                    brushType: 'fill'
                },
                hoverAnimation: true,
                label: {
                    normal: {
                        formatter: '{b}',
                        position: 'right',
                        show: false
                    }
                },
                itemStyle: {
                    normal: {
                        color: {
                            type: 'radial',
                            x: 0.5,
                            y: 0.5,
                            r: 0.5,
                            colorStops: [{
                                    offset: 0,
                                    color: '#00e14a' // 0% 处的颜色
                                },
                                {
                                    offset: 1,
                                    color: '#00e14a' // 100% 处的颜色
                                }
                            ],
                            global: false, // 缺省为 false,
                        },
                    }
                },
            },
            {
                name: '3',
                type: 'effectScatter',
                coordinateSystem: 'geo',
                data: [],
                symbolSize: function (val) {
                    console.log(val);
                    return val[0] / 5;
                },
                showEffectOn: 'render',
                rippleEffect: {
                    period: 4,
                    scale: 3,
                    brushType: 'fill'
                },
                hoverAnimation: true,
                label: {
                    normal: {
                        formatter: '{b}',
                        position: 'right',
                        show: false
                    }

                },
                itemStyle: {
                    normal: {
                        color: {
                            type: 'radial',
                            x: 0.5,
                            y: 0.5,
                            r: 0.5,
                            colorStops: [{
                                    offset: 0,
                                    color: '#e19605' // 0% 处的颜色
                                },
                                {
                                    offset: 1,
                                    color: '#e19605' // 100% 处的颜色
                                }
                            ],
                            global: false, // 缺省为 false,
                        },
                    }
                },
            },
        ]
    }

var sinessData,projectData,expandData=[]
/*
	id: 1
    serviceArea: "山东"//echarts的省市是不带省的  如山东省  echarts里数据为 山东
    serviceCompanyNum: 1055
    serviceTime: "2019-01-28"
    serviceType: 1 //表示第一系列
*/
 for (var i = 0; i < data.length; i++) {
            var dataName = data[i].name;
            if (dataName) {
                if (data[i].serviceType == 1) {//一系列
                    sinessData.push({
                        //省份
                        'name': dataName,
                        //数量  (以下相同 存这个数量是为了做提示框)
                        "serviceCompanyNum": data[i].serviceCompanyNum
                    })
                } else if (data[i].serviceType == 2) {//二系列
                    projectData.push({
                        'name': dataName,
                        "serviceCompanyNum": data[i].serviceCompanyNum
                    })
                } else if (data[i].serviceType == 3) {//三系列
                    expandData.push({
                        'name': dataName,
                        "serviceCompanyNum": data[i].serviceCompanyNum
                    })
                }

            }
        }
//运行函数设置各系列data
        option.series[0].data = convertData(sinessData)
        option.series[1].data = convertData(projectData)
        option.series[2].data = convertData(expandData)

//需要什么效果从echarts官网上找实例复制然后并入就可以了
```

#### 有时候图表会需要一个长链接来更新数据那么就需要利用WebSocket

```js
var socket;
    if (typeof (WebSocket) == "undefined") {
        console.log("您的浏览器不支持WebSocket");
    } else {
        console.log("您的浏览器支持WebSocket");
        //实现化WebSocket对象，指定要连接的服务器地址与端口  建立连接
        //等同于socket = new WebSocket("ws://localhost:8083/checkcentersys/websocket/20");
        socket = new WebSocket("ws://" + window.location.host +"/screen/websocket/后端的端口链接");
        //打开事件
        socket.onopen = function () {
            console.log("Socket 已打开");
            //socket.send("这是来自客户端的消息" + location.href + new Date());
        };
        //获得消息事件
        socket.onmessage = function (msg) {
           
            //发现消息进入    开始处理前端触发逻辑
        };
        //关闭事件
        socket.onclose = function () {
            console.log("Socket已关闭");
        };
        //发生了错误事件
        socket.onerror = function () {
            console.log("Socket发生了错误");
            //此时可以尝试刷新页面
        }
        //离开页面时，关闭socket
        //jquery1.8中已经被废弃，3.0中已经移除
        // $(window).unload(function(){
        //     socket.close();
        //});
    }


```

#### 根据WebSocket返回的数据重新set图表（当然使用定时器也可以）

![](https://github.com/PandoraSB0X/record/blob/master/%E7%AC%94%E8%AE%B0/img/Video_2019-02-01_184220.gif?raw=true)

#### 图表不止这点但是做法都差不多，配置项官网上也有就不挂了