---
title: 通过 IntelliSense 菜单完成正则表达式
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 68b5cb480184a287d9fcb088b0a74ac9d607f3f2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79093852"
---
# <a name="regex-completion-through-intellisense-menu"></a>通过 IntelliSense 菜单完成正则表达式

此重构适用于：

- C#

- Visual Basic

**功能：** 通过 IntelliSense 菜单完成正则表达式 (regex)。

**使用时机：** 想要从 IntelliSense 获得有关编写正则表达式的帮助。 IntelliSense 提供基本完成功能，并说明每个正则表达式字符的含义。 

操作原因：  编写正则表达式很难，IntelliSense 可以帮助你进行编写。

## <a name="how-to"></a>操作说明

1. 请将光标置于正则表达式字符串。
2. 按 Ctrl  +空格键  以触发 IntelliSense  菜单。
3. 选择所需字符添加到正则表达式字符串。

   ![通过 IntelliSense 完成正则表达式](../media/regex-completion-intellisense.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
