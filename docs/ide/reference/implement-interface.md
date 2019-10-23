---
title: 实现接口
ms.date: 01/26/2018
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 45265c10677b8d3eadc27eb3b6e22c69bb5299be
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658921"
---
# <a name="implement-an-interface-in-visual-studio"></a>在 Visual Studio 中实现接口

此代码生成适用于：

- C#

- Visual Basic

**功能：** 快速生成实现接口所需的代码。

**使用时机：** 想要继承接口时。

操作原因：  可以手动逐一实现各个接口，但此功能可自动生成所有方法签名。

## <a name="how-to"></a>操作说明

1. 将光标置于红色波浪线上，该线条表示已引用接口但部分必需成员尚未实现。

   - C#：

       ![突出显示的代码 C#](media/interface-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 VB](media/interface-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
   - **鼠标**
      - 右键单击并选择“快速操作和重构”菜单  。
      - 将鼠标悬停在红色波形曲线上，然后单击出现的 ![错误灯泡](media/error-bulb.png) 图标。
      - 单击 ![错误灯泡](media/error-bulb.png) 图标（如果文本光标已在具有红色波形曲线的行上，它会出现在左边缘）。

3. 从下拉菜单中选择“实现接口”  。

   ![“实现接口”预览](media/interface-preview-cs.png)

   > [!TIP]
   > - 进行选择前，使用预览窗口底部的“预览更改”链接[查看将发生的所有更改](../../ide/preview-changes.md)  。
   > - 通过预览窗口底部的“文档”、“项目”和“解决方案”链接，跨实现此接口的多个类创建适当的方法签名    。

   将创建接口的方法签名以供实现。

   - C#：

       ![“实现接口”的结果 C#](media/interface-result-cs.png)

   - Visual Basic：

       ![“实现接口”的结果 VB](media/interface-result-vb.png)

   > [!TIP]
   > （仅限 C#）使用“显式实现接口”选项，以接口名称作为各个生成方法的开头，避免名称冲突  。
   >
   > ![显式实现接口结果](media/interface-explicitresult-cs.png);

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)