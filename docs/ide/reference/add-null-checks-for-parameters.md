---
title: 为所有（参数）添加 null 检查
description: 了解如何创建用于检查所有可为空的、非选中参数是否为 Null 的 if 语句并将其添加到代码中。
ms.custom: SEO-VS-2020
ms.date: 09/17/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 5828a2bb28f7b3085cd5d43c452c520a730b8175
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "95870958"
---
# <a name="add-null-checks-for-all-parameters"></a>为所有参数添加 null 检查 

此重构适用于： 

- C# 

**功能：** 创建并添加用于检查所有可以为 null 的非选中参数是否为 null 的 `if` 语句。 

**使用时机：** 需要为所有适用的方法参数快速添加 null 检查。

操作原因：编写多个参数的 null 检查可能会很耗时且重复。 使用此重构非常快捷，并使程序更可靠。  

## <a name="how-to"></a>操作说明 

1. 将光标置于方法中的任何参数上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

   ![快速操作和重构](media/add-null-checks-for-all-parameters.png)
   
3. 选择“为所有参数添加 null 检查”选项。

   ![为所有添加 null 检查](media/add-null-checks-for-all.png) 

## <a name="see-also"></a>另请参阅 

- [重构](../refactoring-in-visual-studio.md)
