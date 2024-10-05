---
title : 'markdown代码美化-prismjs'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['javascript','prismjs']
categories: ['应用技术']
---
# markdown代码美化-prismjs

### 实例代码

     <!--重置浏览器样式-->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/normalize.css@8.0.1/normalize.css">  
    <!--代码块主题-->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/themes/prism-coy.min.css">
    <!--工具栏插件-->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/toolbar/prism-toolbar.min.css">
    <!--行号插件-->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/line-numbers/prism-line-numbers.min.css">
    ... 
    <!--prism核心js (用于渲染代码块)-->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/prism.min.js"></script>  
    <!--显示代码块行号-->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/line-numbers/prism-line-numbers.min.js"></script>
    <!--工具栏(一些插件的前置依赖)-->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/toolbar/prism-toolbar.min.js"></script>
    <!--代码块显示语言名称-->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/show-language/prism-show-language.min.js"></script>
    <!--复制代码-->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/copy-to-clipboard/prism-copy-to-clipboard.min.js"></script>
    <!--自动去cdn加载对应语言的代码高亮js-->
    <script src="https://cdn.jsdelivr.net/npm/prismjs@1.27.0/plugins/autoloader/prism-autoloader.min.js"></script>
    <script type="text/javascript">
        window.initPreCode = function () {
            var pre_eles = document.getElementsByTagName("pre");
            for (var i = 0; i < pre_eles.length; i++) {
                pre_eles[i].classList.add("line-numbers");
            }
        } 
    </script>

### 工具网站

<https://www.npmjs.com/package/prismjs>

### Blazor 中使用

1.  使用`MarkDig库` 需要增加 `webstoating.markdig.prism` 库
2.  生成 `MarkdownPipeline` 时，增加`UsePrism()`
3.  在组件的 `OnAfterRender{Async}` 需要 JS互操作
    ```CSharp
    await JsRuntime.InvokeVoidAsync("Prism.highlightAll");
    ```
4.  需要增加行号优化，注释上面的 `window.initPreCode`段是需要给代码块增加样式类
5.  在组件的 `OnAfterRender{Async}` 需要 JS互操作
    ```CSharp
    await JsRuntime.InvokeVoidAsync("initPreCode");
    ```

