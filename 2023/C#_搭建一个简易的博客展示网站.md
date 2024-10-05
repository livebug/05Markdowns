# 搭建一个简易的博客展示网站 

## 1. 使用的东西

GITHUB C#实现的Markdown:  
https://github.com/xoofx/markdig

GITHUB:为ASPNETCORE做的适配：  
https://github.com/RickStrahl/Westwind.AspNetCore.Markdown

BLAZOR：  
https://learn.microsoft.com/zh-cn/aspnet/core/blazor/?view=aspnetcore-6.0


## Q1:处理文章中的文件相对地址
**传入文章地址及网站根uri，相对地址根据`fileuri`转换，根路径根据`baseuri`替换**
```CSharp
private string TransLinksToAbsoluteUrl(string markdown, string fileuri,string baseuri)
{
    var doc = Markdig.Markdown.Parse(markdown);
    var uri = new Uri(fileuri, UriKind.Absolute);

    foreach (var item in doc)
    {
        if (item is not ParagraphBlock paragraph) continue;
        if (paragraph.Inline == null) continue;
        foreach (var inline in paragraph.Inline)
        {
            if (inline is not LinkInline link)
                continue;
            if (link.Url is null)
                continue;
            if (link.Url.Contains("://"))
                continue;

            string newUrl;
            if (Regex.IsMatch(link.Url, "^(/)"))
                newUrl = baseuri + link.Url.ToString().Replace(" ", "%20");
            else // 相对路经这么处理可以
                newUrl = new Uri(uri, link.Url).ToString().Replace(" ", "%20");
            markdown = markdown.Replace("](" + link.Url + ")", "](" + newUrl + ")");
        }
    }
    return markdown;
}
```

## Q2:处理文章中的代码高亮
见 [markdown代码美化-prismjs ](../Node.js/markdown代码美化-prismjs.md)


## Q3:测试中发现 组件的 `OnInitialized()` 会运行两次 
经过复杂的词汇检查，发现可能原因在`\Pages\_Layout.cshtml` 文件的
```CSharp
<component type="typeof(HeadOutlet)" render-mode="ServerPrerendered" />
```
其中 `render-mode` 参数说明如下：
>Describes the render mode of the component.  组件的渲染类型  

|                        |     |                                                                                                                            |
| ---------------------- | --- | -------------------------------------------------------------------------------------------------------------------------- |
| Server                 | 2   | 呈现 Blazor 服务器端应用程序的标记。 这不包括组件的任何输出。 用户代理启动时，它使用此标记启动 blazor 应用程序。           |
| ServerPrerendered      | 3   | 将组件呈现为静态 HTML，并包含 Blazor 服务器端应用程序的标记。 用户代理启动时，它使用此标记启动 blazor 应用程序。           |
| Static                 | 1   | 将组件呈现为静态 HTML。                                                                                                    |
| WebAssembly            | 4   | 呈现 Blazor Webassembly 应用程序的标记。 这不包括组件的任何输出。 用户代理启动时，它使用此标记启动 blazor 客户端应用程序。 |
| WebAssemblyPrerendered | 5   | 将组件呈现为静态 HTML，并包含 Blazor webassembly 应用程序的标记。 用户代理启动时，它使用此标记启动 blazor 客户端应用程序。 |


在 `Blazor Server` 应用中，当 `RenderMode` 为 `ServerPrerendered` 时，组件最初作为页面的一部分静态呈现。 浏览器重新建立与服务器的 `SignalR` 连接后，将再次呈现组件，并且该组件为交互式。 如果存在用于初始化组件的 `OnInitialized{Async}` 生命周期方法，则该方法执行两次：
 + 在静态预呈现组件时执行一次。
 + 在建立服务器连接后执行一次。    
  
在最终呈现组件时，这可能导致 UI 中显示的数据发生明显变化。 若要避免在 Blazor Server 应用中出现此双重呈现行为，请传递一个标识符以在预呈现期间缓存状态并在预呈现后检索状态。

**说明：其实就是三种模式，一种直接就是静态文件，一种是静态文件+程序标记，另一种时只有程序标记；这个程序标记（暂时这么翻译）可以用来引导Blazor应用程序。 翻译很别扭，就是带标记经过处理后才能展示，第二种是先展示静态文件，处理完成后再展示最终状态，所以会初始化两次**


## Q4:在文章中国的 html实例代码不显示，被分析器分析了