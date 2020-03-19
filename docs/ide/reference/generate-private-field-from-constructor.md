---
title: 从构造函数生成私有字段
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
ms.openlocfilehash: 4eb5dd39d0fb2d4cd9ba8ade0d0408d6e36a4854
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094024"
---
# <a name="generate-private-field-from-constructor"></a>从构造函数生成私有字段

此重构适用于： 

- C# 

- Visual Basic

**功能：** 从构造函数生成私有字段。 

**使用时机：** 在你希望从构造函数快速添加私有字段时。

操作原因：  编写私有字段可能会很耗时且重复。 使用此重构非常快捷，并使程序更可靠。

## <a name="how-to"></a>操作说明 

1. 将光标置于构造函数中的参数名称上。

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   
3. 选择“创建和初始化字段”选项  。

   ![从构造函数生成私有字段](media/generate-private-field-from-constructor.png)

## <a name="see-also"></a>请参阅 

- [重构](../refactoring-in-visual-studio.md)
