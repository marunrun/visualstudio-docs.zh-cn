---
title: PTVS 入门：交互式 Python | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: fa594314-bdd0-4da5-874a-57b03414b675
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 4fba8bf658a50a7a7e28abace1eb622ab14f5f26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62550982"
---
# <a name="getting-started-with-ptvs-interactive-python"></a>PTVS 入门：交互式 Python
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

交互式提示或读取-求值-输出循环 (REPL) 是高效编程语言的重要工具。  它们允许执行代码段以发现和了解 API、使用 API 进行体验，并以交互方式开发要包括在项目或程序中的工作代码。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=yc2CROtTsC0&index=5&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)中观看这些说明。  
  
 在“Python 环境”窗口中，你将看到所有 Python 环境的列表。  你可以选择其中任意一个以打开交互式窗口或 REPL。  如果曾经在命令提示符下运行 Python.exe，那么你之前已经看到了 python REPL。  REPL 会发出提示，你可以输入代码，按 Enter，并立即看到代码结果。  这是一个实时执行上下文，其中包含所有执行、变量赋值等的所有状态。 可以引用保存结果的变量，稍后将其提交到复制提示。  你可以编写多行代码并一次执行全部代码（例如，一个方法声明或多个语句）。  
  
 当你开始使用新库时，REPL 是尝试访问该库的好办法。  你可以导入该库，检查子包、类和函数。  Python 可以通过其 `help()` 函数告诉你所有相关信息。  此外，Python Tools for Visual Studio (PTVS) 会基于其编辑器中使用的代码建模为你提供建议和文档，这个过程无需执行库。  当实际执行代码时，PTVS 将根据 Python 运行时中的信息改进 PTVS 建议。  
  
 交互式窗口对于迭代或演化代码开发也非常有用，包括在开发时对代码进行测试。  可以在编辑器窗口中选择一个函数，按右指针按钮，并选择“发送到 Interactive”。  此命令将选择复制到交互式窗口作为下一个输入并加以执行。  你将立即看到结果。  如果需要对前一个输入进行更改，可以按向上键取回代码，进行修，然后按 Ctrl + Enter 执行代码。  在输入结束时按 Enter 将执行它，但在输入过程中按 Enter 将插入新行。  
  
 你可以对每个 Python 安装打开一个交互式窗口，无论多少都可以。  窗口顶部有一些按钮，用于清除显示、重置执行上下文等。 历史记录将保持不变。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=yc2CROtTsC0&index=5&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)中观看这些说明。  
  
## <a name="see-also"></a>另请参阅  
 [Wiki 文档](https://github.com/Microsoft/PTVS/wiki/Interactive-REPL)   
 [PTVS 入门和深入了解视频](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
