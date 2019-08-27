---
title: 入门 （调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- .dbg files
- DBG files
ms.assetid: cb3d040a-2846-40d7-bdbc-8a5beb5dd2f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 089d824a6f693d7a0661b2e099ded82e0b02f403
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62554401"
---
# <a name="getting-started-debug-interface-access-sdk"></a>入门（调试接口访问 SDK）
调试接口访问 (DIA) SDK 将向您提供指导文档和示例，说明了如何使用 DIA API。 在 DIA SDK 中使用接口和方法，可以开发自定义应用程序打开的文件.pdb 和.dbg 文件并搜索其内容的符号、 值、 属性、 地址和其他调试信息。 此 SDK 还提供了引用表中找到与符号关联的属性C++应用程序。

 若要充分利用 DIA SDK，应熟悉以下：

- C++编程语言

- COM 编程

- 用于编译示例 visual Studio 集成的开发环境 (IDE)

  使用 Visual Studio 通常安装 DIA SDK，其默认位置是 *[驱动器]* \Program Files\Microsoft Visual Studio 9.0\DIA SDK。 作为安装的一部分，msdia90.dll，实现 DIA SDK，将自动注册，因此，您需要执行的操作使用它，只需包括`dia2.h`程序和链接到`diaguids.lib`。

  标头： include\dia2.h

  库： lib\diaguids.lib

  DLL: bin\msdia80.dll

  IDL: idl\dia2.idl

## <a name="in-this-section"></a>本节内容

[概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)

评审 dia 时的基本体系结构

[查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

分步说明了如何使用 DIA API 来查询.pdb 文件。

## <a name="see-also"></a>请参阅

- [调试接口访问 SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)