# 在Hexo中使用mermaid
在Hexo中使用mermaid需要先引入一些模块，并配置参数。

# 安装模块
```bash
npm install -s hexo-filter-mermaid-diagrams
```
或者
```bash
yarn add hexo-filter-mermaid-diagrams
```
<!-- more -->
# 添加配置
打开博客根目录下面的_config.yml文件，在底部插入以下代码:
```yml
# mermaid chart
mermaid: ## mermaid url https://github.com/knsv/mermaid
  enable: true
  version: "8.0.0"
  options:  # find more api options from https://github.com/knsv/mermaid/blob/master/src/mermaidAPI.js
    #startOnload: true  // default true
```

# 添加模板引用
在你的主题目录下找到页脚模板文件，themes/<你的主题文件夹>/layout/_partials/footer.swig，在footer.swig文件最后添加以下代码：
```
{% if theme.mermaid.enable %}
  <script src='https://unpkg.com/mermaid@{{ theme.mermaid.version }}/dist/mermaid.min.js'></script>
  <script>
    if (window.mermaid) {
      mermaid.initialize({theme: 'forest'});
    }
  </script>
{% endif %}
```
# 结束
到此为止一切就都ok了，重启hexo server就可以看到了，还有一些其他的插件支持更多的图，这个以后再写了。