---
title: 简化条件表达式
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 0242c8c89848e3e76673ddfbca8a27c20605048d
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810345"
---
# <a name="simplify-conditional-expression-refactoring"></a>简化条件表达式重构

此重构适用于：

- C#

**功能：** 允许简化[条件表达式](/dotnet/csharp/language-reference/operators/conditional-operator)。

**使用时机：** 需要删除不必要的代码以提高清晰度。

操作原因：简化条件表达式可以提供更清晰和简洁的语法。 此重构工具可自动执行此任务，而无需手动执行该任务。

## <a name="how-to"></a>操作说明

1. 将插入符号置于条件表达式上：

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择“简化条件表达式”

    ![简化条件表达式](media/simplify-conditional-expression.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)