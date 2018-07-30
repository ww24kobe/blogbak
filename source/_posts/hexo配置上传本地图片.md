---
title: hexo配置上传本地图片
date: 2018-07-30 00:10:25
tags:
	- hexo 

---

**步骤1**: 把配置文件_config.yml里的post_asset_folder选项设置为true
```
post_asset_folder: true
```

**步骤2**: 在博客目录下执行`npm install hexo-asset-image --save` 安装一个可以上传本地图片的插件。 
来自：[CodeFalling-git](https://github.com/CodeFalling/hexo-asset-image)



安装好之后使用使用`hexo -n 'xxx' `创建文字的时候, 会在/source/_posts文件夹内除了xxx.md还有一个同名的文件夹 

**步骤3** ： 最后在XXX.md中想引入图片时，先把图片复制到xxx这个文件夹中，然后只需要在xxx.md中按照markdown的格式引入图片：

`![文字](图片名.png)`

生成文章 `hexo g` 

进入`public\2017\07\30\index.html`文件中查看相关字段，可以发现，html标签内的语句是`<img src="2017/07/30/xxx/图片名.jpg">`，而不是`<img src="图片名.jpg>`。这很重要，关乎你的网页是否可以真正加载你想插入的图片。





参考地址：

- https://blog.csdn.net/sugar_rainbow/article/details/57415705
- https://www.jianshu.com/p/c2ba9533088a



