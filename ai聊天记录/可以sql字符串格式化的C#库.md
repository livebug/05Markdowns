---
title : 'ai聊天 - C# sql 格式化技术'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: [ai_chat,c#,sql]
categories: ['应用技术']
---
# 可以sql字符串格式化的C#库

在C#中，有一些库可以用来格式化SQL字符串，以下是其中几个比较常用的库：

+ SqlFormatter：一个开源的C#库，用于格式化SQL语句。它支持多种不同的SQL语法，包括MySQL、PostgreSQL、Oracle等。
+ PoorMansTSqlFormatter：另一个开源的C#库，也用于格式化SQL语句。它支持T-SQL和PL/SQL语法，并提供了多种选项来定制格式化输出。
+ Humanizer：一个广泛使用的C#库，提供了多种字符串处理功能，其中包括将不规则的SQL语句转换为格式化的SQL语句的方法。
+ Roslyn Quoter：一个开源的C#库，用于将C#代码转换为字符串表示形式。它可以用于将SQL语句嵌入到C#代码中，并确保它们正确地转义和格式化。

这些库都具有自己的优缺点，可以根据项目的具体需求和个人喜好来选择使用。请注意，在格式化SQL字符串时要特别注意避免SQL注入攻击，并且不要将格式化后的SQL语句直接传递给数据库引擎，而是应该使用参数化查询来执行查询。

## SqlFormatter C#格式化sql字符串的代码
要使用SqlFormatter库来格式化SQL字符串，需要先安装它的NuGet包。可以使用以下命令在Visual Studio的NuGet包管理器控制台中安装：

    Copy code
    Install-Package SqlFormatter
    安装完成后，可以使用以下代码来格式化SQL字符串：

    csharp
    Copy code
    using SqlFormatter;

    // 定义要格式化的SQL字符串
    var sql = "SELECT id, name FROM users WHERE age > 18 ORDER BY name ASC";

    // 创建SqlFormatter对象并调用Format()方法进行格式化
    var formatter = new SqlFormatter();
    var formattedSql = formatter.Format(sql);

    // 输出格式化后的SQL字符串
    Console.WriteLine(formattedSql);
在上述代码中，我们首先定义了一个要格式化的SQL字符串，然后创建了一个SqlFormatter对象，并调用它的Format()方法进行格式化。最后，我们输出格式化后的SQL字符串。

SqlFormatter库支持多种不同的SQL语法，可以通过设置SqlFormatterOptions来定制输出格式。例如，可以使用以下代码将输出格式设置为MySQL风格：

    csharp
    Copy code
    var options = new SqlFormatterOptions
    {
        Language = SqlLanguage.MySql
    };

var formatter = new SqlFormatter(options);
请注意，在使用SqlFormatter库时要特别注意避免SQL注入攻击，并且不要将格式化后的SQL字符串直接传递给数据库引擎，而是应该使用参数化查询来执行查询。