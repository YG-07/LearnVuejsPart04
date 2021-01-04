# LearnVuejsPart04
学习和使用Vue CLI 脚手架
### 一.资料整理来源  
coderwhy老师  B站账号：ilovecoding  
bilibili URL：https://space.bilibili.com/36139192  
视频(95-p) URL：https://www.bilibili.com/video/BV15741177Eh?p=795 

# 二、本部分知识大纲
(数字表示视频URL分p)  
### 一、对比runtimecompiler和runtimeonly (95-)
#### 1.1 初始化2个项目
* 分别选择runtime+compiler和runtime-only  
* 先关闭Eslint规范在`config/index.js`里改成`useEslint: false` 
  
#### 1.2 Vue程序运行过程
* 1.英文过程解释
1. template parse >> ast
2. ast compiler >> render(function)
3. render() return >> virtual DOM
4. virtual DOM update >> UI
* 1.中文过程解释
1. 先将模板解析成抽象语法树(ast，abstract syntax tree)
2. 再将ast编译成render()函数
3. render()再返回虚拟DOM(文档对象模型，Document Object Model)
4. 最后将虚拟DOM更新到用户界面的成为真实DOM


