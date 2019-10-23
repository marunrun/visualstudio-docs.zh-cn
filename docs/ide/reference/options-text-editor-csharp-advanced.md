---
title: 选项，文本编辑器，C#，高级
ms.date: 01/16/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d1d540f3a49eda22973b25a6b9a91691907efe93
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666294"
---
# <a name="options-text-editor-c-advanced"></a>选项，文本编辑器，C#，高级

可使用“高级”选项页修改 C# 的编辑器格式设置、代码重构设置和 XML 文档注释设置  。 要访问此选项页，请选择“工具” > “选项”，然后选择“文本编辑器” > “C#” > “高级”      。

> [!NOTE]
> 并非所有选项都会在此处列出。

## <a name="analysis"></a>分析

- 启用完整解决方案分析

   针对解决方案中的所有文件启用代码分析，而不仅针对打开的代码文件。 详情请参阅[完整解决方案分析](../../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)。

## <a name="using-directives"></a>Using 指令

- 对 using 排序时将“System”指令排在第一位

   当你选择右键单击菜单中的“删除和排序 Using”命令后，它会对 `using` 指令进行排序，并将“System”命名空间置于列表顶部  。

   排序前：

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```

   排序后：

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using AutoMapper;
   using FluentValidation;
   using Newtonsoft.Json;
   ```

- 单独的 using 指令组

   当你选择右键单击菜单中的“删除和排序 Using”  命令后，它会在具有相同根命名空间的指令组之间插入空行，以将 `using` 指令分隔开来。

   排序前：

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```

   排序后：

   ```csharp
   using AutoMapper;

   using FluentValidation;

   using Newtonsoft.Json;

   using System;
   using System.Collections.Generic;
   using System.Linq;
   ```

- 建议对引用程序集中的类型使用 using
- 建议对 NuGet 包中的类型使用 using

   选择这些选项时，[快速操作](../quick-actions.md)可用于安装 NuGet 包，并为未引用的类型添加 `using` 指令。

   ![用于在 Visual Studio 中安装 NuGet 包的快速操作](media/nuget-lightbulb.png)

## <a name="highlighting"></a>Highlighting

- 突出显示对光标下符号的引用

   光标定位在符号内，或单击某个符号时，将突出显示代码文件中该符号的所有实例。

## <a name="outlining"></a>大纲显示

- 打开文件时进入大纲模式

   选中后，会自动大纲显示代码文件，这将创建可折叠代码块。 首次打开文件时，#region 块和非活动代码块处于折叠状态。

- 显示过程行分隔符

   文本编辑器指示过程的可视范围。 在项目的 .cs  源文件中，在下表列出的位置处绘制行：

   |.cs 源文件中的位置|行位置示例|
   |---------------------------------|------------------------------|
   |在块声明构造结束之后|-   在类、结构、模块、接口或枚举的末尾<br />-   在属性、函数或子类之后<br />-   不在属性中的 get 和 set 子句之间|
   |在一组单行构造之后|-   在类文件中的导入语句之后，在类型定义之前<br />-   在类中声明的变量之后，在所有过程之前|
   |在单行声明（非块级声明）之后|-   在导入语句、继承语句、变量声明、事件声明、委托声明和 DLL 声明语句之后|

## <a name="block-structure-guides"></a>块结构指南

如果选中这些复选框，可以在代码中的大括号 ({}  ) 之间显示虚竖线。 然后，就可以轻松查看声明级构造和代码级构造的各个代码块了。

## <a name="editor-help"></a>编辑器帮助

- 为 /// 生成 XML 文档注释

   选中后，在键入 `///` 命令说明后为 XML 文档注释插入 XML 元素。 有关 XML 文档的详细信息，请参阅 [XML 文档注释（C# 编程指南）](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)。

## <a name="see-also"></a>请参阅

- [如何：为文档生成插入 XML 注释](../../ide/reference/generate-xml-documentation-comments.md)
- [XML 文档注释（C# 编程指南）](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [使用 XML 注释记录代码（C# 指南）](/dotnet/csharp/codedoc)
- [设置语言特定的编辑器选项](../../ide/reference/setting-language-specific-editor-options.md)
- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
