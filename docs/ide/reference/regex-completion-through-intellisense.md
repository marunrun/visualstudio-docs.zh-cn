---
title: 通过 IntelliSense 菜单完成正则表达式
ms.date: 06/10/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 75110432f9bba35ce02588032b9a41dece01056b
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033418"
---
# <a name="regex-completion-through-intellisense-menu"></a>通过 IntelliSense 菜单完成正则表达式

此重构适用于：

- C#

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
