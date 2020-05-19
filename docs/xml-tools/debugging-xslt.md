---
title: 调试 XSLT 代码的方法
ms.date: 03/05/2019
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: f6f4a1ce60f04bcea6e21b52db9347a95292dab2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592849"
---
# <a name="debugging-xslt"></a>调试 XSLT

你可以在 Visual Studio 中调试 XSLT 代码。 XSLT 调试器支持设置断点、查看 XSLT 执行状态等操作。 可以使用 XSLT 调试器来调试 XSLT 样式表或 XSLT 应用程序。

你可以通过进入并逐行执行代码、逐行执行代码或跳出代码来一次执行一行代码。 使用 XSLT 调试器的代码逐步执行功能的命令与其他 Visual Studio 调试器的命令相同。

开始调试后，XSLT 调试器即会打开窗口以显示输入文档和 XSLT 输出。

> [!NOTE]
> XSLT 调试器仅在 Visual Studio Professional 和 Enterprise 版本中提供。

## <a name="debug-from-the-xml-editor"></a>从 XML 编辑器中进行调试

在编辑器中打开样式表或输入 XML 文件时，可以启动调试器。 这样可以在设计样式表时进行调试。

1. 在 Visual Studio 中打开样式表或 XML 文件。

1. 从“XML”菜单中选择“启动 XSLT 调试”，或按 Alt+F5   。

## <a name="debug-from-an-app-that-uses-xslt"></a>从使用 XSLT 的应用进行调试

你可以在调试应用程序的同时进入并逐行执行 XSLT。 在 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> 调用中按 F11 键时，调试程序可以进入并逐行执行 XSLT 代码。

> [!NOTE]
> 不支持从 <xref:System.Xml.Xsl.XslTransform> 类进入并逐行执行 XSLT。 <xref:System.Xml.Xsl.XslCompiledTransform> 类是唯一支持在调试的同时进入并逐行执行 XSLT 的 XSLT 处理器。

### <a name="to-start-debugging-an-xslt-application"></a>开始调试 XSLT 应用程序

1. 在实例化 <xref:System.Xml.Xsl.XslCompiledTransform> 对象时，在代码中将 `enableDebug` 参数设置为 `true`。 此设置通知 XSLT 处理器在编译代码时创建调试信息。

1. 按 F11 键进入并逐行执行 XSLT 代码。

   XSLT 样式表已加载到新的文档窗口中，XSLT 调试程序也将启动。

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
      xslt.Load(stylesheet);

      // Execute the XSLT transform.
      FileStream outputStream = new FileStream(outputFile, FileMode.Append);
      xslt.Transform(sourceFile, null, outputStream);
    }
  }
}
```

## <a name="xslt-profiler"></a>XSLT 探查器

[XSLT 探查器](../xml-tools/xslt-profiler.md)是一种工具，开发人员可用它来创建详细的 XSLT 性能报告，从而对 XSLT 代码中与性能相关的问题进行衡量、评估并将这些问题作为目标。 有关详细信息，请参阅[XSLT 探查器](../xml-tools/xslt-profiler.md)。

## <a name="see-also"></a>请参阅

- [演练：调试 XSLT 样式表](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
- [初步了解 Visual Studio 调试器](../debugger/debugger-feature-tour.md)
- [调试基础知识：断点](../debugger/using-breakpoints.md)
