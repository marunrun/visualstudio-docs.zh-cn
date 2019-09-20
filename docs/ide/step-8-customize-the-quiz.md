---
title: 步骤 8：自定义测验
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.devlang:
- csharp
- vb
dev_langs:
- CSharp
- VB
ms.assetid: dc8edb13-1b23-47d7-b859-8c6f7888c1a9
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 86fb0b7d22e02e563fe022b470651e2c335e4000
ms.sourcegitcommit: 541a0556958201ad6626bc8638406ad02640f764
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71079458"
---
# <a name="step-8-customize-the-quiz"></a>步骤 8：自定义测验

在本教程的最后一部分中，您将了解一些自定义测验和扩展所学内容的方式。 例如，可考虑程序如何创建一个答案永不为分数的随机除法问题。 若要了解详细信息，请将 `timeLabel` 控件更改为其他颜色，并为测验者提供提示。

> [!NOTE]
> 本主题是基本编码概念教程系列中的一部分。
> - 有关本教程的概述，请参阅[教程 2：创建计时数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。
> - 若要下载完整版代码，请参阅[数学测验教程的完整示例](https://code.msdn.microsoft.com/Complete-Math-Quiz-8581813c)。

## <a name="to-customize-the-quiz"></a>自定义测验

- 通过设置“timeLabel”控件的“BackColor”属性，使其在测验只剩下 5 秒时变为红色   。

  ```csharp
  timeLabel.BackColor = Color.Red;
  ```

  ```vb
  timeLabel.BackColor = Color.Red
  ```

  > [!IMPORTANT]
  > 使用此页右上角的编程语言控件查看 C# 代码片段或 Visual Basic 代码片段。<br><br>![Docs.Microsoft.com 的编程语言控件](../ide/media/docs-programming-language-control.png)

  当测验结束时重置颜色。

- 当测验参加者在 <xref:System.Windows.Forms.NumericUpDown> 控件中输入正确答案时，通过播放声音来进行提示。 （您必须为每个控件的 <xref:System.Windows.Forms.NumericUpDown.ValueChanged> 事件编写事件处理程序，只要用户更改控件的值，就激发该事件。）

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程，请参阅[教程 3：  创建匹配游戏](../ide/tutorial-3-create-a-matching-game.md)。

- 要返回上一个教程步骤，请参阅[步骤 7：添加乘法和除法问题](../ide/step-7-add-multiplication-and-division-problems.md)。
