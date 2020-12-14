---
title: 生成解构函数快速操作
description: 了解如何使用“快速操作和重构”菜单快速为新的解构函数生成方法存根。
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: ff2ac7682eff1c3da0597a95945a6a0b016d9213
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617248"
---
# <a name="generate-a-deconstructor-in-visual-studio"></a>在 Visual Studio 中生成解构函数

此代码生成适用于：

- C#

**功能：** 可以立即为新的解构函数生成方法存根。

**使用时机：** 需要自动正确解构类型。

操作原因：可以手动键入解构函数，但此功能将生成带有正确 out 参数的存根。

## <a name="generate-a-deconstructor"></a>生成解构函数

1. 声明具有指定的所需 out 参数的新类型。 如果找不到与声明匹配的解构实例，则此声明将导致错误。

   ![缺少解构函数错误](media/deconstruct.png)

2. 执行以下任一步骤：

   - **键盘**
      - 将光标置于声明中，选择 Ctrl+。 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 选择 :::image type="icon" source="media/screwdriver.png"::: 图标（如果文本光标已在此类中的空行上，它会出现在左边缘）。

      ![生成解构代码修补程序](media/deconstruct-codefix.png)

3. 选择“生成方法 'MyInternalClass.Deconstruct'”以生成解构函数。

   ![生成的解构函数代码](media/deconstruct-result.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)