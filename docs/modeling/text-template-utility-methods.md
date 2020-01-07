---
title: 文本模板实用工具方法
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- text templates, utility methods
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c55da4d58b717bc4d42b6fafdd084067b7e21a31
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591757"
---
# <a name="text-template-utility-methods"></a>文本模板实用工具方法

在 Visual Studio 文本模板中编写代码时，有几种方法始终可用。 这些方法是在 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>中定义的。

> [!TIP]
> 您还可以在常规（非预处理）文本模板中使用主机环境提供的其他方法和服务。 例如，你可以解析文件路径、记录错误以及获取 Visual Studio 提供的服务和任何加载的包。 有关详细信息，请参阅[从文本模板访问 Visual Studio](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))。

## <a name="write-methods"></a>写入方法

您可以使用 `Write()` 和 `WriteLine()` 方法在标准代码块中追加文本，而不是使用表达式代码块。 以下两个代码块在功能上是等效的。

### <a name="code-block-with-an-expression-block"></a>带有表达式块的代码块

```
<#
int i = 10;
while (i-- > 0)
    { #>
        <#= i #>
    <# }
#>
```

### <a name="code-block-using-writeline"></a>使用 WriteLine （）的代码块

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

你可能会发现，在带有嵌套控制结构的长代码块中使用这些实用工具方法之一而不是表达式块很有用。

`Write()` 和 `WriteLine()` 方法有两个重载，一个重载采用单个字符串参数，另一个采用复合格式字符串和要包含在字符串中的对象数组（如 `Console.WriteLine()` 方法）。 `WriteLine()` 的以下两种用法在功能上是等效的：

```
<#
    string msg = "Say: {0}, {1}, {2}";
    string s1 = "hello";
    string s2 = "goodbye";
    string s3 = "farewell";

    WriteLine(msg, s1, s2, s3);
    WriteLine("Say: hello, goodbye, farewell");
#>
```

## <a name="indentation-methods"></a>缩进方法

您可以使用缩进方法格式化文本模板的输出。 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 类具有一个 `CurrentIndent` string 属性，该属性显示文本模板中的当前缩进和一个 `indentLengths` 字段，该字段是已添加的缩进的列表。 您可以使用 `PushIndent()` 方法添加缩进，并使用 `PopIndent()` 方法减去缩进。 如果要删除所有缩进，请使用 `ClearIndent()` 方法。 以下代码块显示了这些方法的用法：

```
<#
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    ClearIndent();
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
#>
```

此代码块产生以下输出：

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>错误和警告方法

可以使用错误和警告实用工具方法将消息添加到 Visual Studio 错误列表。 例如，下面的代码会将错误消息添加到错误列表。

```
<#
  try
  {
    string str = null;
    Write(str.Length.ToString());
  }
  catch (Exception e)
  {
    Error(e.Message);
  }
#>
```

## <a name="access-to-host-and-service-provider"></a>对主机和服务提供程序的访问权限

属性 `this.Host` 可提供对执行模板的主机公开的属性的访问。 若要使用 `this.Host`，必须在 `<@template#>` 指令中设置 `hostspecific` 特性：

`<#@template ... hostspecific="true" #>`

`this.Host` 的类型取决于执行模板的主机的类型。 在 Visual Studio 中运行的模板中，可以将 `this.Host` 转换为 `IServiceProvider` 以获取对 IDE 等服务的访问权限。 例如：

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>使用一组不同的实用工具方法

作为文本生成过程的一部分，模板文件转换为类，该类始终 `GeneratedTextTransformation`命名，并从 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>继承。 如果要改为使用一组不同的方法，可以编写自己的类并在模板指令中指定它。 类必须继承自 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>。

```
<#@ template inherits="MyUtilityClass" #>
```

使用 `assembly` 指令可引用可在其中找到编译类的程序集。
