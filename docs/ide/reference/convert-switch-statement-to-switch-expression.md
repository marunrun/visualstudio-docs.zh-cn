---
title: 将 Switch 语句转换为 Switch 表达式
ms.date: 06/19/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: cc13cffe8352d9fb57f5bb991c3af615eddb2a14
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "68740058"
---
# <a name="convert-switch-statement-to-switch-expression"></a>将 Switch 语句转换为 Switch 表达式

此重构适用于：

- C#

**功能：** 将 [Switch 语句](/dotnet/csharp/language-reference/keywords/switch)转换为 C# 8.0 [Switch 表达式](/dotnet/csharp/whats-new/csharp-8#switch-expressions)。

**使用时机：** 想要将 `switch` 语句转换为 `switch` 表达式，反之亦然。 

操作原因：  若仅在使用表达式，可以通过此重构轻松地实现传统 `switch` 语句的转换。

## <a name="how-to"></a>操作说明

1. 在项目文件中[将语言版本设置为预览版](/dotnet/csharp/language-reference/configure-language-version#edit-the-project-file)，因为 `switch` 表达式是新的 C# 8.0 功能。
2. 请将光标置于 `switch` 关键字，并按“Ctrl+.”   。 触发“快速操作和重构”  菜单。
3. 选择“将 Switch 语句转换为表达式”。 

   ![将 Switch 语句转换为 Switch 表达式](media/convert-switch-statement-to-switch-expression.png) 

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
