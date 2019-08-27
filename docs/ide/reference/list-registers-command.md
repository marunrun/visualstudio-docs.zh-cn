---
title: “列出寄存器”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 95edb5098d73e8fccb47f9f059473394afe5f542
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919115"
---
# <a name="list-registers-command"></a>“列出寄存器”命令
显示选中寄存器的值并允许修改要显示的寄存器列表。

## <a name="syntax"></a>语法

```cmd
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]
[/Watch [{register|registerGroup}...]]
[/Unwatch [{register|registerGroup}...]]
```

## <a name="switches"></a>开关
/Display [{`register`&#124;`registerGroup`}...]

显示指定 `register` 或 `registerGroup` 的值。 如果没有指定 `register` 或 `registerGroup`，将显示寄存器的默认列表。 如果没有指定任何开关，则出现相同行为。 例如:

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