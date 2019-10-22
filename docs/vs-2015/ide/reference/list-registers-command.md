---
title: “列出寄存器”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3476244d3044eb80dbfce3559479421b012cc5fa
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659501"
---
# <a name="list-registers-command"></a>“列出寄存器”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示选中寄存器的值并允许修改要显示的寄存器列表。

## <a name="syntax"></a>语法

```
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]
[/Watch [{register|registerGroup}...]]
[/Unwatch [{register|registerGroup}...]]
```

## <a name="switches"></a>开关
 /Display [{`register`&#124; `registerGroup`} ...]显示指定 `register` 或 `registerGroup` 的值。 如果没有指定 `register` 或 `registerGroup`，将显示寄存器的默认列表。 如果没有指定任何开关，则出现相同行为。 例如:

 `Debug.ListRegisters /Display eax`

 等效于

 `Debug.ListRegisters eax`

 /List 显示列表中的所有注册组。

 /Watch [{`register`&#124; `registerGroup`} ...]向列表中添加一个或多个 `register` 或 `registerGroup` 值。

 /Unwatch [{`register`&#124; `registerGroup`} ...]从列表中删除一个或多个 `register` 或 `registerGroup` 值。

## <a name="remarks"></a>备注
 别名 `r` 可用来代替 `Debug.ListRegisters`。

## <a name="example"></a>示例
 此示例使用 `Debug.ListRegisters` 别名 `r` 显示寄存组 `Flags` 的值。

```
r /Display Flags
```

## <a name="see-also"></a>请参阅
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)[调试基础知识：注册窗口](../../debugger/debugging-basics-registers-window.md)[如何：使用 "寄存器" 窗口](../../debugger/how-to-use-the-registers-window.md)
