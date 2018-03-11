---
layout: post
title: 在GitHub上搭建个人博客
date: 2018-03-08 15:32:24.000000000 +08:00
tag: other
---
{% raw %}
#### 创建项目
按照[github pages](https://pages.github.com/)页面的指引创建项目

#### 搭建本地环境
jekyll依赖ruby环境  
安装完ruby环境后执行  

```shell
# Install Jekyll and Bundler gems through RubyGems
gem install jekyll bundler

```
将github上的博客项目clone到本地  

`git clone https://github.com/yaoandw/yaoandw.github.io.git`


#### 下载模板
下载地址: [vno-jekyll](https://github.com/onevcat/vno-jekyll)
下载完解压后把内容复制到项目目录yaoandw.github.io中,然后执行
`bundle install`

执行完毕后,再执行

`bundle exec jekyll serve`  
来启动本地jekyll服务,起来后通过
[http://localhost:4000/](http://localhost:4000/)访问
#### 修改模板支持标签
刚才下载的vno-jekyll模板是不支持标签功能的,下面做些改动来支持标签功能
在`_layout`目录下创建文件`tagpage.html`,输入  

```html
---
layout: default
---

<h1>{{ page.tag }}</h1>

<ul>
{% for post in site.tags[page.tag] %}
  <li>
    {{ post.date | date: "%B %d, %Y" }}: <a href="{{ post.url }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>
```
创建`yaoandw.github.io/tag/java/index.html`输入

```html
---
layout: tagpage
tag: java
---
```
这里可以依次创建你想要创建的标签,eg:`yaoandw.github.io/tag/android/index.html`

然后修改`_config.yml`文件,加入  

```
mytags:
    - {title: Java, description: java, url: '/tag/java/index.html'}
    - {title: iOS, description: iOS, url: '/tag/ios/index.html'}
    - {title: Android, description: Android, url: '/tag/android/index.html'}
    - {title: Financial, description: Financial, url: '/tag/financial/index.html'}
    - {title: Kid, description: Kid, url: '/tag/kid/index.html'}
    - {title: Other, description: Other, url: '/tag/other/index.html'}
```
修改`_includes/side_panel.html`,找到

```html
{% for item in site.nav %}
    <li class="navigation__item"><a href="{{item.url}}" target="_blank" title="{{item.description}}">{{item.title}}</a></li>
{% endfor %}           
```
在下面加入

```html
{% for item in site.mytags %}
    <li class="navigation__item"><a href="{{item.url}}" title="{{item.description}}">{{item.title}}</a></li>
{% endfor %}
```
如果你创建的目录不是取名`/tag/`的话,还需要修改`js/main.js`,添加或者修改这段代码

```javascript
if (window.location.pathname.substring(0, 5) == "/tag/") {
    $('.panel-cover').addClass('panel-cover--collapsed');
  }
```
好了,现在执行

`bundle exec jekyll serve` 

看看是否ok了

#### 添加统计
使用[不蒜子](http://busuanzi.ibruce.info/)统计
在`_include/footer.html`中加入

```html
<script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>
<span id="busuanzi_container_site_uv">本站访客数<span id="busuanzi_value_site_uv"></span>人次</span>
<span id="busuanzi_container_page_pv">本文总阅读量<span id="busuanzi_value_page_pv"></span>次</span>
```

#### 绑定域名

访问github上的项目页面,点击`setting`-`GitHub Pages`-`Custom domain`,输入域名.

然后回到终端,执行  
```shell
dig yaoandw.github.io +noall +answer
```
获取到一个ip

登录域名服务商处,我这里是阿里云
将域名解析到此ip地址.
好了,这样就可以了  
具体操作可以参考<https://help.github.com/articles/setting-up-an-apex-domain-and-www-subdomain/>
#### 支持https
如果使用github提供的的二级域名,默认就是支持https的,但是使用了自己的域名后就会出现证书问题,  
网上查一下,找到两种方法  

* 使用cloudflare中转一下,可以参考[这里](https://www.jonathan-petitcolas.com/2017/01/13/using-https-with-custom-domain-name-on-github-pages.html)

* 使用[netlify](https://www.netlify.com/)提供的空间,可以参考[这里](https://jaeger.itscoder.com/web/2017/08/30/github-page-https)

本人使用了第二种方案,更直接一点,不过要注意一点,在netlify上完成设置后,不要忘了将域名指向netlify这边.

### ref

<http://louisly.com/2016/04/used-jekyll-to-create-my-github-blog/>

<https://jaeger.itscoder.com/web/2017/08/30/github-page-https>
{% endraw %}