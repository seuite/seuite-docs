# 如何创建自己的主页

## 硬件环境部分

最简单的方法是使用GitHub Pages，或是自己购买一个vps/使用24小时开机的闲置电脑，当然你也可以把它托管在我们的服务器上

### 购买vps
待补充
### 托管给我们
待完善

## 软件编写部分

如果你具有编程基础，或是愿意学习一点点命令行操作，我推荐你使用[Hexo](#hexo)来生成你自己的主页

如果你认为命令行对于你而言难度过大，但是愿意学习一些[Markdown文档](http://wiki.seu.services/guide/OneMinuteGoMarkdown)的使用，你也可以使用[Docute](#docute)来生成自己的主页

如果你觉得命令行难度太大，同时也觉得学习markdown负担过重，没关系，你可以直接到我们的[wiki](http://wiki.seu.services/club)合适的页面上创建一个你自己的页面，使用我们的可视化编辑器来进行编辑！

### Hexo
Hexo 是一个静态页面生成器，适合简单的展示使用，这是官方[主页](https://hexo.io)和[文档](https://hexo.io/docs)，事实上SEUITE的[主页](https://seu-ite.github.io)就是使用hexo自动生成的

你只需要
```bash
    npm install hexo-cli -g
    hexo init blog
    cd blog
    npm install
    hexo server
```
即刻拥有自己博客！

### Docute
Docute也是一个网站生成器，但是它比hexo更轻，更简单！这是官方[主页](https://docute.org/zh/)，它也就是文档！这个[站点](http://docs.seu.services)就是用docute生成的
创建一个index.html文件，然后输入以下内容：
```html
<!DOCTYPE>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <title>My Docs</title>
    <link rel="stylesheet" href="https://unpkg.com/docute@4/dist/docute.css">
  </head>
  <body>
    <div id="docute"></div>
    <script src="https://unpkg.com/docute@4/dist/docute.js"></script>
    <script>
      new Docute({
        target: '#docute'
      })
    </script>
  </body>
</html>
```
然后和你的md一起部署到硬件环境上就可以了！

