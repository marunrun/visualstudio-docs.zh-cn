---
title: 伪变量 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Watch window, pseudovariables
- debugging [Visual Studio], pseudovariables
- pseudovariables
ms.assetid: fae84f68-2138-4144-9bd4-c9e271b6182a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5b0369a30e69fc69782bbc4a0f5b0c4518cac07
ms.sourcegitcommit: 10d16e18c5f5e482c4c2856e6cacaad283463b65
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776089"
---
# <a name="pseudovariables-in-the-visual-studio-debugger"></a>Visual Studio 调试器中的伪变量
伪变量是用于在变量窗口或“快速监视”对话框中显示某些信息的术语。 你可以像输入普通变量那样输入伪变量。 但伪变量不是变量，它不与程序中的变量名相对应。

## <a name="example"></a>示例
 假设你在编写本机代码应用程序，并且希望看到此应用程序中分配的句柄数。 可以在“监视”窗口的“名称”列中输入以下伪变量，然后按“返回”计算它 ：

`$handles`

 在本机代码中，可使用的伪变量如下表所示：

|伪变量|函数|
|--------------------|--------------|
|`$err`|显示函数 SetLastError 设置的上一个错误值。 显示的值代表将由 GetLastError 函数返回的值。<br /><br /> 使用 `$err,hr` 查看此值的已解码形式。 例如，如果上一个错误是 3，则 `$err,hr` 将显示 `ERROR_PATH_NOT_FOUND : The system cannot find the path specified.`|
|`$handles`|显示应用程序中分配的句柄数。|
|`$vframe`|显示当前堆栈帧的地址。|
|`$tid`|显示当前线程的线程 ID。|
|`$env`|在字符串查看器中显示环境块。|
|`$cmdline`|显示已启动程序的命令行字符串。|
|`$pid`|显示进程 ID。|
|`$` registername<br /><br /> or<br /><br /> `@` registername|显示寄存器“registerName”的内容。<br /><br /> 通常，只需输入寄存器名便可以显示寄存器的内容。 仅在寄存器名重载变量名时才需要使用此语法。 如果寄存器名与当前范围内的某个变量名同名，则调试器将该名称解释为变量名。 这时就需要使用 `$` registername 或 `@` registername 寄存器名 。|
|`$clk`|以时钟形式显示时间。|
|`$user`|显示一个结构，在该结构中含有应用程序运行于的帐户的帐户信息。 出于安全原因，将不显示密码信息。|
|`$exceptionstack`|显示当前 Windows 运行时异常的堆栈跟踪。 `$ exceptionstack` 仅适用于 UWP 应用。 C++ 异常和 SEH 异常不支持 `$ exceptionstack`|
|`$returnvalue`|显示方法的返回值。|

 在 C# 中，可使用的伪变量如下表所示：

|伪变量|函数|
|--------------------|--------------|
|`$exception`|显示有关上一个异常的信息。 如果没有发生异常，则计算 `$exception` 将显示错误消息。<br /><br /> 当“异常助手”处于禁用状态时，如果发生异常，`$exception` 将自动添加到“局部变量”窗口中。|
|`$user`|显示一个结构，在该结构中含有应用程序运行于的帐户的帐户信息。 出于安全原因，将不显示密码信息。|
|`$returnvalue`|显示 .NET 方法的返回值。|

 在 Visual Basic 中，可使用的伪变量如下表所示：

|伪变量|函数|
|--------------------|--------------|
|`$exception`|显示有关上一个异常的信息。 如果没有发生异常，则计算 `$exception` 将显示错误消息。|
|`$delete` 或 `$$delete`|删除已在“即时”窗口中创建的隐式变量。 语法是 `$delete,` 变量或 `$delete,` 变量`.`|
|`$objectids` 或 `$listobjectids`|将所有活动对象 ID 显示为指定的表达式的子级。 语法是 `$objectid,` 表达式或 `$listobjectids,` 表达式`.`|
|`$` N `#`|显示对象 ID 等于 N 的对象。|
|`$dynamic`|显示这两个特殊“动态视图”实现 `IDynamicMetaObjectProvider` 的对象的节点。 接口。 语法是 `$dynamic,` 对象。 此功能仅应用于使用 .NET Framework 版本 4 或更高版本的代码。|

## <a name="see-also"></a>请参阅
- [监视和快速监视窗口](../debugger/watch-and-quickwatch-windows.md)
- [变量窗口](../debugger/debugger-windows.md)
