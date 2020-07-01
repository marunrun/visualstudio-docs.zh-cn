---
title: 通过 IntelliSense 菜单完成 DateTime 和 TimeSpan
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: eaa8a344e46c031b37b52106ba9aef25dac59b0c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290773"
---
# <a name="datetime-and-timespan-completion-through-intellisense-menu"></a>通过 IntelliSense 菜单完成 DateTime 和 TimeSpan

此重构适用于：

- C#

**功能：** 通过 IntelliSense 菜单完成 DateTime 和 TimeSpan 字符串文本。

**使用时机：** 你希望编写 DateTime 和 TimeSpan 字符串文本。 IntelliSense 提供基本完成功能，并说明每个字符的含义。 

操作原因：记住 DateTime 格式很难，IntelliSense 可以帮助你进行编写。

## <a name="how-to"></a>操作说明

1. 将光标置于 DateTime 或 TimeSpan 字符串文本中。
2. 按 Ctrl+空格键以触发 IntelliSense 菜单。
3. 选择要添加的字符。

   ![通过 IntelliSense 完成 DateTime](media/datetime-completion.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
