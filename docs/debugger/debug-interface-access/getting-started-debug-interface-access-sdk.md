---
title: 入门（调试接口访问 SDK） |Microsoft Docs
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
ms.openlocfilehash: 2dd6a98f377ba295d6a866c9db95671de4ff16ea
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745107"
---
# <a name="getting-started-debug-interface-access-sdk"></a>入门（调试接口访问 SDK）
调试接口访问（DIA） SDK 提供了说明文档和演示如何使用 DIA API 的示例。 使用 DIA SDK 中的接口和方法开发自定义应用程序，这些应用程序打开 .pdb 和 dbg 文件，然后在其内容中搜索符号、值、属性、地址和其他调试信息。 此 SDK 还提供与应用程序中C++的符号关联的属性的引用表。

 为了最好地使用 DIA SDK，你应熟悉以下内容：

- C++编程语言

- COM 编程

- 用于编译示例的 Visual Studio 集成开发环境（IDE）

  DIA SDK 通常随 Visual Studio 一起安装，其默认位置为 *[drive]* \Program Files\Microsoft Visual studio 9.0 \ DIA SDK。 作为安装的一部分，将自动注册实现 DIA SDK 的 msdia90，因此，你需要做的就是将 `dia2.h` 包含在程序中并链接到 `diaguids.lib`。

  标头： include\dia2。h

  库： lib\diaguids.lib

  DLL: bin\msdia80.dll

  IDL: idl\dia2.idl

## <a name="in-this-section"></a>本节内容

[概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)

查看 DIA 的基本体系结构。

[查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

提供有关如何使用 DIA API 查询 .pdb 文件的分步说明。

## <a name="see-also"></a>请参阅

- [调试接口访问 SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)