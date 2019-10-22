---
title: “列出模块”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listmodules
helpviewer_keywords:
- Debug.ListModules command
- ListModules command
- list modules command
ms.assetid: 3cb73774-6ac0-43b2-b781-75ed47175bfd
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4600f27f62d6e840041a65b4128df128e4d36873
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659534"
---
# <a name="list-modules-command"></a>“列出模块”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

列出当前进程的模块。

## <a name="syntax"></a>语法

```
Debug.ListModules [/Address:yes|no] [/Name:yes|no] [/Order:yes|no]
[/Path:yes|no] [/Process:yes|no] [/SymbolFile:yes|no]
[/SymbolStatus:yes|no] [/Timestamp:yes|no] [/Version:yes|no]
```

#### <a name="parameters"></a>参数
 /Address： `yes|no` 可选。 指定是否显示模块的内存地址。 默认值是 `yes`。

 /Name:`yes|no`（可选）。 指定是否显示模块的名称。 默认值是 `yes`。

 /Order： `yes|no` 可选。 指定是否显示模块的顺序。 默认值是 `no`。

 /Path:`yes|no`（可选）。 指定是否显示模块的路径。 默认值是 `yes`。

 /Process： `yes|no` 可选。 指定是否显示模块的进程。 默认值是 `no`。

 /SymbolFile： `yes|no` 可选。 指定是否显示模块的符号文件。 默认值是 `no`。

 /SymbolStatus： `yes|no` 可选。 指定是否显示模块的符号状态。 默认值是 `yes`。

 /Timestamp： `yes|no` 可选。 指定是否显示模块的时间戳。 默认值是 `no`。

 /Version:`yes|no`（可选）。 指定是否显示模块的版本。 默认值是 `no`。

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 此示例列出模块名称、地址和当前进程的时间戳。

```
Debug.ListModules /Address:yes /Name:yes /Order:no /Path:no /Process:no /SymbolFile:no /SymbolStatus:no /Timestamp:yes /Version:no
```

## <a name="see-also"></a>另请参阅
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)[命令窗口](../../ide/reference/command-window.md)[如何：使用 "模块" 窗口](../../debugger/how-to-use-the-modules-window.md)
