Vue引入axios发送post请求后端接受不到数据，因为post发送的数据格式不正确，
---解决方法是URLSearchParams()是web的API
    Var p=new URLSearchParams()
    p.append(‘名称’，‘数值’)
    axios({
           data:p,
           url:’/usr/’,
           method:post
})

//搭建项目
http://blog.csdn.net/fly_home_ysc/article/details/77053415
vue-cli初始化
搭建node环境
vue-cli 是基于node环境的一个vue钩子框架，可让为开发者开发者快速的搭建一整套包含vue，ut等相关的配置。
首先需要安装node环境，可以直接到中文官网http://nodejs.cn/下载安装包。 
只是这样安装的 node 是固定版本的，如果需要多版本的 node，可以使用 nvm 安装http://blog.csdn.net/s8460049/article/details/52396399。（具体参看官网查看node 
的安装教程）。安装成功node后，我们可以打开node的cmd控制台，通过命令来查看node是否安装成功和node版本
node -v  //查看node的安装版本
npm -v  //查看npm的安装版本，npm 是包依赖额安装工具
安装vue-cli
安装好了node后，我们可以直接在控制台通过命令安装vue-cli
npm install -g vue-cli //-g 表示全局安装vue-cli
这种安装方式比较慢，推荐使用国内镜像来安装，所以我们先设置cnpm，在控制台安装cnpm 命令，安装成功后，我们也可以通过cnpm -v来查看对应的安装版本。
当然，如果安装失败，可以使用 npm cache clean 清理缓存，然后再重新安装。后面的安装过程中，如有安装失败的情况，也需要先清理缓存。
或者通过命令npm config set strict-ssl false关闭npm的https
npm config set strict-ssl false  //关闭npm的https
// npm cache clean 如果安装失败，请打开该注释，然后两句一起运行
npm install -g cnpm --registry=https://registry.npm.taobao.org
然后使用 cnpm 安装 vue-cli
cnpm install vue-cli -g
如果提示“无法识别 ‘vue’ ” ，有可能是 npm 版本过低，可以使用 npm install -g npm 来更新版本
npm install -g npm //升级npm的版本到最新版
•	1
初始化项目
然后，我们就可以通过vue init webpack Vue-Project来初始化项目。webpack 是模板名称，可以到 vue.js 的 GitHub 上查看更多的模板https://github.com/vuejs-templates，Vue-Project是项目的名字，自定义即可。命令执行之后，会在当前目录生成一个以该名称命名的项目文件夹
vue init webpack Vue-Project //Vue-Project是项目的名字，自定义即可
在初始化的过程中会询问初始化一些相关的说明和配置，相关的说明均会写入package.json文件中，先关配置会自动生成对应的模块。 
 
其中，如果需要使用ESLint规范和相关的unit test 和e2e，请输入yes，这样初始化出来的项目，会自动配置好对应的模块。
安装完成后，然后进入项目目录（cd Vue-Project ），使用 cnpm（或者npm） 安装依赖，然后启动项目
// install dependencies
npm install 

// serve with hot reload at localhost:8080
npm run dev

// build for production with minification
npm run build

// build for production and view the bundle analyzer report
npm run build --report

// run unit tests
npm run unit

// run e2e tests
npm run e2e

// run all tests
npm test
如果浏览器打开之后，没有加载出页面，有可能是本地的 8080 端口被占用，需要修改一下配置文件 config>index.js，修改对应的端口
项目测试
在自己编写的项目中，运行eslint的保存信息的时候，可自行查看报错信息，然后对应进行解决，如果发现对应的规则与自己的习惯不一致，可参看下面的那个ESLint的学习资料进行相关的配置，比如去掉文件最后的一行空白，将缩进空格改为4个等。
'rules': {
    // no-var
    'no-var': 'error',
    // 要求或禁止 var 声明中的初始化
    'init-declarations': 2,
    // 强制使用单引号
    'quotes': ['error', 'single'],
    // 要求或禁止使用分号而不是 ASI
    'semi': ['error', 'never'],
    // 禁止不必要的分号
    'no-extra-semi': 'error',
    // 强制使用一致的换行风格
    'linebreak-style': ['error', 'unix'],
    // 空格2个
    'indent': ['error', 2, {'SwitchCase': 1}],
    // 指定数组的元素之间要以空格隔开(,后面)， never参数：[ 之前和 ] 之后不能带空格，always参数：[ 之前和 ] 之后必须带空格
    'array-bracket-spacing': [2, 'never'],
    // 在块级作用域外访问块内定义的变量是否报错提示
    'block-scoped-var': 0,
    // if while function 后面的{必须与if在同一行，java风格。
    'brace-style': [2, '1tbs', {'allowSingleLine': true}],
    // 双峰驼命名格式
    'camelcase': 2,
    // 数组和对象键值对最后一个逗号， never参数：不能带末尾的逗号, always参数：必须带末尾的逗号， 
    'comma-dangle': [2, 'never'],
    // 控制逗号前后的空格
    'comma-spacing': [2, {'before': false, 'after': true}],
    // 控制逗号在行尾出现还是在行首出现
    'comma-style': [2, 'last'],
    // 圈复杂度
    'complexity': [2, 9],
    // 以方括号取对象属性时，[ 后面和 ] 前面是否需要空格, 可选参数 never, always
    'computed-property-spacing': [2, 'never'],
    // TODO 关闭 强制方法必须返回值，TypeScript强类型，不配置
    // 'consistent-return': 0
  }
参考ESLint入门的资料：http://blog.csdn.net/walid1992/article/details/54633760
打包上线
自己的项目文件都需要放到 src 文件夹下，相关的部分静态资源需要放在static文件夹下（建议使用less或者sass的方式来进行css的预处理，可以保证对应的静态资源都进行打包）
项目开发完成之后，可以输入 npm run build 来进行打包工作
npm run build
注意的问题：
1、有时候可能会提示图片资源过大，可以采用网站：https://tinypng.com 来将图片压缩一下 
2、出现报错信息 xxx/xxx/aaxxx.js from UglifyJs Unexpected token: punc (())的时候，是因为项目中没有.babelrc文件或者没有配置.babelrc文件。需要在项目的根目录新增一个文件.babelrc，然后配置：
{
  "presets": [
    "es2015"
  ]
}
3、如果出现错误：Couldn’t find preset “es2015” relative to directory的错误，是因为没有安装依赖包：babel-preset-es2015或者安装的失败，需要重新安装。
npm install babel-preset-es2015 --save-dev 
//--save表示将对应的依赖写入package.json中的dependencies生成模块中，--save-dev表示将对应的依赖写入package.json中的devDependencies开发模块中
4、需要将代码打包成es5模式的代码，还需要在build文件夹中webpack.base.conf.js文件的module版块中加入如下代码：
module: {
        loaders: [
            {
                test: /\.js$/,
                exclude: /(node_modules|bower_components)/,
                loader: 'babel',
                query: {
                    presets: ['es2015']
                }
            }
        ]
    }
打包完成后，会生成 dist 文件夹，如果已经修改了文件路径，可以直接打开本地文件查看
项目上线时，只需要将 dist 文件夹放到服务器就行了。




//面试题
一、一个页面上两个div左右铺满整个浏览器，要保证左边的div一直为100px，右边的div跟随浏览器大小变化（比如浏览器为500，右边div为400，浏览器为900，右边div为800），请写出大概的css代码。
1.使用flex
//html
<div class='box'><div class='left'></div> <div class='right'></div></div>

//css
.box {
    width: 400px;
    height: 100px;
    display: flex;
    flex-direction: row;
    align-items: center;
    border: 1px solid #c3c3c3;
}
.left {
    flex-basis：100px;
    -webkit-flex-basis: 100px;
    /* Safari 6.1+ */
    background-color: red;
    height: 100%;
}
.right {
    background-color: blue;
    flex-grow: 1;
}
2.浮动布局
原理是： 浮动的元素脱离了正常的文档流，并且失去了块级元素的特性，不在独占一行，右面的元素设置margin-left的值之后就会和左面的元素在同一行
<div id="left">Left sidebar</div>
<div id="content">Main Content</div>

<style type="text/css">
* {
    margin: 0;
    padding: 0;
}
#left {
    float: left;
    width: 220px;
    background-color: green;
}
#content {
    background-color: orange;
    margin-left: 220px;
    /*==等于左边栏宽度==*/
}
</style>
二、请写出一些前端性能优化的方式，越多越好
1.减少dom操作
2.部署前，图片压缩，代码压缩
3.优化js代码结构，减少冗余代码
4.减少http请求，合理设置 HTTP缓存
5.使用内容分发cdn加速
6.静态资源缓存
7.图片延迟加载
三、一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）
输入地址
1.浏览器查找域名的 IP 地址
2.这一步包括 DNS 具体的查找过程，包括：浏览器缓存->系统缓存->路由器缓存…
3.浏览器向 web 服务器发送一个 HTTP 请求
4.服务器的永久重定向响应（从 http://example.com 到 http://www.example.com）
5.浏览器跟踪重定向地址
6.服务器处理请求
7.服务器返回一个 HTTP 响应
8.浏览器显示 HTML
9.浏览器发送请求获取嵌入在 HTML 中的资源（如图片、音频、视频、CSS、JS等等）
10.浏览器发送异步请求
四、请大概描述下页面访问cookie的限制条件
跨域问题
设置了HttpOnly
五、描述浏览器重绘和回流，哪些方法能够改善由于dom操作产生的回流
1.直接改变className，如果动态改变样式，则使用cssText
// 不好的写法
var left = 1;
var top = 1;
el.style.left = left + "px";
el.style.top = top + "px"; // 比较好的写法
el.className += " className1";
// 比较好的写法
el.style.cssText += ";
left: " + left + "px;
top: " + top + "px;";
2.让要操作的元素进行”离线处理”，处理完后一起更新
a) 使用DocumentFragment进行缓存操作,引发一次回流和重绘；
b) 使用display:none技术，只引发两次回流和重绘；
c) 使用cloneNode(true or false) 和 replaceChild 技术，引发一次回流和重绘
六、vue生命周期钩子
1.	beforcreate
2.	created
3.	beformount
4.	mounted
5.	beforeUpdate
6.	updated
7.	actived
8.	deatived
9.	beforeDestroy
10.	destroyed
七、js跨域请求的方式，能写几种是几种
1、通过jsonp跨域
2、通过修改document.domain来跨子域
3、使用window.name来进行跨域
4、使用HTML5中新引进的window.postMessage方法来跨域传送数据（ie 67 不支持）
5、CORS 需要服务器设置header ：Access-Control-Allow-Origin。
6、nginx反向代理 这个方法一般很少有人提及，但是他可以不用目标服务器配合，不过需要你搭建一个中转nginx服务器，用于转发请求
八、对前端工程化的理解
开发规范 模块化开发 组件化开发 组件仓库 性能优化 项目部署 开发流程 开发工具
九, js深度复制的方式
1.使用jq的$.extend(true, target, obj)
2.newobj = Object.create(sourceObj)，// 但是这个是有个问题就是 newobj的更改不会影响到 sourceobj但是 sourceobj的更改会影响到newObj
3.newobj = JSON.parse(JSON.stringify(sourceObj))
十、js设计模式
总体来说设计模式分为三大类：
创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。 结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。 行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模
十一、图片预览
<input type="file" name="file" onchange="showPreview(this)" />
<img id="portrait" src="" width="70" height="75">

function showPreview(source) {
  var file = source.files[0];
  if(window.FileReader) {
      var fr = new FileReader();
      fr.onloadend = function(e) {
        document.getElementById("portrait").src = e.target.result;
      };
      fr.readAsDataURL(file);
  }
}
十二、扁平化多维数组
1、老方法
var result = []
function unfold(arr){
     for(var i=0;i< arr.length;i++){
      if(typeof arr[i]=="object" && arr[i].length>1) {
       unfold(arr[i]);
     } else {        
       result.push(arr[i]);
     }
  }
}
var arr = [1,3,4,5,[6,[0,1,5],9],[2,5,[1,5]],[5]];
unfold(arr)
2、使用tostring
var c=[1,3,4,5,[6,[0,1,5],9],[2,5,[1,5]],[5]];
var b = c.toString().split(',')
3、使用es6的reduce函数
var arr=[1,3,4,5,[6,[0,1,5],9],[2,5,[1,5]],[5]];
const flatten = arr => arr.reduce((a, b) => a.concat(Array.isArray(b) ? flatten(b) : b), []);
var result = flatten(arr)
十三、iframe有那些缺点？
iframe会阻塞主页面的Onload事件； 搜索引擎的检索程序无法解读这种页面，不利于SEO; iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。 使用iframe之前需要考虑这两个缺点。如果需要使用iframe，最好是通过javascript动态给iframe添加src属性值，这样可以绕开以上两个问题。

