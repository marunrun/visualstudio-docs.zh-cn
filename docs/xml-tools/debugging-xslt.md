---
title: 调试 XSLT 代码的方法
ms.date: 03/05/2019
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 67ea95e3c52daed03acfe451f353edc039e1fecb
ms.sourcegitcommit: 9753c7544cec852ca5efd0834e0956d9e53a5734
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67043533"
---
# <a name="debugging-xslt"></a>调试 XSLT

你可以调试在 Visual Studio 中的 XSLT 代码。 XSLT 调试器支持设置断点、 查看 XSLT 执行状态等。 XSLT 调试程序可以用于调试 XSLT 样式表或 XSLT 应用程序。

可以通过单步执行、 逐过程执行，或跳出代码单步执行一次执行一行代码。 有关使用 XSLT 调试程序的代码单步执行功能的命令是不同于其他 Visual Studio 调试器。

开始调试后，XSLT 调试器即会打开窗口以显示输入文档和 XSLT 输出。

> [!NOTE]
> XSLT 调试程序是仅在 Visual Studio Professional 和 Enterprise 版本中可用。

## <a name="debug-from-the-xml-editor"></a>从 XML 编辑器中进行调试

样式表或输入的 XML 文件在编辑器中打开时，可以启动调试器。 这样可以调试在设计样式表。

1. 在 Visual Studio 中打开样式表或 XML 文件。

1. 选择**启动 XSLT 调试**从**XML**菜单或按**Alt**+**F5**。

## <a name="debug-from-an-app-that-uses-xslt"></a>从使用 XSLT 的应用程序进行调试

您可以单步执行 XSLT 调试应用程序时。 当您按下**F11**上<xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName>调用时，调试器可以单步执行 XSLT 代码。

> [!NOTE]
> 不支持从 <xref:System.Xml.Xsl.XslTransform> 类进入并逐行执行 XSLT。 <xref:System.Xml.Xsl.XslCompiledTransform> 类是唯一支持在调试的同时进入并逐行执行 XSLT 的 XSLT 处理器。

### <a name="to-start-debugging-an-xslt-application"></a>开始调试 XSLT 应用程序

1. 在实例化 <xref:System.Xml.Xsl.XslCompiledTransform> 对象时，在代码中将 `enableDebug` 参数设置为 `true`。 此设置通知 XSLT 处理器在编译代码时创建调试信息。

1. 按**F11**来单步执行 XSLT 代码。

   在新的文档窗口中加载的 XSLT 样式表并启动 XSLT 调试程序。

   或者，可以将断点添加到样式表并运行应用程序。

### <a name="example"></a>示例

下面是一个 C# XSLT 程序的示例。 该示例显示如何启用 XSLT 调试。

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Xsl;

namespace ConsoleApplication
{
  class Program
  {
    private const string sourceFile = @"c:\data\xsl_files\books.xml";
    private const string stylesheet = @"c:\data\xsl_files\below-average.xsl";
    private const string outputFile = @"c:\data\xsl_files\output.xml";

    static void Main(string[] args)
    {
      // Enable XSLT debugging.
      XslCompiledTransform xslt = new XslCompiledTransform(true);

      // Compile the style sheet.
      xslt.Load(stylesheet)

      // Execute the XSLT transform.
      FileStream outputStream = new FileStream(outputFile, FileMode.Append);
      xslt.Transform(sourceFile, null, outputStream);
    }
  }
}
```

## <a name="xslt-profiler"></a>XSLT 探查器

[XSLT 探查器](../xml-tools/xslt-profiler.md)是一个工具，使开发人员能够衡量、 评估，并通过创建详细的 XSLT 性能报告着力 XSLT 代码中的与性能相关问题。 有关详细信息，请参阅[XSLT 探查器](../xml-tools/xslt-profiler.md)。

## <a name="see-also"></a>请参阅

- [演练：调试 XSLT 样式表](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
- [先来看一下 Visual Studio 调试器](../debugger/debugger-feature-tour.md)
- [调试基础知识：断点](../debugger/using-breakpoints.md)
