---
title: "\"编辑并继续\" 错误消息对话框 |Microsoft Docs"
ms.date: 10/15/2018
ms.topic: reference
f1_keywords:
- vs.debug.ENC.SupportedButNotAvailable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7df95eae689f7c3abbb0d75a7557ce749bdceee5
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188231"
---
# <a name="edit-and-continue-error-message"></a>"编辑并继续" 错误消息

当你对支持“编辑并继续”的代码语言进行调试，但“编辑并继续”并不适用于你所做的代码更改时，会显示“编辑并继续”错误消息框。 该错误消息提供了更详细的说明。 若要响应该对话框，选择**确定**按钮以关闭对话框并取消编辑尝试。

此错误消息的可能原因包括：

- 尝试编辑 SQL Server 代码。
- 正在尝试编辑优化的代码。 可能需要从发布版本切换为调试版本。
- 尝试在代码运行时编辑代码，而不是在调试器中暂停。 尝试[设置断点](../debugger/using-breakpoints.md)，并在暂停时编辑代码。
- 尝试在只启用非托管调试时编辑托管代码。 "编辑并继续" 不适用于[混合模式调试](../debugger/how-to-debug-in-mixed-mode.md)。
- 使用编程语言编辑并继续进行的代码更改不受支持。 有关详细信息，请参阅[中C#有关支持的代码更改](supported-code-changes-csharp.md)的文章、[不支持的编辑 Visual Basic 编辑并继续](supported-code-changes-csharp.md)，以及[支持C++的代码更改](supported-code-changes-cpp.md)。
- 尝试在附加到的应用中编辑代码，而不是从 "**调试**" 菜单开始调试。
- 尝试在调试 Dr. Watson 转储时编辑代码。
- 尝试在发生未经处理的异常之后编辑代码，但未选择 "**在未经处理的异常上展开调用堆栈**" 选项。
- 尝试在调试嵌入的运行时应用程序时编辑代码。
- 尝试使用版本低于4.5.1 的 .NET Framework 版本和64位应用目标来编辑托管代码。 若要对4.5.1 之前的 .NET Framework 使用 "编辑并继续"，请将 "目标" 设置为 " **\<项目**组" 中的 " **x86** " > > "**属性**" > "**编译**" 选项**卡，**
- 尝试编辑在调试过程中修改的程序集中的代码，该程序已被重新加载。
- 尝试编辑尚未加载的程序集中的代码。
- 开始调试应用程序的旧版本，因为最新版本具有生成错误。

有关详细信息，请参见:
- [C++编辑并继续博客文章](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)
- [受支持的代码更改 (C++)](../debugger/supported-code-changes-cpp.md)
- [编辑并继续](../debugger/edit-and-continue.md)