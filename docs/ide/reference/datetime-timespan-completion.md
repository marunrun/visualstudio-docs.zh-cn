---
title: 通过 IntelliSense 菜单完成 DateTime 和 TimeSpan
ms.date: 07/31/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 36b6d5440e532653845638f87f7f1d7066af6ba3
ms.sourcegitcommit: 43df639b2cd99200f725a8ebb941477481a6f0ff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87471543"
---
# <a name="datetime-and-timespan-completion-through-intellisense-menu"></a>通过 IntelliSense 菜单完成 DateTime 和 TimeSpan

此重构适用于：

- C#

**功能：** 通过 IntelliSense 菜单完成 DateTime 和 TimeSpan 字符串文本和格式字符串的填写。

**使用时机：** 你需要编写 DateTime 和 TimeSpan 字符串文本和格式字符串。 IntelliSense 提供基本完成功能，并说明每个字符的含义。 

操作原因：记住 DateTime 格式很难，IntelliSense 可以帮助你进行编写。

## <a name="how-to"></a>操作说明

1. 将光标置于 DateTime 或 TimeSpan 格式字符串中。
2. 按 Ctrl+空格键以触发 IntelliSense 菜单。
3. 选择要添加的字符。

   ![通过 IntelliSense 完成 DateTime](media/datetime-completion.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
