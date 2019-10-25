---
title: “列出模块”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listmodules
helpviewer_keywords:
- Debug.ListModules command
- ListModules command
- list modules command
ms.assetid: 3cb73774-6ac0-43b2-b781-75ed47175bfd
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 86e479879051d38df1da3ed2677303a76ea2d289
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747915"
---
# <a name="list-modules-command"></a>“列出模块”命令
列出当前进程的模块。

## <a name="syntax"></a>语法

```
Debug.ListModules [/Address:yes|no] [/Name:yes|no] [/Order:yes|no]
[/Path:yes|no] [/Process:yes|no] [/SymbolFile:yes|no]
[/SymbolStatus:yes|no] [/Timestamp:yes|no] [/Version:yes|no]
```

#### <a name="parameters"></a>参数
/Address:`yes|no`

可选。 指定是否显示模块的内存地址。 默认值是 `yes`。

/Name:`yes|no`

可选。 指定是否显示模块的名称。 默认值是 `yes`。

/Order:`yes|no`

可选。 指定是否显示模块的顺序。 默认值是 `no`。

/Path:`yes|no`

可选。 指定是否显示模块的路径。 默认值是 `yes`。

/Process:`yes|no`

可选。 指定是否显示模块的进程。 默认值是 `no`。

/SymbolFile:`yes|no`

可选。 指定是否显示模块的符号文件。 默认值是 `no`。

/SymbolStatus:`yes|no`

可选。 指定是否显示模块的符号状态。 默认值是 `yes`。

/Timestamp:`yes|no`

可选。 指定是否显示模块的时间戳。 默认值是 `no`。

/Version:`yes|no`

可选。 指定是否显示模块的版本。 默认值是 `no`。

## <a name="example"></a>示例
此示例列出模块名称、地址和当前进程的时间戳。

```
Debug.ListModules /Address:yes /Name:yes /Order:no /Path:no /Process:no /SymbolFile:no /SymbolStatus:no /Timestamp:yes /Version:no
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [如何：使用“模块”窗口](../../debugger/how-to-use-the-modules-window.md)