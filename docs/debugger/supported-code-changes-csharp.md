---
title: 支持的代码更改（C# 和 Visual Basic）| Microsoft Docs
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
ms.openlocfilehash: 44881035da14483c3ddf1f4c48cb3957a1ce8b50
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729091"
---
# <a name="supported-code-changes-c-and-visual-basic"></a>支持的代码更改（C# 和 Visual Basic）
“编辑并继续”处理方法体内的大多数类型的代码更改。 但是，方法体外的大多数更改以及方法体内的小部分更改在调试期间不能应用。 若要应用这些不受支持的更改，您必须停止调试，重新开始新版本的代码。

## <a name="supported-changes-to-code"></a>支持的代码更改

下表显示了在调试会话期间无需重启会话即可对 C# 和 Visual Basic 代码所进行的更改。

|语言元素/功能|支持的编辑操作|限制|
|-|-|-|
|类型|添加方法、字段、构造函数等|[是](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|迭代器|添加或修改|否|
|async/await 表达式|添加或修改|[是](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|动态对象|添加或修改|否|
|Lambda 表达式|添加或修改|[是](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|LINQ 表达式|添加或修改|[与 lambda 表达式相同](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|

> [!NOTE]
> “编辑并继续”通常支持较新的语言功能，如字符串内插和 NULL 条件运算符。 有关最新信息，请参阅 [Enc 支持的编辑](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)页。

## <a name="unsupported-changes-to-code"></a>不支持的代码更改
 在调试会话期间，不能对 C# 和 Visual Basic 代码应用下列更改：

- 对当前语句或任何其他活动语句的更改。

     活动语句包括为转至当前语句而调用过的任何语句（位于调用堆栈的函数中）。

     当前语句在源窗口中以黄色背景标记。 其他活动语句以阴影背景标记，并且是只读的。 可在“选项”对话框中更改这些默认颜色。

- 下表按语言元素显示了不支持的代码更改。

|语言元素/功能|不支持的编辑操作|
|-|-|
|所有代码元素|重命名|
|命名空间|添加|
|命名空间、类型、成员|删除|
|泛型|添加或修改|
|接口|修改|
|类型|添加抽象或虚拟成员、添加替代（了解[详细信息](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)）|
|类型|添加析构函数|
|成员|修改引用嵌入式互操作类型的成员|
|成员|在通过执行代码访问后修改静态成员|
|成员 (Visual Basic)|使用 On Error 或 Resume 语句修改成员|
|成员 (Visual Basic)|修改包含 Aggregate、Group By、Simple Join 或 Group Join LINQ 查询子句的成员|
|方法|修改签名|
|方法|通过添加方法主体使抽象方法变为非抽象方法|
|方法|删除方法主体|
|特性|添加或修改|
|事件或属性|修改类型参数、基类型、委托类型或返回类型 |
|运算符或索引器|修改类型参数、基类型、委托类型或返回类型 |
|捕捉块|在包含活动语句时进行修改|
|try-catch-finally 块|在包含活动语句时进行修改|
|using 语句|添加|
|异步方法/lambda|在面向 .NET Framework 4 及更低版本的项目中修改异步方法/lambda（了解[详细信息](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)）|
|迭代器|在面向 .NET Framework 4 及更低版本的项目中修改迭代器（了解[详细信息](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)）|

## <a name="unsafe-code"></a>不安全代码
 对不安全代码的更改与对安全代码的更改具有相同的限制，但它还包含一条附加限制：“编辑并继续”不支持更改存在于包含 `stackalloc` 运算符的方法内的不安全代码。

## <a name="unsupported-app-scenarios"></a>不支持的应用方案

不受支持的应用和平台包括 ASP.NET 5、Silverlight 5 和 Windows 8.1。

> [!NOTE]
> 支持的应用包括 Windows 10 中的 UWP，以及面向 .NET Framework 4.6 桌面版或更高版本的 x86 和 x64 应用（.NET Framework 仅为桌面版本）。

## <a name="unsupported-scenarios"></a>不支持的方案
 在以下调试方案中，“编辑并继续”不可用：

- 混合模式（本机/托管）调试。

- SQL 调试。

- 调试 Dr.Watson 转储。

- 调试嵌入式运行时应用程序。

- 使用“附加到进程”（“调试”>“附加到进程”）调试应用程序，而不是通过选择“调试”菜单中的“启动”来运行应用程序  。

- 调试优化后的代码。

- 如果由于生成错误无法生成新版本的代码，则对旧版本的代码进行调试。

## <a name="see-also"></a>请参阅
- [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
- [如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)