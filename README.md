# LearnVuejsPart04
学习和使用Vue CLI 脚手架
### 一.资料整理来源  
coderwhy老师  B站账号：ilovecoding  
bilibili URL：https://space.bilibili.com/36139192  
视频(95-p) URL：https://www.bilibili.com/video/BV15741177Eh?p=795 

# 二、本部分知识大纲
(数字表示视频URL分p)  
### 一、对比runtimecompiler和runtimeonly (95-96)
#### 1.1 初始化2个项目
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

### 二、Vue CLI3的创建和使用
#### 2.1 认识Vue CLI3
vue-cli3与2版本有很大区别：  
* vue-cli3是基于webpack 4打造，vue-cli2还是webapck 3
* vue-cli3的设计原则是“0配置”，移除的配置文件根目录下的build和config等目录
* vue-cli3提供了vue ui命令，提供了可视化配置，更加人性化
* 移除了static文件夹，新增了public文件夹，并且index.html移动到public中



