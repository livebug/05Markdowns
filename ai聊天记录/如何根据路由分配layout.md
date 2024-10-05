---
title : '如何根据路由分配layout'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: [ai_chat,blazor]
categories: ['应用技术']
---
在 Blazor 中，可以根据路由动态地分配不同的布局（Layout）。这可以通过创建一个自定义的 `Router` 组件来实现，该组件根据路由选择合适的布局。

以下是一个示例，展示如何根据路由分配不同的布局：

### 1. 创建布局组件

首先，创建两个布局组件。例如，创建 `MainLayout.razor` 和 `AdminLayout.razor`。

#### `MainLayout.razor`
```razor
@inherits LayoutComponentBase

<PageTitle>Main Layout</PageTitle>

<div class="main-layout">
    <div class="sidebar">
        @* Sidebar content *@
    </div>
    <div class="main-content">
        @Body
    </div>
</div>

<style>
    /* Styles specific to MainLayout */
</style>
```

#### `AdminLayout.razor`
```razor
@inherits LayoutComponentBase

<PageTitle>Admin Layout</PageTitle>

<div class="admin-layout">
    <div class="navbar">
        @* Navbar content *@
    </div>
    <div class="admin-content">
        @Body
    </div>
</div>

<style>
    /* Styles specific to AdminLayout */
</style>
```

### 2. 创建自定义 `Router` 组件

创建一个新的组件 `CustomRouter.razor`，并在其中实现根据路由选择布局的逻辑。

#### `CustomRouter.razor`
```razor
@using Microsoft.AspNetCore.Components.Routing
@inherits Router

<Router AppAssembly="typeof(Program).Assembly">
    <Found Context="routeData">
        @{
            var pageType = routeData.PageType;
            LayoutAttribute layoutAttribute = null;
            if (pageType != null)
            {
                layoutAttribute = pageType.GetCustomAttributes(typeof(LayoutAttribute), true)
                    .FirstOrDefault() as LayoutAttribute;
            }
            var layout = layoutAttribute?.LayoutType ?? typeof(MainLayout);

            if (routeData.PageType?.Namespace?.Contains("Admin") == true)
            {
                layout = typeof(AdminLayout);
            }
        }
        <LayoutView Layout="@layout" RouteData="@routeData" />
    </Found>
    <NotFound>
        <h3>Sorry, there's nothing at this address.</h3>
    </NotFound>
</Router>
```

### 3. 使用自定义 `Router` 组件

在 `App.razor` 中使用自定义的 `Router` 组件代替默认的 `Router` 组件。

#### `App.razor`
```razor
<CustomRouter AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="MainLayout" />
    </Found>
    <NotFound>
        <PageTitle>Not found</PageTitle>
        <h3>Sorry, there's nothing at this address.</h3>
    </NotFound>
</CustomRouter>
```

### 4. 配置页面组件

在页面组件中，可以通过命名空间或者自定义属性来决定使用哪个布局。例如，可以将管理页面放在 `Admin` 命名空间下：

#### `Pages/Admin/Dashboard.razor`
```razor
@page "/admin/dashboard"

<h3>Admin Dashboard</h3>

@code {
    // Page specific code
}
```

#### `Pages/Index.razor`
```razor
@page "/"

<h3>Main Page</h3>

@code {
    // Page specific code
}
```

通过上述步骤，Blazor 应用程序将根据路由动态选择不同的布局。通过检查路由的命名空间或其他条件，可以灵活地控制布局的选择。