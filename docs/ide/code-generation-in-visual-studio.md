---
title: 代码生成功能
ms.date: 01/11/2018
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 11e82560b5dc049643df013d840b709da5446b56
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974990"
---
# <a name="code-generation-features-in-visual-studio"></a>Visual Studio 中的代码生成功能

Visual Studio 可通过诸多方式帮助你生成、修复和重构代码。

## <a name="features"></a>功能

- 可使用[代码片段](../ide/code-snippets.md)插入 [switch](/dotnet/csharp/language-reference/keywords/switch) 块或 [enum](/dotnet/csharp/language-reference/keywords/enum) 声明等模板。

- 可使用[快速操作](../ide/quick-actions.md)来生成类和属性等代码，或引入局部变量。 还可使用“快速操作”[提升代码性能](../ide/common-quick-actions.md)，例如删除不必要的转换和未使用的变量，或在访问变量之前添加 null 检查。

- 可[重构代码](../ide/refactoring-in-visual-studio.md)以重命名变量、重新排列方法参数或将类型与其文件名同步（仅举几例）。

> [!NOTE]
> Visual Studio 的每种语言服务都由自己的代码生成服务，一些功能仅在 C# 中可用，而一些可同时在 C# 和 Visual Basic 中使用。

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)
- [快速操作](../ide/quick-actions.md)
- [重构](../ide/refactoring-in-visual-studio.md)
- [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)