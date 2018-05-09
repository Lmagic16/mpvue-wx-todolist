## 小程序练手项目 —— mpvue-wx-todolist
利用 mpvue 编写的小程序
[小程序开发指南](https://developers.weixin.qq.com/ebook?action=get_post_info&token=935589521&volumn=1&lang=zh_CN&book=miniprogram&docid=0008aeea9a8978ab0086a685851c0a)
[mpvue文档](http://mpvue.com/)

### 项目结构
```
│  .babelrc
│  .editorconfig  //编辑器配置文件，代码格式化工具
│  .eslintignore  //eslint忽略文件配置
│  .eslintrc.js
│  .gitignore    //git 忽略文件配置
│  .postcssrc.js
│  index.html
│  package-lock.json
│  package.json
│  project.config.json   //项目配置文件，配置小程序appid
│  README.md
├─build
├─config
├─dist     //生成的小程序相关代码
│  │  app.js
│  │  app.json
│  │  app.wxss
│  ├─components
│  ├─pages   
│  └─static
│      ├─css
│      │  └─pages        
│      ├─icon
│      └─js           
├─src     //主要源码
│  │  App.vue
│  │  main.js     //入口 + 小程序里 app.json 配置
│  ├─components   公用组件，暂未使用
│  │      card.vue
│  ├─pages     //小程序页面
│  │  ├─addTodo
│  │  │      index.vue
│  │  │      main.js
│  │  ├─index
│  │  │      index.vue
│  │  │      main.js
│  │  ├─logs
│  │  │      index.vue
│  │  │      main.js
│  │  └─TodoDetail
│  │          index.vue
│  │          main.js   
│  └─utils     
└─static     //静态资源存放

```

### overview
![图一](https://upload-images.jianshu.io/upload_images/11791792-fd9324643f6b27b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/375)
![图二](https://upload-images.jianshu.io/upload_images/11791792-e9bcf9965a35eb52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/375)
![图三](https://upload-images.jianshu.io/upload_images/11791792-378425bd8498bd6c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/375)
![图4](https://upload-images.jianshu.io/upload_images/11791792-8e536af22b657ceb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/375)
![图5](https://upload-images.jianshu.io/upload_images/11791792-1812ac7b1f489e1b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/375)

## 如何运行

### 安装
$npm install

将文件 project.config.json 中的 appid 修改为自己小程序的 appid

### 启动
$npm run dev

### 预览
通过微信开发者工具打开本项目根目录（非 dist 目录）进行预览

### 构建
$npm run build

build for production with minification

## 小程序大致原理
[整理版本](https://github.com/Lmagic16/blog/issues/31)

## 问题记录
1. 页面构成，页面间如何跳转？
2. 页面跳转时如何传递数据？
3. 页面间如何共享数据？