---
title: 提取方法
description: 通过选择代码并按 Ctrl+R、Ctrl+M，将代码片段转换为自己的方法。
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 50f14cc2a7eafe5d65e0c6a6af54bafa2ebb5a1f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75569694"
---
# <a name="extract-a-method-refactoring"></a>“提取方法”重构

此重构适用于：

- C#

- Visual Basic

**功能：** 将代码片段转换为独立的方法。

**使用时机：** 需要从其他方法调用某些方法中现有的代码片段时。

操作原因：  可以复制/粘贴该代码，但这样会导致重复。 更好的解决方案是将此片段重构为独立的且可供任何其他方法自行调用的方法。

## <a name="how-to"></a>操作说明

1. 突出显示要提取的代码：

   - C#：

       ![突出显示的代码- C#](media/extractmethod-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 - Visual Basic](media/extractmethod-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl+R”  ，然后按“Ctrl+M”  。 （请注意，键盘快捷方式可能因所选的配置文件而有所不同。）
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单，然后从“预览”弹出窗口选择“提取方法”  。
   - **鼠标**
      - 选择“编辑 > 重构 > 提取方法”  。
      - 右键单击代码，然后选择“重构 > 提取 > 提取方法”  。
      - 右键单击代码，选择“快速操作和重构”  菜单，然后从“预览”弹出窗口选择“提取方法”  。

   将立即创建方法。 现在可以在此处为方法重命名，只需键入新的名称即可。

   > [!TIP]
   > 还可以将注释和其他字符串更新为使用该新名称，也可在保存前使用“重命名”  框（在 IDE 的右上方）中的复选框[预览更改](../../ide/preview-changes.md)。

   - C#：

      ![重命名方法 - C#](media/extractmethod-rename-cs.png)

   - Visual Basic：

      ![重命名方法 - Visual Basic](media/extractmethod-rename-vb.png)

3. 对更改感到满意时，单击“应用”按钮或按 Enter 即可提交所做的更改   。

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
