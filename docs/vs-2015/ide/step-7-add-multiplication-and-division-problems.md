---
title: 步骤 7：添加乘法和除法问题 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: e638959e-f6a4-4eb4-b2e9-f63b7855cf8f
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 47623d7a65de85b50ad1910425052288a261e49d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178571"
---
# <a name="step-7-add-multiplication-and-division-problems"></a>步骤 7：添加乘法和除法问题
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本教程的第 7 部分中，您将添加乘法和除法题，但首先要考虑如何做出这种更改。 考虑与存储值相关的初始步骤。  
  
### <a name="to-add-multiplication-and-division-problems"></a>添加乘法和除法问题  
  
1. 再向窗体添加四个整型变量。  
  
     [!code-csharp[VbExpressTutorial3Step7#15](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#15)]
     [!code-vb[VbExpressTutorial3Step7#15](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#15)]  
  
2. 与前面的操作一样，修改 `StartTheQuiz()` 方法，以便为乘法和除法题填入随机数。  
  
     [!code-csharp[VbExpressTutorial3Step7#16](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#16)]
     [!code-vb[VbExpressTutorial3Step7#16](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#16)]  
  
3. 修改 `CheckTheAnswer()` 方法，使之同样检查乘法和除法题。  
  
     [!code-csharp[VbExpressTutorial3Step7#17](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#17)]
     [!code-vb[VbExpressTutorial3Step7#17](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#17)]  
  
     由于使用键盘无法方便地输入乘号 (×) 和除号 (÷)，因此 Visual C# 和 Visual Basic 接受用星号 (*) 代替乘号，用斜线 (/) 代替除号。  
  
4. 更改计时器 Tick 事件处理程序的最后部分，使其在时间用完时填入正确答案。  
  
     [!code-csharp[VbExpressTutorial3Step7#23](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#23)]
     [!code-vb[VbExpressTutorial3Step7#23](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#23)]  
  
5. 保存并运行程序。  
  
     如下图所示，测验对象必须回答四个问题才能完成测验。  
  
     ![包含四个问题的数学测验](../ide/media/express-finishedquiz.png "Express_FinishedQuiz")  
包含四个问题的数学测验  
  
### <a name="to-continue-or-review"></a>继续或查看  
  
- 要转到下一个教程步骤，请参阅[步骤 8：自定义测验](../ide/step-8-customize-the-quiz.md)。  
  
- 要返回上一个教程步骤，请参阅[步骤 6：添加减法问题](../ide/step-6-add-a-subtraction-problem.md)。
