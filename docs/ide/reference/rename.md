---
title: 重构重命名
ms.date: 05/04/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.rename
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 8d5b3d32b23b336dc86a92c33bcb97d02312f2dc
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84182947"
---
# <a name="rename-a-code-symbol-refactoring"></a>“重命名代码符号”重构

此重构适用于：

- C#

- Visual Basic

**功能：** 重命名代码符号的标识符，例如字段、本地变量、方法、命名空间、属性和类型。

**使用时机：** 想要安全地进行重命名（无需查找所有实例）并复制/粘贴新名称。

操作原因：复制和粘贴整个项目的新名称可能会导致错误。 此重构工具将准确地执行重命名操作。

## <a name="how-to"></a>操作说明

1. 突出显示要重命名的项，或将文本光标置于其中：

   - C#：

       ![突出显示的代码 - C#](media/rename-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 - Visual Basic](media/rename-highlight-vb.png)

2. 接下来，按如下所示使用键盘或鼠标：

   - **键盘**
      - 按“Ctrl+R”，然后按“Ctrl+R”。 （请注意，键盘快捷方式可能因所选的配置文件而有所不同。）
   - **鼠标**
      - 选择“编辑 > 重构 > 重命名”。
      - 右键单击代码并选择“重命名”。

3. 只需通过键入新名称即可重命名项。

   - C#：

      ![重命名动画 - C#](media/rename-animated-cs.gif)

   - Visual Basic：

      ![重命名 - VB](media/rename-rename-vb.png)

   > [!TIP]
   > 还可将注释和其他字符串更新为使用该新名称，也可在保存前使用“重命名”框（在编辑器的右上方）中的复选框[预览更改](../../ide/preview-changes.md)。

4. 对更改感到满意时，单击“应用”按钮或按 Enter 即可提交所做的更改 。

## <a name="remarks"></a>备注

- 从 Visual Studio 2019 16.3 版开始，在重命名与它所在的文件的名称相匹配的类型时，将出现一个复选框，你可以在其中同时重命名该文件。 重命名类、接口或枚举时，也会显示此选项。 具有多个定义的分部类型不支持此选项。

   ![使用文件重命名动画 - C#](media/rename-with-file-animated-cs.gif)

- 如果所用名称已存在（这可能导致冲突），“重命名”框将发出警告。

   ![重命名冲突](media/rename-conflict-cs.png)

- 重命名符号的另一种方法是在编辑器中更改其名称。 然后，当光标位于符号名称处，按 Ctrl+。 或者只需展开显示的灯泡图标菜单，选择“将 \<old name> 重命名为 \<new name>”。

   ![在编辑器中重命名](media/rename-with-editor-cs.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
