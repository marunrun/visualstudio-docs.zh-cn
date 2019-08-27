---
title: 步骤 4：添加 checktheanswer （） 方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: c66f3831-b4a0-40bc-a109-8f46f4db35ed
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a9806bad150a5d03a942c7dfb36753f91d10536e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442563"
---
# <a name="step-4-add-the-checktheanswer-method"></a>步骤 4：添加 CheckTheAnswer() 方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本教程的第 4 部分中，您将编写一个方法 `CheckTheAnswer()`，用于判定数学题的答案是否正确。 本主题是基本编码概念教程系列中的一部分。 有关本教程的概述，请参阅[教程 2：创建计时的数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。  
  
> [!NOTE]
> 如果您一直使用 Visual Basic 学习本教程，则将使用 `Function` 关键字而不是一般的 `Sub` 关键字，因为此方法将返回一个值。 真的很简单：sub 不会返回值，但函数会返回值。  
  
### <a name="to-verify-whether-the-answers-are-correct"></a>验证答案是否正确  
  
1. 添加 `CheckTheAnswer()` 方法。  
  
     当调用此方法时，它将 addend1 和 addend2 的值相加，然后将结果与 sum `NumericUpDown` 控件的值进行比较。 如果二者相等，则此方法将返回值 `true`。 否则，此方法将返回值 `false`。 你的代码应类似以下内容。  
  
     [!code-csharp[VbExpressTutorial3Step4#8](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step4/cs/form1.cs#8)]
     [!code-vb[VbExpressTutorial3Step4#8](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step4/vb/form1.vb#8)]  
  
     接下来，您将通过更新计时器 Tick 事件处理程序方法中的代码来调用新的 `CheckTheAnswer()` 方法检查答案。  
  
2. 将下面的代码添加到 `if else` 语句。  
  
     [!code-csharp[VbExpressTutorial3Step4#10](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step4/cs/form1.cs#10)]
     [!code-vb[VbExpressTutorial3Step4#10](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step4/vb/form1.vb#10)]  
  
     如果答案正确，`CheckTheAnswer()` 将返回 `true`。 事件处理程序停止计时器，并显示祝贺消息，然后使“开始”按钮再次可用。 否则，继续进行测验。  
  
3. 保存并运行您的程序，开始测验，并提供加法题的正确答案。  
  
    > [!NOTE]
    > 在输入答案时，您必须在开始输入答案前选择默认值或手动删除零。 您将在本教程的后面部分中纠正这一行为。  
  
     提供正确答案后，将打开一个消息框，“开始”按钮变得可用，同时计时器将停止。  
  
### <a name="to-continue-or-review"></a>继续或查看  
  
- 要转到下一个教程步骤，请参阅[步骤 5：将添加 Enter 事件处理程序为 NumericUpDown 控件](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)。  
  
- 要返回上一个教程步骤，请参阅[步骤 3：添加一个倒计时计时器](../ide/step-3-add-a-countdown-timer.md)。
