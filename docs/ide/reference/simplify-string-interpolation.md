---
title: 简化字符串内插
ms.date: 02/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 15f034b0ecf46e19681f3b74e4137a2de9e9d950
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77283435"
---
# <a name="simplify-string-interpolation-refactoring"></a>简化字符串内插重构

此重构适用于：

- C#

**功能：** 让你可以[简化字符串内插](https://docs.microsoft.com/dotnet/csharp/tutorials/string-interpolation)。

**使用时机：** 当你有可简化的字符串内插时。

操作原因：  简化字符串内插可以提供更清晰和简洁的语法。 此重构工具可自动执行此任务，而无需手动执行该任务。

## <a name="how-to"></a>操作说明

1. 将插入光标置于字符串内插上：

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

3. 选择“简化内插” 

    ![简化字符串内插](media/simplify-string-interpolation.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)