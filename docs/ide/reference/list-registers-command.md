---
title: “列出寄存器”命令
description: 了解 List Registers 命令，以及它如何显示所选寄存器的值，并允许你修改要显示的寄存器列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5459ded60ea90ae00a3f943f829065a82548d160
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305293"
---
# <a name="list-registers-command"></a>“列出寄存器”命令
显示选中寄存器的值并允许修改要显示的寄存器列表。

## <a name="syntax"></a>语法

```cmd
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]
[/Watch [{register|registerGroup}...]]
[/Unwatch [{register|registerGroup}...]]
```

## <a name="switches"></a>交换机
/Display [{`register`&#124;`registerGroup`}...]

显示指定 `register` 或 `registerGroup` 的值。 如果没有指定 `register` 或 `registerGroup`，将显示寄存器的默认列表。 如果没有指定任何开关，则出现相同行为。 例如：

`Debug.ListRegisters /Display eax`

等效于

`Debug.ListRegisters eax`

/List

在列表中显示所有寄存器组。

/Watch [{`register`&#124;`registerGroup`}...]

向列表添加一个或多个 `register` 或 `registerGroup` 值。

/ Unwatch [{`register`&#124;`registerGroup`}...]

从列表中删除一个或多个 `register` 或 `registerGroup` 值。

## <a name="remarks"></a>备注
别名 `r` 可用来代替 `Debug.ListRegisters`。

## <a name="example"></a>示例
此示例使用 `Debug.ListRegisters` 别名 `r` 显示寄存组 `Flags` 的值。

```cmd
r /Display Flags
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [调试基础知识：“寄存器”窗口](../../debugger/debugging-basics-registers-window.md)
- [如何：使用“寄存器”窗口](../../debugger/how-to-use-the-registers-window.md)
