---
title: 生成字段、属性、局部变量
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b554aa5586150942c0fc7d7aeada9356a67029ca
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595600"
---
# <a name="generate-a-field-property-or-local-variable-in-visual-studio"></a>在 Visual Basic 中生成字段、属性或局部变量

此代码生成适用于：

- C#

- Visual Basic

**功能：** 为之前未声明的字段、属性或本地内容快速生成代码。

**使用时机：** 键入时想要引入新字段、属性或本地内容，并想要自动以适当的方式对其进行声明时。

操作原因：  可以在使用该字段、属性或本地内容之前对其进行声明，但此功能可自动生成声明和类型。

## <a name="how-to"></a>操作说明

1. 将光标置于红色波浪线上。 红色波浪线表示尚无任何字段、本地内容或属性。

   - C#：

       ![突出显示的代码 C#](media/field-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 VB](media/field-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 ![错误灯泡](media/error-bulb.png) 图标。
      - 单击 ![错误灯泡](media/error-bulb.png) 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![生成字段/属性/本地内容预览](media/field-preview-cs.png)

3. 可从下拉菜单中选择一种生成选项。

   > [!TIP]
   > 进行选择前，使用预览窗口底部的“预览更改”链接[查看将发生的所有更改](../../ide/preview-changes.md)  。

   通过从字段、属性或本地内容用法推断出的类型来创建它们。

   - C#：

       ![“生成方法”的结果 C#](media/field-result-cs.png)

   - Visual Basic：

       ![“生成方法”的结果 VB](media/field-result-vb.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
