---
title: 生成构造函数快速操作
description: 了解如何使用“快速操作和重构”菜单快速为类上的新构造函数生成代码。
ms.custom: SEO-VS-2020
ms.date: 07/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 80de8b5c8b5699f4ddbf5148e16afd2da42388f2
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617547"
---
# <a name="generate-a-constructor-in-visual-studio"></a>在 Visual Studio 中生成构造函数

此代码生成适用于：

- C#

- Visual Basic

**功能：** 为类上的新构造函数快速生成代码。

**使用时机：** 想要引入新构造函数，并想要自动以适当的方式声明它，或要修改现有的构造函数时。

操作原因：可以在使用该构造函数之前对其进行声明，但此功能可自动使用适当的参数生成它。 此外，修改现有的构造函数需要更新所有的调用站点，使用此功能自动更新时除外。

方法：有多种生成构造函数的方法：

- [生成构造函数并选择成员](#pick)
- [生成包含属性的构造函数](#with)
- [从所选字段生成构造函数](#selection)
- [从新用法生成构造函数](#usage)
- [向现有的构造函数添加参数](#addparameter)
- [从构造函数参数创建和初始化字段/属性](#create)

## <a name="generate-constructor-and-pick-members-c-only"></a><a id = "pick"></a> 生成构造函数并选择成员（仅限 C#）

1. 将光标置于类中的任何空行：

   ![光标置于空行](media/constructor1-highlight-cs.png)

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 单击 :::image type="icon" source="media/screwdriver.png"::: 图标（如果文本光标已在此类中的空行上，它会出现在左边缘）。

   ![“生成构造函数”选项的屏幕截图。](media/constructor1-preview-cs.png)

1. 从下拉菜单中选择“生成构造函数”。

   “选取成员”对话框随即打开。

1. 选择要包含为构造函数参数的成员。 可使用上下箭头对其排序。 选择 **“确定”** 。

   ![选择成员对话框](media/constructor1-dialog-cs.png)

   > [!TIP]
   > 可以选中“添加 null 检查”复选框，为构造函数参数自动生成 null 检查。

   会使用指定的参数创建构造函数。

   ![此屏幕截图显示用指定参数创建的构造函数。](media/constructor1-result-cs.png)

## <a name="generate-constructor-with-properties-c-only"></a><a id = "with"></a> 生成包含属性的构造函数（仅限 C#）

1. 将光标放在实例上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择“在 `<QualifiedName>` 中生成构造函数(包含属性)”。

   ![“在 Key 中生成构造函数(包含属性)”选项的屏幕截图。](media/generate-constructor-with-properties.png)

## <a name="generate-constructor-from-selected-fields-c-only"></a><a id="selection"></a> 基于所选字段生成构造函数（仅限 C#）

1. 突出显示要在生成的构造函数中内附的成员：

   ![突出显示成员](media/constructor2-highlight-cs.png)

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 单击 :::image type="icon" source="media/screwdriver.png"::: 图标（如果文本光标已在包含选定内容的行上，它会出现在左边缘）。

      ![“生成构造函数 Person string string”选项的屏幕截图。](media/constructor2-preview-cs.png)

1. 从下拉菜单中选择“生成构造函数 'TypeName(...)'”。

   会使用所选的参数创建构造函数。

   ![此屏幕截图显示用选定参数创建的构造函数。](media/constructor2-result-cs.png)

## <a name="generate-constructor-from-new-usage-c-and-visual-basic"></a><a id="usage"></a> 基于新用法生成构造函数（C# 和 Visual Basic）

1. 将光标置于红色波浪线上。 红色波浪线表示尚无针对构造函数的任何调用。

   - C#：

       ![突出显示的代码 C#](media/constructor-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 VB](media/constructor-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 :::image type="icon" source="media/error-bulb.png"::: 图标。
      - 单击 :::image type="icon" source="media/error-bulb.png"::: 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![“在 Person 中生成构造函数”选项的屏幕截图。](media/constructor-preview-cs.png)

3. 从下拉菜单中选择“在 'TypeName' 中生成构造函数”。

   > [!TIP]
   > 进行选择前，使用预览窗口底部的“预览更改”链接[查看将发生的所有更改](../../ide/preview-changes.md)。

   使用从构造函数用法推断出的任意参数创建它。

   - C#：

       ![“生成方法”的结果 C#](media/constructor-result-cs.png)

   - Visual Basic：

       ![“生成方法”的结果 VB](media/constructor-result-vb.png)

## <a name="add-parameter-to-existing-constructor-c-only"></a><a id="addparameter"></a> 向现有构造函数添加参数（仅限 C#）

1. 从现有构造函数调用添加参数。

2. 将光标放在有红色波形曲线的行上，该曲线指示使用了尚不存在的构造函数。

    ![此屏幕截图显示了红色波形曲线所在的行。](media/constructor4-highlight-cs.png)

3. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 :::image type="icon" source="media/error-bulb.png"::: 图标。
      - 单击 :::image type="icon" source="media/error-bulb.png"::: 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![“将参数添加到 Person string string”选项的屏幕截图。](media/constructor4-preview-cs.png)

4. 从下拉菜单中选择“将参数添加到 'TypeName(...)'”。

   这会使用从参数用法推断出的类型将其添加到构造函数。

   ![屏幕截图：使用从参数用法推断出的类型将其添加到构造函数。](media/constructor4-result-cs.png)

还可以向现有方法添加参数。 有关详细信息，请参阅[向方法添加参数](add-parameter.md)。

## <a name="create-and-initialize-a-field-or-property-from-a-constructor-parameter-c-only"></a><a id="create"></a> 基于构造函数参数创建和初始化字段或属性（仅限 C#）

1. 查找现有构造函数并添加参数：

   ![显示现有构造函数的屏幕截图。](media/constructor5-highlight-cs.png)

1. 将光标置于新添加的参数中。

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单。
      - 单击 :::image type="icon" source="media/screwdriver.png"::: 图标（如果文本光标已在包含所添加的参数的行上，它会出现在左边缘）。

   ![“创建和初始化属性 Age”选项的屏幕截图。](media/constructor5-preview-cs.png)

1. 从下拉菜单中选择“创建并初始化属性”或“创建并初始化字段” 。

   这会声明并自动命名字段或属性，使其与你的类型相匹配。 还会添加一行代码，用于在构造函数正文中初始化字段或属性。

   ![屏幕截图：声明并自动命名字段或属性，使其与你的类型相匹配。](media/constructor5-result-cs.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
