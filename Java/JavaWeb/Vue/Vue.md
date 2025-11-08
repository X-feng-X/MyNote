# Vue

+ Vue 是一套**前端框架**，免除原生 JavaScript 中的 DOM 操作，简化书写
+ 基于 **MVVM**（Model-View-ViewModel）实现，实现数据的**双向绑定**，将编程的关注点放在数据上
+ 官网：[Vue.js - 渐进式 JavaScript 框架 | Vue.js](https://cn.vuejs.org/)

## 一、Vue 基础知识

### 1. Vue 快速入门

+ 新建 HTML 页面，引入 Vue.js 文件

```html
<script src="js/vue.js"></script>
```

+ 在 JS 代码区域，创建 Vue 核心对象，定义数据模型

```html
<script>
	new Vue({
        el: "#app",
        data: {
            message: "Hello Vue!"
        }
    })
</script>
```

+ 编写视图

```html
<div id="app">
    <input type="text" v-model="message">
    {{ message }}
</div>
```

#### 1.1 插值表达式

+ 形式：`{{表达式}}`
+ 内容可以是：
  + 变量
  + 三元运算符
  + 函数调用
  + 算术运算

#### 代码演示

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-快速入门</title>
    <script src="js\vue.js"></script>
</head>

<body>

    <div id="app">
        <input type="text" v-model="message">
        {{message}}
    </div>

</body>
<script>
    // 定义Vue对象
    new Vue({
        el: "#app", // Vue接管的区域
        data: {
            message: "Hello Vue"
        }
    })
</script>

</html>
```



-----------------------------------



### 2. Vue 常用指令

+ 指令：HTML 标签上带有 `v-` 前缀的特殊属性，不同指令具有不同含义。例如：v-if，v-for...
+ 常用指令

<table>
    <tr>
    	<th>指令</th>
        <th>作用</th>
    </tr>
    <tr>
    	<td>v-bind</td>
        <td>为 HTML 标签绑定属性值，如设置 href，css 样式等</td>
    </tr>
    <tr>
    	<td>v-model</td>
        <td>在表单元素上创建双向数据绑定</td>
    </tr>
    <tr>
    	<td>v-on</td>
        <td>为 HTML 标签绑定事件</td>
    </tr>
    <tr>
    	<td>v-if</td>
        <td rowspan="3">条件性的渲染某元素，判定为 true 时渲染，否则不渲染</td>
    </tr>
    <tr>
    	<td>v-else-if</td>
    </tr>
    <tr>
    	<td>v-else</td>
    </tr>
    <tr>
    	<td>v-show</td>
        <td>根据条件展示某元素，区别在于切换的是 display 属性的值</td>
    </tr>
    <tr>
    	<td>v-for</td>
        <td>列表渲染，遍历容器的元素或者对象的属性</td>
    </tr>
</table>

#### 2.1 v-bind

```html
<a v-bind:href="url">feng</a>
```

```html
<a :href="url">feng</a>
```

#### 2.2 v-model

```html
<input type="text" v-model="url">
```

```html
<script>
    new Vue({
        el: "#app",
        data: {
            url: "https://www.baidu.com"
        }
    })
</script>
```

注意事项：通过 v-bind 或者 v-model 绑定的变量，必须在数据模型中声明

#### 2.3 v-on

```html
<input type="button" value="按钮" v-on:click="handle()">
```

```html
<input type="button" value="按钮" @click="handle()">
```

```html
<script>
    new Vue({
        el: "#app",
        data: {
            // ...
        },
        methods: {
            handle:function(){
                alert('我被点击了');
            }
        },
    })
</script>
```

#### 2.4 v-if

```html
// 年龄{{age}}，经判定为：
<span v-if="age <= 35">年轻人</span>
<span v-else-if="age > 35 && age < 60">中年人</span>
<span v-else>老年人</span>
```

#### 2.5 v-show

```html
// 年龄{{age}}，经判定为：
<span v-show="age <= 35">年轻人</span>
```

区别为：切换的是 css 的样式 display 属性的值来展示的

#### 2.6 v-for

```html
<div v-for="addr in addrs">{{addr}}</div>
```

```html
<div v-for="(addr,index) in addrs">{{index + 1}} : {{addr}}</div>
```

```html
data: {
	...
	addrs: ['北京','上海','广州','深圳','成都','杭州']
},
```

#### 案例：通过 Vue 完成表格数据的渲染展示

> 需求：
>
> <img src="./assets/image-20250603162246092.png" alt="image-20250603162246092" style="zoom:50%;" />

##### 代码实现

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-案例</title>
    <script src="js/vue.js"></script>
</head>

<body>

    <div id="app">
        <table border="1" cellspacing="0" width="60%">
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>年龄</th>
                <th>性别</th>
                <th>成绩</th>
                <th>等级</th>
            </tr>

            <tr align="center" v-for="(user,index) in users">
                <td>{{index + 1}}</td>
                <td>{{user.name}}</td>
                <td>{{user.age}}</td>
                <td>
                    <span v-if="user.gender == 1">男</span>
                    <span v-if="user.gender == 2">女</span>
                </td>
                <td>{{user.score}}</td>
                <td>
                    <span v-if="user.score >= 85">优秀</span>
                    <span v-else-if="user.score >= 60">及格</span>
                    <span style="color: red;" v-else>不及格</span>
                </td>
            </tr>
        </table>
    </div>

</body>
<script>
    new Vue({
        el: "#app",
        data: {
            users: [{
                name: "Tom",
                age: 20,
                gender: 1,
                score: 78
            }, {
                name: "Rose",
                age: 18,
                gender: 2,
                score: 86
            }, {
                name: "Jerry",
                age: 26,
                gender: 1,
                score: 90
            }, {
                name: "Tony",
                age: 30,
                gender: 1,
                score: 52
            }]
        },
        methods: {

        }
    })
</script>

</html>
```



-------------------------------



### 3. Vue 生命周期

+ 生命周期：指一个对象从创建到销毁的整个过程
+ 生命周期的八个阶段：每触发一个生命周期事件，会自动执行一个生命周期方法（钩子）

| 状态          | 阶段周期     |
| ------------- | ------------ |
| beforeCreate  | 创建前       |
| created       | 创建后       |
| beforeMount   | 挂载前       |
| **mounted**   | **挂载完成** |
| beforeUpdate  | 更新前       |
| updated       | 更新后       |
| beforeDestroy | 销毁前       |
| destroyed     | 销毁后       |

<img src="./assets/image-20250603165413768.png" alt="image-20250603165413768" style="zoom:50%;" />

```html
<script>
	new Vue({
        el: "#app",
        data: {
            
        },
        mounted() {
            console.log("Vue挂载完毕，发送请求获取数据");
        },
        methods: {
            
        },
    })
</script>
```

+ mounted：挂在完成，Vue 初始化成功，HTML 页面渲染成功（发送请求到服务端，加载数据）

### 总结

1. Vue 是什么？

+ Vue 是一个基于 MVVM 模型的前端 js 框架

2. Vue 常用指令？

+ v-bind、v-model、v-on、v-if、v-show、v-for

3. Vue 生命周期？

+ mounted



-------------------------------------



## 二、Ajax

+ 概念：Asynchronous JavaScript And XML，**异步**的 JavaScript 和 XML
+ 作用：
  + 数据交换：通过 Ajax 可以给服务器发送请求，并获取服务器响应的数据
  + 异步交互：可以在**不重新加载整个页面**的情况下，与服务器交换数据并**更新部分网页**的技术，如：搜索联想、用户名是否可用的校验等等

<img src="./assets/image-20250603170712717.png" alt="image-20250603170712717" style="zoom:50%;" />

### 1. 同步与异步

<img src="./assets/image-20250603170917760.png" alt="image-20250603170917760" style="zoom:50%;" />

### 2. 原生 Ajax

1. 准备数据地址
2. 创建 XMLHttpRequest 对象：用于和服务器交换数据
3. 向服务器发送请求
4. 获取服务器响应数据

```html
<body>

    <input type="button" value="获取数据" onclick="getData()">

    <div id="div1"></div>

</body>
<script>
    function getData() {
        // 1. 创建XMLHttpRequest
        var xmlHttpRequest = new XMLHttpRequest();

        // 2. 发送异步请求
        xmlHttpRequest.open('GET', 'https://www.baidu.com');
        xmlHttpRequest.send(); // 发送请求

        // 3. 获取服务响应数据
        xmlHttpRequest.onreadystatechange = function () {
            if (xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200) {
                document.getElementById('div1').innerHTML = xmlHttpRequest.responseText;
            }
        }
    }
</script>
```

这种请求方式比较繁琐，而且在早期的浏览器当中还存在兼容性问题，所以在现在的项目开发中原生的方式已经基本不用了，现在用的是封装起来的技术，比如 Axios



-----------------------------------------



### 3. Axios

+ 介绍：Axios 对原生的 Ajax 进行了封装，简化书写，快速开发
+ 官网：https://www.axios-http.cn/

<img src="./assets/image-20250603172218514.png" alt="image-20250603172218514" style="zoom:50%;" />

#### 3.1 Axios 入门

1. 引入 Axios 的 js 文件

```html
<script src="js/axios-0.18.0.js"></script>
```

2. 使用 Axios 发送请求，并获取响应结果

```javascript
axios({
	method: "get",
    url: "https://baidu.com"
}).then((result)=>{
    console.log(result.data);
});
```

```javascript
axios({
	method: "post",
    url: "https://baidu.com",
    data: "id=1"
}).then((result)=>{
    console.log(result.data);
});
```

#### 3.2 请求方式别名

> + `axios.get(url [, config])`
> + `axios.delete(url [, config])`
> + `axios.post(url [, data[, config]])`
> + `axios.put(url [, data[, config]])`

+ 发送 GET 请求

```javascript
axios.get("https://baidu.com").then((result)=>{
    consle.log(result.data);
})
```

+ 发送 POST 请求

```javascript
axios.post("https://baidu.com", "id=1").then((result)=>{
    consle.log(result.data);
})
```

#### 代码演示

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ajax-Axios</title>
    <script src="js/axios.js"></script>
</head>

<body>

    <input type="button" value="获取数据GET" onclick="get()">

    <input type="button" value="删除数据POST" onclick="post()">

</body>
<script>
    function get() {
        // 通过axios发送异步请求-get
        // axios({
        //     method: "get",
        //     url: "https://baidu.com"
        // }).then((result) => {
        //     console.log(result.data);
        // })

        axios.get("https://baidu.com").then((result) => {
            console.log(result.data);
        })
    }

    function post() {
        // 通过axios发送异步请求-post
        // axios({
        //     method: "post",
        //     url: "https://baidu.com",
        //     data: "id=1"
        // }).then((result) => {
        //     console.log(result.data);
        // });

        axios.post("https://baidu.com", "id=1").then((result) => {
            console.log(result.data);
        })
    }

</script>

</html>
```



------------------------



## 三、前后端分离开发

### 1. 介绍

前后端混合开发（前后端不分离）

+ 沟通成本高
+ 分工不明确
+ 不便管理
+ 不便维护扩展

#### 1.1 前后端分离开发

当前最主流的开发模式：前后端分离

<img src="./assets/image-20250605202245733.png" alt="image-20250605202245733" style="zoom:50%;" />

<img src="./assets/image-20250605202307090.png" alt="image-20250605202307090" style="zoom:50%;" />



------------------------------



### 2. YAPI

+ 介绍：YApi 是高效、易用、功能强大的 api 管理平台，旨在为开发、产品、测试人员提供更优雅的接口管理服务
+ 地址：[[YApi Pro-高效、易用、功能强大的可视化接口管理平台](https://yapi.pro/)](http://yapi.paiplus.work/)

<img src="./assets/image-20250605203234969.png" alt="image-20250605203234969" style="zoom:50%;" />

+ 添加项目
+ 添加分类
+ 添加接口



------------------------------



## 四、前端工程化

之前在文件夹中一个一个创建 html 文件是小白眼中的前端开发，没有规范化的存储目录，所以在现在的前端开发中都讲究前端开发的模块化、组件化、规范化、自动化

<img src="./assets/image-20250605203647562.png" alt="image-20250605203647562" style="zoom:50%;" />

**前端工程化**：是指在企业级的前端项目开发中，把前端开发所需的工具、技术、流程、经验等进行规范化、标准化

### 1. 环境准备

+ 介绍：Vue-cli 是 Vue 官方提供的一个脚手架，用于快速生成一个 Vue 的项目模板
+ Vue-cli 提供了如下功能：
  + 统一的目录结构
  + 本地调试
  + 热部署
  + 单元测试
  + 集成打包上线
+ 依赖环境：NodeJS

##### 1.1 安装 Node.js

官网：[下载 | Node.js 中文网](https://nodejs.cn/download/)

1. 双击安装包

<img src="./assets/image-20250605205002933.png" alt="image-20250605205002933" style="zoom:50%;" />

2. 选择安装目录

选择安装到一个，没有中文，没有空格的目录下（新建一个文件夹 NodeJS）

<img src="./assets/image-20250605205100254.png" alt="image-20250605205100254" style="zoom:50%;" />

<img src="./assets/image-20250605205148296.png" alt="image-20250605205148296" style="zoom:50%;" />

3. 验证 NodeJS 环境变量

NodeJS 安装完毕后，会自动配置好环境变量，我们验证一下是否安装成功，通过：`node -v`

<img src="./assets/image-20250605205323242.png" alt="image-20250605205323242" style="zoom:50%;" />

4. 配置 npm 的全局安装路径

<img src="./assets/image-20250605205549573.png" alt="image-20250605205549573" style="zoom:50%;" />

使用管理员身份运行命令行，在命令行中，执行如下指令：

```cmd
npm config set prefix "D:\nodejs\22.14.0\node_global"
```

注意：D:\nodejs\22.14.0\node_global 这个目录是 NodeJS 的安装目录

<img src="./assets/image-20250605205847817.png" alt="image-20250605205847817" style="zoom:50%;" />

5. 切换 npm 的淘宝镜像

使用管理员身份运行命令行，在命令行中，执行如下指令：

```cmd
npm config set registry https://registry.npmmirror.com/
```

验证 npm 镜像源是否切换成功

```cmd
npm config get registry
```


6. 安装 Vue-cli

使用管理员身份运行命令行，在命令行中，执行如下命令：

```cmd
npm install -g @vue/cli
```

这个过程中，会联网下载，可能会耗时几分钟，耐心等待

<img src="./assets/image-20250605211926859.png" alt="image-20250605211926859" style="zoom:50%;" />



-----------------------



### 2. Vue 项目简介

#### 2.1 使用 vue/cli

+ 命令行：`vue create vue-project01`
+ 图像化界面：`vue ui`

<img src="./assets/image-20250605212840526.png" alt="image-20250605212840526" style="zoom:50%;" />

<img src="./assets/image-20250605212817204.png" alt="image-20250605212817204" style="zoom:50%;" />

<img src="./assets/image-20250605212925349.png" alt="image-20250605212925349" style="zoom:50%;" />

<img src="./assets/image-20250605213027345.png" alt="image-20250605213027345" style="zoom:50%;" />

<img src="./assets/image-20250605213114313.png" alt="image-20250605213114313" style="zoom:50%;" />

<img src="./assets/image-20250605213209155.png" alt="image-20250605213209155" style="zoom:50%;" />

<img src="./assets/image-20250605213326423.png" alt="image-20250605213326423" style="zoom:50%;" />

**报错就用管理员身份运行**

<img src="./assets/image-20250605214238589.png" alt="image-20250605214238589" style="zoom:50%;" />

#### 2.2 使用 vite

在要安装的目录的命令行输入
```
npm init vue@latest
```
+ 如果报错就用管理员运行

这一指令将会安装并执行 `create-vue`，它是 Vue 官方的项目脚手架工具。你将会看到一些诸如 TypeScript 和测试支持之类的可选功能提示

<img src="./assets/image-20250605214659101.png" alt="image-20250605214659101" style="zoom:50%;" />

+ cnpm 是 npm 的镜像，安装速度更快

<img src="./assets/image-20250226200412942-1749131251850-5.png" alt="image-20250226200412942" style="zoom:50%;" />

复制浏览器地址进入浏览器访问它

<img src="./assets/image-20250226200509442-1749131261837-8.png" alt="image-20250226200509442" style="zoom:50%;" />

项目就创建成功了

#### 2.3 Vue 项目 - 目录结构

+ 基于 Vue 脚手架创建出来的工程，有标准的目录结构，如下：

<img src="./assets/image-20250605214859637.png" alt="image-20250605214859637" style="zoom:50%;" />

<img src="./assets/image-20250605215116512.png" alt="image-20250605215116512" style="zoom:50%;" />

#### 2.4 Vue 项目 - 启动

+ 方式一：图形化界面

<img src="./assets/image-20250605215402755.png" alt="image-20250605215402755" style="zoom:50%;" />

+ 方式二：命令行

在终端输入：

```cmd
npm run serve
```

<img src="./assets/image-20250702164514654.png" alt="image-20250702164514654" style="zoom:50%;" />

#### 2.5 Vue 项目 - 配置端口

+ vue.config.js

<img src="./assets/image-20250702164810679.png" alt="image-20250702164810679" style="zoom:50%;" />

```javascript
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    port: 7000
  }
})

```

<img src="./assets/image-20250702164957503.png" alt="image-20250702164957503" style="zoom:50%;" />



-------------------------



### 3. Vue 项目开发流程

我们现在访问到的页面是 Vue 项目默认的首页 **index.html**

<img src="./assets/image-20250702165229770.png" alt="image-20250702165229770" style="zoom:50%;" />

在 index.html 中默认是引入了入口文件 main.js 的

<img src="./assets/image-20250702165317013.png" alt="image-20250702165317013" style="zoom:50%;" />

+ `import` 代表的是引入模块
+ `export` 是将对象或者是函数导出为模块
+ `router` 路由
+ `render` 是一个函数，是将上面导入进来的 App 当中所定义的视图创建出对应的虚拟 DOM 元素，然后挂载到 #app 这个区域

等价于：

<img src="./assets/image-20250702165933817.png" alt="image-20250702165933817" style="zoom:50%;" />



+ Vue 的组件文件以 `.vue` 结尾，每个组件文件由三个部分组成：<template>、<script>、<style>
  + `<template>`：模板部分，用来生成 html 代码的，也就在说在 template 当中可以定义原生的 html 代码
  + `<script>`：里面定义的是 js 代码，主要是用来控制模板当中的数据来源以及行为
  + `<style>`：控制 css 样式的

```vue
<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Hello Vue"
    }
  },
  methods: {

  }
}
</script>

<style></style>

```



-----------------------------



## 五、Vue 组件库 Element

什么是 Element？

+ Element：是饿了么团队研发的，一套为开发者、设计师和产品经理准备的基于 Vue2.0 的桌面端**组件**库
+ 组件：组成网页的部件，例如：超链接、按钮、图片、表格、表单、分页条等等
+ 官网：[Element - 网站快速成型工具](https://element.eleme.cn/#/zh-CN)

### 1. 快速入门

+ 安装 ElementUI 组件库（在当前工程下），在命令行执行指令：
  + 报错的话用管理员身份运行

```cmd
npm install element-ui@2.15.3
```

```cmd
npm i element-ui -S 
```

+ 引入 ElementUI 组件库
  + main.js

```javascript
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);
```

+ 访问官网，复制组件码，调整

#### 1.1 操作演示

<img src="./assets/image-20250702173924302.png" alt="image-20250702173924302" style="zoom:50%;" />

+ 在 **node_modules** 文件夹下有 element-ui 文件即为安装成功

<img src="./assets/image-20250702174024901.png" alt="image-20250702174024901" style="zoom:50%;" />

+ 在 **main.js** 中写入如下内容：

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'
// 引入ElementUI组件
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.config.productionTip = false
Vue.use(ElementUI); // 代表要使用这个组件

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')

```

+ 在 **views** 文件夹下创建 .vue 文件

<img src="./assets/image-20250702174601277.png" alt="image-20250702174601277" style="zoom:67%;" />

+ 在网站中复制代码

<img src="./assets/image-20250702174654895.png" alt="image-20250702174654895" style="zoom:50%;" />

+ views/element/ElementView.vue

```vue
<template>
    <div>
        <!-- button按钮 -->
        <el-row>
            <el-button>默认按钮</el-button>
            <el-button type="primary">主要按钮</el-button>
            <el-button type="success">成功按钮</el-button>
            <el-button type="info">信息按钮</el-button>
            <el-button type="warning">警告按钮</el-button>
            <el-button type="danger">危险按钮</el-button>
        </el-row>
    </div>
</template>

<script>
export default {

}
</script>

<style></style>
```

+ Vue.app

```vue
<template>
  <div>
    <!-- <h1>{{ message }}</h1> -->
    <element-view></element-view>
  </div>
</template>

<script>
import ElementView from './views/element/ElementView.vue'
export default {
  components: { ElementView },
  data() {
    return {
      message: "Hello Vue"
    }
  },
  methods: {

  }
}
</script>

<style></style>

```

+ 效果

<img src="./assets/image-20250702175314776.png" alt="image-20250702175314776" style="zoom:50%;" />



--------------------------------------



### 2. 常见组件

**就是在 Element 组件官网复制粘贴**

#### 2.1 常见组件 - 表格

+ Table 表格：用于展示多条结构类似的数据，可对数据进行排序、筛选、对比或其他自定义操作

<img src="./assets/image-20250710182452615.png" alt="image-20250710182452615" style="zoom:50%;" />

```vue
<template>
    <div>
        <!-- button按钮 -->
        <el-row>
            <el-button>默认按钮</el-button>
            <el-button type="primary">主要按钮</el-button>
            <el-button type="success">成功按钮</el-button>
            <el-button type="info">信息按钮</el-button>
            <el-button type="warning">警告按钮</el-button>
            <el-button type="danger">危险按钮</el-button>
        </el-row>

        <br>

        <!-- Table表格 -->
        <el-table :data="tableData" border style="width: 100%">
            <el-table-column prop="date" label="日期" width="180">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="180">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tableData: [{
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-04',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1517 弄'
            }, {
                date: '2016-05-01',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1519 弄'
            }, {
                date: '2016-05-03',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1516 弄'
            }]
        }
    }

}
</script>

<style></style>
```



------------------------------



#### 2.2 常见组件 - 分页

+ Pagination 分页：当数据量过多时，使用分页分解数据
  + 各种用到的属性、事件可以划到网页下方查看其作用

<img src="./assets/image-20250710182507970.png" alt="image-20250710182507970" style="zoom:50%;" />

```vue
<template>
    <div>
        <!-- Pagination分页 -->
        <el-pagination background layout="sizes, prev, pager, next, jumper, total" @size-change="handleSizeChange"
            @current-change="handleCurrentChange" :total="1000">
        </el-pagination>
    </div>
</template>

<script>
export default {
    data() {
        return {}
}
</script>

<style></style>
```



--------------------------



#### 2.3 常见组件 - 对话框

+ Dialog 对话框：在保留当前页面状态的情况下，告知用户并承载相关操作

<img src="./assets/image-20250710182521222.png" alt="image-20250710182521222" style="zoom:50%;" />

```vue
<template>
    <div>
        <!-- Table -->
        <el-button type="text" @click="dialogTableVisible = true">打开嵌套表格的 Dialog</el-button>

        <el-dialog title="收货地址" :visible.sync="dialogTableVisible">
            <el-table :data="gridData">
                <el-table-column property="date" label="日期" width="150"></el-table-column>
                <el-table-column property="name" label="姓名" width="200"></el-table-column>
                <el-table-column property="address" label="地址"></el-table-column>
            </el-table>
        </el-dialog>

    </div>
</template>

<script>
export default {
    data() {
        return {
            gridData: [{
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-04',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-01',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-03',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }],
            dialogTableVisible: false,
</script>

<style></style>
```



------------------------



#### 2.4 常见组件 - 表单

+ Form 表单：由输入框、选择器、单选框、多选框等控件组成，用以收集、校验、提交数据

<img src="./assets/image-20250710183601499.png" alt="image-20250710183601499" style="zoom:50%;" />

```vue
<template>
    <div>
        <!-- Dialog对话框 - Form表单 -->
        <el-button type="text" @click="dialogFormVisible = true">打开嵌套 Form 的 Dialog</el-button>

        <el-dialog title="Form 表单" :visible.sync="dialogFormVisible">
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="活动名称">
                    <el-input v-model="form.name"></el-input>
                </el-form-item>
                <el-form-item label="活动区域">
                    <el-select v-model="form.region" placeholder="请选择活动区域">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="活动时间">
                    <el-col :span="11">
                        <el-date-picker type="date" placeholder="选择日期" v-model="form.date1"
                            style="width: 100%;"></el-date-picker>
                    </el-col>
                    <el-col class="line" :span="2">-</el-col>
                    <el-col :span="11">
                        <el-time-picker placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
                    </el-col>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">提交</el-button>
                    <el-button>取消</el-button>
                </el-form-item>
            </el-form>
        </el-dialog>

    </div>
</template>

<script>
export default {
    data() {
        return {
            form: {
                name: '',
                region: '',
                date1: '',
                date2: '',
            },
        }
    },
    methods: {
        onSubmit: function () {
            alert(JSON.stringify(this.form));
        }
    }
}
</script>

<style></style>
```



----------------------------------



### 3. 案例

根据页面原型完成员工管理页面开发，并通过 Axios 完成数据异步加载

<img src="./assets/image-20250713151135804.png" alt="image-20250713151135804" style="zoom:50%;" />

步骤：

+ 创建页面，完成页面的整体布局规划
+ 布局中各个部分的组件实现
+ 列表数据的异步加载，并渲染展示

在 Vue 项目中使用 Axios：

+ 在项目目录下安装 axios：`npm install axios`
  + 报错就使用管理员身份运行
+ 需要使用 axios 时，导入 axios：`import axios from 'axios'`

#### 代码演示

```vue
<template>
    <div>
        <el-container style="height: 700px; border: 1px solid #eee">
            <el-header style="font-size: 40px; background-color: rgb(238, 241, 246)">Feng 智能学习辅助系统</el-header>
            <el-container>
                <el-aside width="200px" style="border: 1px solid #eee">
                    <el-menu :default-openeds="['1', '3']">
                        <el-submenu index="1">
                            <template slot="title"><i class="el-icon-message"></i>系统信息管理</template>
                            <el-menu-item index="1-1">部门管理</el-menu-item>
                            <el-menu-item index="1-2">员工管理</el-menu-item>
                        </el-submenu>
                    </el-menu>
                </el-aside>
                <el-main>
                    <!-- 表单 -->
                    <el-form :inline="true" :model="searchForm" class="demo-form-inline">
                        <el-form-item label="姓名">
                            <el-input v-model="searchForm.name" placeholder="姓名"></el-input>
                        </el-form-item>

                        <el-form-item label="性别">
                            <el-select v-model="searchForm.gender" placeholder="性别">
                                <el-option label="男" value="1"></el-option>
                                <el-option label="女" value="2"></el-option>
                            </el-select>
                        </el-form-item>

                        <el-form-item label="入职日期">
                            <!-- 日期选择器 -->
                            <el-date-picker v-model="searchForm.entrydate" type="daterange" range-separator="至"
                                start-placeholder="开始日期" end-placeholder="结束日期">
                            </el-date-picker>
                        </el-form-item>

                        <el-form-item>
                            <el-button type="primary" @click="onSubmit">查询</el-button>
                        </el-form-item>
                    </el-form>
                    <!-- 表格 -->
                    <el-table :data="tableData" border>
                        <el-table-column prop="name" label="姓名" width="180">
                        </el-table-column>
                        <el-table-column label="图像" width="180">
                            <template slot-scope="scope">
                                <img :src="scope.row.image" width="100px" height="70px">
                            </template>
                        </el-table-column>
                        <el-table-column label="性别" width="140">
                            <template slot-scope="scope">
                                {{ scope.row.gender == 1 ? '男' : '女' }}
                            </template>
                        </el-table-column>
                        <el-table-column prop="job" label="职位" width="140">
                        </el-table-column>
                        <el-table-column prop="entrydate" label="入职时间" width="180">
                        </el-table-column>
                        <el-table-column prop="updatetime" label="最后操作时间" width="230">
                        </el-table-column>
                        <el-table-column>
                            <el-button type="primary" size="mini">编辑</el-button>
                            <el-button type="danger" size="mini">删除</el-button>
                        </el-table-column>
                    </el-table>

                    <br>

                    <!-- 分页条 -->
                    <el-pagination background layout="sizes, prev, pager, next, jumper, total"
                        @size-change="handleSizeChange" @current-change="handleCurrentChange" :total="1000">
                    </el-pagination>
                </el-main>
            </el-container>
        </el-container>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            tableData: [],
            searchForm: {
                name: "",
                gender: "",
                entrydate: [],
            }
        }
    },
    methods: {
        onSubmit: function () {
            alert("查询数据")
        },
        handleSizeChange: function (val) {
            alert("每页记录数变化" + val)
        },
        handleCurrentChange: function (val) {
            alert("页码发生变化" + val)
        },
    },
    mounted() {
        // 发送异步请求，获取数据
        axios.get("url地址").then((result) => {
            this.tableData = result.data.data;
        });
    }
}
</script>

<style></style>
```



----------------------------



## 六、Vue 路由

前端路由：由 URL 中的 hash（#号）与组件之间的对应关系

### 1. Vue Router

+ 介绍：Vue Router 是 Vue 的官方路由
+ 组成：
  + VueRouter：路由器类，根据路由请求在路由视图中动态渲染选中的组件
  + <router-link>：请求链接组件，路由器会解析成 <a>
  + <router-view>：动态视图组件，用来渲染展示与路由器路径对应的组件

eg：

```
/user : UserView.vue
/emp : EmpView.vue
/order : OrderView.vue
```

<img src="./assets/image-20250713161151764.png" alt="image-20250713161151764" style="zoom:50%;" />

+ 安装**（创建 Vue 项目时已选择）**

```cmd
npm install vue-router 
```

+ 定义路由

<img src="./assets/image-20250713162313035.png" alt="image-20250713162313035" style="zoom:50%;" />

### 2. 案例：通过 Vue 的路由 VueRouter 完成左侧菜单栏点击切换效果

```vue
<router-link to="/dept">部门管理</router-link>

<router-link to="/emp">员工管理</router-link>
```

在对应的区域加上标签 router-view 来制定我们要动态展示哪个组件（本案例中在 App.vue 中加上即可）

```vue
<router-view></router-view>
```



-------------------------



## 七、打包部署

### 1. 打包

<img src="./assets/image-20250713162513687.png" alt="image-20250713162513687" style="zoom:50%;" />

或者终端输入：

```cmd
npm run build
```

打包完成后出现 **dist 目录**

<img src="./assets/image-20250713162627362.png" alt="image-20250713162627362" style="zoom:50%;" />

### 2. 部署

#### 2.1 Nginx

+ 介绍：Nginx 是一款轻量级的 Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。其特点是占有内存少，并发能力强，在各大型互联网公司都有非常广泛的使用
+ 官网：[nginx](https://nginx.org/)

<img src="./assets/image-20250713163003707.png" alt="image-20250713163003707" style="zoom:50%;" />

将其放在一个没有中文和空格的目录下

<img src="./assets/image-20250713163245068.png" alt="image-20250713163245068" style="zoom:50%;" />

+ conf：保存 nginx 的配置文件
+ html：存放静态资源文件的
+ logs：日志文件目录
+ temp：临时文件目录

#### 2.2 部署

+ 部署：将打包好的 dist 目录下的文件，复制到 nginx 安装目录的 html 目录下
+ 启动：双击 nginx.exe 文件即可，Nginx 服务器默认占用 80 端口号

注意：Nginx 默认占用80端口号，如果80端口号被占用，可以在 nginx.conf 中修改端口号（netstat -ano | findStr 80）

在命令行中输入 `netstat -ano | findStr 80` 可以查找当前系统中哪个进程占用了80端口

在 conf 中的 nginx.conf 可以更改端口号

<img src="./assets/image-20250713163851155.png" alt="image-20250713163851155" style="zoom:50%;" />



---------------------------------
