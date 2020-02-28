---
title: 从构造函数生成私有字段
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 8ef4188216b669b30b7af9bd725ec432bcd0a774
ms.sourcegitcommit: 3c105990656cd509062ce60e52e776c794f6305d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77529412"
---
# <a name="generate-private-field-from-constructor"></a>从构造函数生成私有字段

此重构适用于： 

- C# 

**功能：** 从构造函数生成私有字段。 

**使用时机：** 在你希望从构造函数快速添加私有字段时。

操作原因：编写私有字段可能会很耗时且重复。 使用此重构非常快捷，并使程序更可靠。

## <a name="how-to"></a>操作说明 

1. 将光标置于构造函数中的参数名称上。

2. 按“Ctrl”+**。** 触发“快速操作和重构”菜单。
   
3. 选择“创建和初始化字段”选项。

   ![从构造函数生成私有字段](media/generate-private-field-from-constructor.png)

## <a name="see-also"></a>请参阅 

- [重构](../refactoring-in-visual-studio.md)
