---
title: 支持代码更改 (C#和 Visual Basic) |Microsoft Docs
ms.date: 10/11/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], supported code changes
- Edit and Continue [Visual Basic], supported code changes
ms.assetid: c7a48ea9-5a7f-4328-a9d7-f0e76fac399d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: f20f61ffc4a6e4105a96b58c3dc73e7154e7c9cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929722"
---
# <a name="supported-code-changes-c-and-visual-basic"></a>支持的代码更改（C# 和 Visual Basic）
“编辑并继续”处理方法体内的大多数类型的代码更改。 但是，方法体外的大多数更改以及方法体内的小部分更改在调试期间不能应用。 若要应用这些不受支持的更改，您必须停止调试，重新开始新版本的代码。

## <a name="supported-changes-to-code"></a>支持的代码的更改

下表显示了可能会对进行的更改C#和 Visual Basic 代码，无需重新启动该会话的调试会话期间。

|语言元素/功能|受支持的编辑操作|限制|
|-|-|-|
|类型|添加方法、 字段、 构造函数、 et al|[是](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|Iterators|添加或修改|否|
|async/await 表达式|添加或修改|[是](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|动态对象|添加或修改|否|
|Lambda 表达式|添加或修改|[是](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|LINQ 表达式|添加或修改|[Lambda 表达式相同](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|

> [!NOTE]
> 编辑并继续通常支持较新的语言功能，例如字符串插值和 null 条件运算符。 有关最新信息，请参阅[Enc 支持编辑](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)页。

## <a name="unsupported-changes-to-code"></a>不支持的更改代码
 以下更改无法应用于C#和在调试会话过程中的 Visual Basic 代码：

- 对当前语句或任何其他活动语句的更改。

     活动语句包括为转至当前语句而调用过的任何语句（位于调用堆栈的函数中）。

     当前语句在源窗口中以黄色背景标记。 其他活动语句以阴影背景标记，并且是只读的。 可在“选项”对话框中更改这些默认颜色。

- 下表显示对代码的更改不受支持的语言元素。

|语言元素/功能|不受支持的编辑操作|
|-|-|
|所有代码元素|重命名|
|命名空间|添加|
|命名空间、 类型、 成员|删除|
|泛型|添加或修改|
|接口|修改|
|类型|添加抽象或虚拟成员，添加重写 (请参阅[详细信息](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))|
|类型|添加析构函数|
|成员|修改引用嵌入的互操作类型的成员|
|成员 (Visual Basic)|修改成员与 On Error 或 Resume 语句|
|成员 (Visual Basic)|修改包含 Aggregate、 Group By、 简单加入或组加入 LINQ 查询子句的成员|
|方法|修改签名|
|方法|通过添加方法主体来使抽象方法成为非抽象|
|方法|删除方法主体|
|特性|添加或修改|
|事件或属性|修改类型参数、 基类型的委托类型，或返回类型 |
|运算符或索引器|修改类型参数、 基类型的委托类型，或返回类型 |
|捕捉块|它包含活动语句时，修改|
|try – catch – finally 块|它包含活动语句时，修改|
|using 语句|添加|
|异步方法/lambda|修改异步方法/lambda 面向.NET Framework 4 的项目中，并减少 (请参阅[详细信息](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))|
|Iterators|修改面向.NET Framework 4 的项目中的迭代器，并减少 (请参阅[详细信息](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))|

## <a name="unsafe-code"></a>不安全代码
 对不安全代码的更改与对安全代码的更改有相同的限制，但它还包含一条附加限制：编辑并继续不支持对包含的方法内退出的不安全代码的更改`stackalloc`运算符。

## <a name="unsupported-app-scenarios"></a>不受支持的应用方案

不受支持的应用程序和平台包括 ASP.NET 5、 Silverlight 5 和 Windows 8.1。

> [!NOTE]
> 支持的应用包括在 Windows 10 和 x86 和 x64 应用程序面向.NET Framework 4.6 的 UWP 桌面或更高版本 （.NET Framework 是桌面版）。

## <a name="unsupported-scenarios"></a>不支持的方案
 在以下调试方案中，“编辑并继续”不可用：

- 混合模式（本机/托管）调试。

- SQL 调试。

- 调试 Dr.Watson 转储。

- 调试嵌入式运行时应用程序。

- 调试应用程序中使用附加到进程 (**调试 > 附加到进程**) 而不是通过选择运行该应用程序**启动**从**调试**菜单。

- 调试优化后的代码。

- 如果由于生成错误无法生成新版本的代码，则对旧版本的代码进行调试。

## <a name="see-also"></a>请参阅
- [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
- [如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)