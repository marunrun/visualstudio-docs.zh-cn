---
title: 步骤 10：为其他按钮和复选框编写代码
ms.date: 08/30/2019
ms.assetid: 185cf370-ab39-4ac0-b6bc-601d5b95a4a2
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e99e3bf3f6b8adc88eca94be4d9f5a1bb9b8c7a7
ms.sourcegitcommit: 6eed0372976c0167b9a6d42ba443f9a474b8bb91
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2019
ms.locfileid: "71118931"
---
# <a name="step-10-write-code-for-additional-buttons-and-a-check-box"></a>步骤 10：为其他按钮和复选框编写代码

现在，您可以完成其他四个方法了。 虽然您可以复制并粘贴此代码，但是若想从此教程中学些到最多的内容，那么请键入代码并使用 IntelliSense。

此代码将为您之前添加的按钮添加功能。 如果不使用此代码，这些按钮将不执行任何操作。 当您激活控件时，这些按钮将使用其 <xref:System.Windows.Forms.Control.Click> 事件（复选框使用 <xref:System.Windows.Forms.CheckBox.CheckedChanged> 事件）来执行不同的操作。 例如，`clearButton_Click`（或 `ClearButton_Click`）事件（当选择“清除图片”按钮时激活），在将其“图像”属性设置为“null”（或“无”）后，可擦除当前的图像     。 代码中的每个事件都包括一些注释，用于解释代码所执行的操作。

> [!TIP]
> 作为最佳做法：请始终为代码添加注释。 注释是供用户阅读的信息，花些时间使您的代码易于理解是值得的。 应用会忽略注释行上的所有内容。 在 C# 中，通过在开头键入两个正斜杠 (//) 来注释一行；在 Visual Basic 中，通过以单引号 (') 开头来注释一行。

## <a name="how-to-write-code-for-additional-buttons-and-a-check-box"></a>如何为其他按钮和复选框编码代码

将以下代码添加到你的 Form1  代码文件（Form1.cs  或 Form1.vb  ）。
> [!IMPORTANT]
> 使用此页右上角的编程语言控件查看 C# 代码片段或 Visual Basic 代码片段。<br><br>![Docs.Microsoft.com 的编程语言控件](../ide/media/docs-programming-language-control.png)

  [!code-csharp[VbExpressTutorial1Step9_10#2](../ide/codesnippet/CSharp/step-10-write-code-for-additional-buttons-and-a-check-box_1.cs)]

  [!code-vb[VbExpressTutorial1Step9_10#2](../ide/codesnippet/VisualBasic/step-10-write-code-for-additional-buttons-and-a-check-box_1.vb)]

> [!NOTE]
> 代码可能未显示 camelCase 字母。

## <a name="next-steps"></a>后续步骤

* 要转到下一个教程步骤，请参阅[步骤 11：运行应用并尝试其他功能](../ide/step-11-run-your-program-and-try-other-features.md)** 。

* 要返回上一个教程步骤，请参阅[步骤 9：检查代码、为代码添加注释和测试代码](../ide/step-9-review-comment-and-test-your-code.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
