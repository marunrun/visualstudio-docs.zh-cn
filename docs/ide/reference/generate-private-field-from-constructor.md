---
title: 从构造函数生成私有字段和属性
description: 了解如何使用“快速操作和重构”菜单从构造函数生成私有字段和属性。
ms.custom: SEO-VS-2020
ms.date: 06/20/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: e989efed8b58746312ed5f5a510efa049393f3db
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617456"
---
# <a name="generate-private-field-and-property-from-constructor"></a>从构造函数生成私有字段和属性

此重构适用于： 

- C# 

**功能：** 从构造函数生成私有字段或属性。 

**使用时机：** 希望从构造函数快速添加和初始化私有字段或属性。

操作原因：编写私有字段和属性可能会很耗时且重复。 使用此重构非常快捷，并使程序更可靠。

## <a name="how-to"></a>操作说明 

1. 将光标置于构造函数中的参数名称上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   
3. 接下来，在下列各项中选择一项:

- “创建并初始化字段”或“创建并初始化属性”。

   ![从构造函数生成私有字段](media/generate-private-field-from-constructor.png)

## <a name="see-also"></a>请参阅 

- [重构](../refactoring-in-visual-studio.md)
