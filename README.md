    
    https://hexo.io/zh-cn/docs/github-pages.html
    
    Token:f4b639866c1feca3a6bfd8a7ca2a20ba4694f161
    
    npm install -g hexo

    hexo version

    hexo init nodejs-hexo

    cd nodejs-hexo

    hexo server

    http://blog.fens.me/hexo-blog-github/

---
    
### 目录

    ├── scaffolds                       脚手架，也就是一个工具模板
    ├── scripts                         写文件的js，扩展hexo的功能
    ├── source                          存放博客正文内容
    │   ├── _drafts                     草稿箱
    │   └── _posts                      文件箱
    ├── themes                          存放皮肤的目录
    │   └── landscape                   默认的皮肤
    └── _config.yml                     全局的配置文件

    在这里，我们每次用到的就是_posts目录里的文件，而_config.yml文件和themes目录是第一次配置好就行了。

    _posts目录：Hexo是一个静态博客框架，因此没有数据库。文章内容都是以文本文件方式进行存储的，直接存储在_posts的目录。Hexo天生集成了markdown，我们可以直接使用markdown语法格式写博客，例如:hello-world.md。新增加一篇文章，就在_posts目录，新建一个xxx.md的文件。

    themes目录：是存放皮肤的，包括一套Javascript+CSS样式和基于EJS的模板设置。通过在themes目录下，新建一个子目录，就可以创建一套新的皮肤，当然我们也可以直接在landscape上面修改。

---
### 命令行

    查看命令行帮助 hexo help

    创建新的文章 hexo new new_aritcle

    同时，网页的右侧还会出现Categories(目录)，Tags(标签)，Tag Cloud(标签云)的显示。

    我们在写文章时，有一些语法的要求。

    语法包括3部分：

    基本信息：标题，发布日期，分类目录，标签，类型，固定发布链接

---

###  发布到项目到github

    1. 静态化处理

    写完了文章，我们就可以发布了。要说明的一点是hexo的静态博客框架，那什么是静态博客呢？静态博客，是只包含html, javascript, css文件的网站，没有动态的脚本。虽然我们是用Node进行的开发，但博客的发布后就与Node无关了。在发布之前，我们要通过一条命令，把所有的文章都做静态化处理，就是生成对应的html, javascript, css，使得所有的文章都是由静态文件组成的。

    2. hexo generate

    在本地目录下，会生成一个public的目录，里面包括了所有静态化的文件。

    3. 发布到github

    接下来，我们把这个博客发布到github。

    在github中创建一个项目nodejs-hexo，项目地址：https://github.com/bsspirit/nodejs-hexo

    编辑全局配置文件：_config.yml，找到deploy的部分，设置github的项目地址。

    deploy:
    type: github
    repo: git@github.com:bsspirit/nodejs-hexo.git

    然后，通过命令进行部署 hexo deploy

    这个静态的web网站就被部署到了github，检查一下分支是gh-pages。gh-pages是github为了web项目特别设置的分支。

    然后，点击”Settings”，找到GitHub Pages，提示“Your site is published at http://bsspirit.github.io/nodejs-hexo”，打开网页 http://bsspirit.github.io/nodejs-hexo，就是我们刚刚发布的站点。

    4. 设置域名

    看起来css和js的加载路径不太对，不过没有关系。接下来，我们配置好域名，这个路径就会正确的。比如，我有一个域名是 52u.me，为了中国DNS解析，我先把域名绑定在Dnspod管理，再做跳转。

    域名有两种配置方式：

    主域名绑定：直接绑定主域名52u.me
    子域名绑定：绑定子域名blog.52u.me

    在dnspod控制台，设置主机记录@，类型A，到IP 192.30.252.153。

    有时候，我们的主域名正在使用着，需要先新建一个博客绑定到子域名，比如: blog.52u.me。

    在dnspod控制台，我们要做3步设置。

    设置主机记录github，类型A，到IP 199.27.76.133
    设置主机记录bsspirit.github.io，类型CNAME，到github.52u.me.
    设置主机记录blog，类型CNAME，到 bsspirit.github.io
    记得我们还要修改文件CNAME，改为blog.52u.me。通过浏览器，访问http://blog.52u.me，就可以打开了我们的博客站点了，而这次用的是二级域名。

    由于每次执行deploy的时候，gh-pages分支所有的文件都会被覆盖，所以我们最好在source目录下创建这个CNAME文件，这样每次部署就不用动手创建了。


### 替换皮肤    

    博客系统流行的原因，是因为他的个人性，而皮肤正式个性化的一种体现。

    利用hexo替换皮肤，还是比较简单的，3步完成。

    5.1 找到一个皮肤或者自己开发一个皮肤

    打开hexo的皮肤列表页面，你可以找到很多的皮肤，网页地址： https://github.com/tommy351/hexo/wiki/Themes。

    放到themes目录下

    比如，我觉得pacman(https://github.com/A-limon/pacman)这个皮肤还不错，我就可以下载皮肤到themes目录下面。

    通过git命令下载皮肤 git clone https://github.com/A-limon/pacman.git themes/pacman

    5.3. 在_config.yml指定皮肤

    编辑文件_config.yml，找到theme一行，改成 theme: pacman

    本地启动hexo服务器，打开浏览器 http://localhost:4000