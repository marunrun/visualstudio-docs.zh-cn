---
title: 内联方法
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 0cc619ea61a7fd4d7f4bc542b946e298933a8f73
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2020
ms.locfileid: "93403504"
---
# <a name="inline-method"></a>内联方法

此重构适用于：

- C#

- Visual Basic

**功能：** 内联方法重构。 

**使用时机：** 要将单个语句中对静态、实例和扩展方法的使用替换为删除原始方法声明的选项。

操作原因：此重构会提供更清晰的语法。

## <a name="how-to"></a>操作说明

1. 将脱字号放在方法使用上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择以下选项之一： 
    
   选择“内联 `<QualifiedMethodName>`”，删除内联方法声明：

    ![将类变为抽象](media/inline-method-remove-declaration.png)

   选择“内联并保留 `<QualifiedMethodName>`”，保留原始方法声明：

    ![将类变为抽象](media/inline-method-preserve-declaration.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
