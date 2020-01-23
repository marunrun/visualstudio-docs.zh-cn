---
title: 生成构造函数快速操作
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 3c8259841af4511bd782bca1be222353634638f5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75569499"
---
# <a name="generate-a-constructor-in-visual-studio"></a>在 Visual Studio 中生成构造函数

此代码生成适用于：

- C#

- Visual Basic

**功能：** 为类上的新构造函数快速生成代码。

**使用时机：** 想要引入新构造函数，并想要自动以适当的方式声明它，或要修改现有的构造函数时。

操作原因：  可以在使用该构造函数之前对其进行声明，但此功能可自动使用适当的参数生成它。 此外，修改现有的构造函数需要更新所有的调用站点，使用此功能自动更新时除外。

 方法：有多种生成构造函数的方法：

- [生成构造函数并选择成员](#pick)
- [从所选字段生成构造函数](#selection)
- [从新用法生成构造函数](#usage)
- [向现有的构造函数添加参数](#addparameter)
- [从构造函数参数创建和初始化字段/属性](#create)

## <a id = "pick"></a> 生成构造函数并选择成员（仅限 C#）

1. 将光标置于类中的任何空行：

   ![光标置于空行](media/constructor1-highlight-cs.png)

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 单击 ![左边缘中](media/screwdriver.png) 图标（如果文本光标已在此类中的空行上，它会出现在左边缘）。

   ![生成构造函数预览](media/constructor1-preview-cs.png)

1. 从下拉菜单中选择“生成构造函数”  。

   “选取成员”  对话框随即打开。

1. 选择要包含为构造函数参数的成员。 可使用上下箭头对其排序。 选择 **“确定”** 。

   ![选择成员对话框](media/constructor1-dialog-cs.png)

   > [!TIP]
   > 可以选中“添加 null 检查”复选框，为构造函数参数自动生成 null 检查。 

   会使用指定的参数创建构造函数。

   ![生成构造函数结果](media/constructor1-result-cs.png)

## <a id="selection"></a> 基于所选字段生成构造函数（仅限 C#）

1. 突出显示要在生成的构造函数中内附的成员：

   ![突出显示成员](media/constructor2-highlight-cs.png)

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 单击 ![左边缘中](media/screwdriver.png) 图标（如果文本光标已在包含选定内容的行上，它会出现在左边缘）。

      ![生成构造函数预览](media/constructor2-preview-cs.png)

1. 从下拉菜单中选择“生成构造函数 'TypeName(...)'”  。

   会使用所选的参数创建构造函数。

   ![“生成构造函数”的结果](media/constructor2-result-cs.png)

## <a id="usage"></a> 基于新用法生成构造函数（C# 和 Visual Basic）

1. 将光标置于红色波浪线上。 红色波浪线表示尚无针对构造函数的任何调用。

   - C#：

       ![突出显示的代码 C#](media/constructor-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 VB](media/constructor-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 ![错误灯泡](media/error-bulb.png) 图标。
      - 单击 ![错误灯泡](media/error-bulb.png) 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![生成构造函数预览](media/constructor-preview-cs.png)

3. 从下拉菜单中选择“在 'TypeName' 中生成构造函数”  。

   > [!TIP]
   > 进行选择前，使用预览窗口底部的“预览更改”链接[查看将发生的所有更改](../../ide/preview-changes.md)  。

   使用从构造函数用法推断出的任意参数创建它。

   - C#：

       ![“生成方法”的结果 C#](media/constructor-result-cs.png)

   - Visual Basic：

       ![“生成方法”的结果 VB](media/constructor-result-vb.png)

## <a id="addparameter"></a> 向现有构造函数添加参数（仅限 C#）

1. 从现有构造函数调用添加参数。

2. 将光标放在有红色波形曲线的行上，该曲线指示使用了尚不存在的构造函数。

    ![生成构造函数突出显示](media/constructor4-highlight-cs.png)

3. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 ![错误灯泡](media/error-bulb.png) 图标。
      - 单击 ![错误灯泡](media/error-bulb.png) 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

      ![生成构造函数预览](media/constructor4-preview-cs.png)

4. 从下拉菜单中选择“将参数添加到 'TypeName(...)'”  。

   这会使用从参数用法推断出的类型将其添加到构造函数。

   ![生成构造函数结果](media/constructor4-result-cs.png)

还可以向现有方法添加参数。 有关详细信息，请参阅[向方法添加参数](add-parameter.md)。

## <a id="create"></a> 基于构造函数参数创建和初始化字段或属性（仅限 C#）

1. 查找现有构造函数并添加参数：

   ![生成构造函数突出显示](media/constructor5-highlight-cs.png)

1. 将光标置于新添加的参数中。

1. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 单击 ![左边缘中](media/screwdriver.png) 图标（如果文本光标已在包含所添加的参数的行上，它会出现在左边缘）。

   ![生成构造函数预览](media/constructor5-preview-cs.png)

1. 从下拉菜单中选择“创建并初始化属性”或“创建并初始化字段”   。

   这会声明并自动命名字段或属性，使其与你的类型相匹配。 还会添加一行代码，用于在构造函数正文中初始化字段或属性。

   ![生成构造函数结果](media/constructor5-result-cs.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
