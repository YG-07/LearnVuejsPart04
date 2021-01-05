# LearnVuejsPart04
学习和使用Vue CLI 脚手架
### 一.资料整理来源  
coderwhy老师  B站账号：ilovecoding  
bilibili URL：https://space.bilibili.com/36139192  
视频(95-p) URL：https://www.bilibili.com/video/BV15741177Eh?p=95 

# 二、本部分知识大纲
(数字表示视频URL分p)  
### 一、对比runtimecompiler和runtimeonly (95-96)
#### 1.1 初始化2个项目
使用指令：`vue init webpack 项目名`  
* 分别选择`runtime+compiler(运行时+编译器)`和`runtime-only(只含有运行时)`模式创建  
* 关闭Eslint规范在`config/index.js`里改成`useEslint: false` 
  
#### 1.2 Vue程序基本运行过程
* 1.英文过程解释
1. template parse >> ast
2. ast compiler >> render(function)
3. render() return >> virtual DOM
4. VDOM update >> UI
* 1.中文过程解释
1. 先将模板解析成抽象语法树(ast，abstract syntax tree)
2. 再将ast编译成render()函数
3. render()再返回虚拟DOM(文档对象模型，Document Object Model)
4. 最后将虚拟DOM更新到用户界面的真实DOM
  
 #### 1.3 对比区别
 1. main.js的Vue实例
 * rc导入组件方式：`components: { App }, template: '<App/>'`  
 * ro导入组件方式：`render: h => h(App)` ，相当于：
 ```javaScript
  render:function (h) {
    return h(App)
  }
 ```  
 2. 编译过程
 * rc过程：`template -> ast -> render -> vdom -> UI`  
 * ro过程：`render -> vdom -> UI`  
 总结：  
 1. runtime-only性能更高
 2. runtime-only代码量更少(因此runtime-only更加实用)

#### 1.4 认识render函数
render函数博客 URL：https://baijiahao.baidu.com/s?id=1603797081408586727
可以删掉components和template属性  
```javaScript
render: function (createElement) {
    //1.普通用法：createElement('标签名',{属性对象},['内容',其他参数])
    return createElement('h2',{class: 'box'}, 
    ['Hello World', createElement('button', ['按钮'])])
    // 2.组件用法:
    // return createElement(cpn)
}
```
#### 1.5 对于组件里的template
导入之后由`vue-template-compiler`插件自动将template转换成render()  

### 二、Vue CLI3的创建和使用 (97-98)
#### 2.1 认识Vue CLI3
vue-cli3与2版本有很大区别：  
* vue-cli3是基于webpack 4打造，vue-cli2还是webapck 3
* vue-cli3的设计原则是“0配置”，移除的配置文件根目录下的build和config等目录
* vue-cli3提供了vue ui命令，提供了可视化配置，更加人性化
* 移除了static文件夹，新增了public文件夹，并且index.html移动到public中

#### 2.2 创建Vue CLI3
使用指令：`vue create 项目名`  
配置项目：
1. 手动选择特性Manually select features(按空格选择和取消)
2. 特性有：**Babel、TypeScript、Progressive Web App (PWA) Support、Router、Vuex、CSS Pre-processors、Linter / Formatter、Unit Testing、E2E Testing**等
3. 配置文件夹In dedicated config files
4. 保存为一个预设方案,Yes,如:coderwhy
5. 选择NPM或Yarn(新版本可能没有)
  
* 若想**删除自定义预设**，在`C:\Users\Administrator\.vuerc`文件里修改删除(rc后缀run command，终端运行，Linux命名)
#### 2.3 Vue CLI3项目的目录结构
明显在Vue CLI2基础上，简化了很多  
* node_modules，node的模块
* public文件夹，相当于static静态文件
* src资源文件夹
* .gitignore上传仓库忽略文件
* babel.config.js，Babel将ES6编译成ES5
* package.json，简化了配置cli-service间接管理
* package-lock.json，配置的缓存文件

#### 2.4 编译运行项目
运行：`npm run serve` ，发布：`npm run build`  
* 在Vue构造函数时，如果没有没有el属性时，可以使用`.$mount('#app')`进行手动挂载。
```javaScript
new Vue({
  render: h => h(App),
}).$mount('#app')
```
#### 2.5 Vue CLI3的配置文件查看和修改
* 在项目CMD里使用：`vue ui`打开网页版插件管理工具，点击**导入**项目文件夹

#### 2.6 箭头函数的使用和this指向
#### 2.6.1 定义函数的方式：  
1. 直接function
```javaScript
const aaa = function () {}
```
2. 对象字面量里定义
```javaScript
const obj = {
  bbb: function () {},
  bb() {}
}
```
3. ES6箭头函数
```javaScript
//一个参数可以省略括号
const power = num => { return num * num }
//只有一行代码可以省略return关键字
const sum = (num1, num2) => num + num 
```
* 箭头函数应用，如：定时器或其他函数作为参数时
```javaScript
setTimeout(() => {}, 100)
```
#### 2.6.2 箭头函数中的this
* 箭头函数的this例子：
```javaScript
const obj = {
  aaa() {
    setTimeout(function () {
      console.log(this) //window
    })
    setTimeout(() => {
      console.log(this) //obj对象
    })
  }
}
```
结论：`箭头函数的this是向外层作用域中，一层层查找this，直到有this的定义`  

