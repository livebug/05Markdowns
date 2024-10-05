---
title : 'C# dotnet test 基本使用'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['C#']
categories: ['应用技术']
---
# C# dotnet test 基本使用

最开始对测试无所谓，但是真正自己写库的时候，测试真的至关重要，模块函数的单元测试

+ `dotnet test` 执行所有的测试
+ `dotnet test --filter TestDemoVisitor` 执行特定的测试
+ `dotnet test -l "console;verbosity=detailed" ` 打印日志