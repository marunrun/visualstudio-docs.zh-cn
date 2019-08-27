---
title: 步骤 8：自定义测验
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- csharp
- vb
ms.assetid: dc8edb13-1b23-47d7-b859-8c6f7888c1a9
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1868cd30cc41187ac995e71ee86d81dd0fb83d5a
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416459"
---
# <a name="step-8-customize-the-quiz"></a>步骤 8：自定义测验
在本教程的最后一部分中，您将了解一些自定义测验和扩展所学内容的方式。 例如，可考虑程序如何创建一个答案永不为分数的随机除法问题。 若要了解详细信息，请将 `timeLabel` 控件更改为其他颜色，并为测验者提供提示。

## <a name="to-customize-the-quiz"></a>自定义测验

- 通过设置“timeLabel”控件的“BackColor”属性，使其在测验只剩下 5 秒时变为红色  

```csharp
timeLabel.BackColor = Color.Red;
```

```vb
timeLabel.BackColor = Color.Red
```

当测验结束时重置颜色。

- 当测验参加者在 <xref:System.Windows.Forms.NumericUpDown> 控件中输入正确答案时，通过播放声音来进行提示。 （您必须为每个控件的 <xref:System.Windows.Forms.NumericUpDown.ValueChanged> 事件编写事件处理程序，只要用户更改控件的值，就激发该事件。）

## <a name="to-continue-or-review"></a>继续或查看

- 若要下载测验的完整版本，请参阅[数学测验教程的完整示例](https://code.msdn.microsoft.com/Complete-Math-Quiz-8581813c)。

- 要转到下一个教程，请参阅[教程 3：创建匹配游戏](../ide/tutorial-3-create-a-matching-game.md)。

- 要返回上一个教程步骤，请参阅[步骤 7：添加乘法和除法问题](../ide/step-7-add-multiplication-and-division-problems.md)。
