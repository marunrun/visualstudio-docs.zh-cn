---
title: 生成方法重写
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 3c3a8f4eaf863fd8174ff70339fffc80141fc38d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75569239"
---
# <a name="generate-an-override-in-visual-studio"></a>在 Visual Studio 中生成方法重写

此代码生成适用于：

- C#

- Visual Basic

**功能：** 快速生成针对任意方法的代码，以从基类替代它。

**使用时机：** 想要重写一个基类方法并自动生成签名时。

操作原因：  可以自己编写方法签名，但此功能可自动生成签名。

## <a name="how-to"></a>操作说明

1. 在 C# 中键入 `override` 或在 Visual Basic 中键入 `Overrides`，后接空格（可在此处插入重写方法）。

   - C#：

      ![重写 IntelliSense C#](media/override-intellisense-cs.png)

   - Visual Basic：

      ![重写 IntelliSense VB](media/override-intellisense-vb.png)

2. 从基类中选择要重写的方法。

   > [!TIP]
   > - 使用“属性”图标 ![“属性”图标](media/override-property-cs.png) 显示或隐藏列表中的属性。
   > - 使用“方法”图标 ![“方法”图标](media/override-method-cs.png) 显示或隐藏列表中的方法。

   所选方法或属性将作为替代添加到类中以供实现。

   - C#：

       ![重写结果 C#](media/override-result-cs.png)

   - Visual Basic：

       ![重写结果 VB](media/override-result-vb.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
