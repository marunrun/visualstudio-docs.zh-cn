---
title: 扩展调试器的路线图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 89a07bc5a5c4c8b7a6054b53610325c654355bc8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695958"
---
# <a name="roadmap-for-extending-the-debugger"></a>扩展调试器的路线图
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

此文档提供了用来扩展调试器的指南和参考信息 [!INCLUDE[vs_current_short](../../includes/vs-current-short-md.md)] [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试文档包括示例、全面的参考和多个代表方案，这些方案演示了自定义调试器的典型方式。  
  
 编译器及其输出会确定在您的产品中实现调试需要执行哪些操作。 如果编译器：  
  
- 面向 Windows 本机操作系统并写入。PDB 文件，你可以通过将集成到中的本机代码调试引擎 (DE) 调试程序 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 不需要实现 "DE 计算器" 或 "表达式计算器"。 表达式计算器是用 c + + 编程语言的语法编写的。  
  
-  (MSIL) 输出生成 Microsoft 中间语言，你可以用托管代码调试引擎 DE 调试程序，该程序也集成到中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 因此，只需实现表达式计算器。 提供了一个示例表达式计算器。 有关详细信息，请参阅下列主题：  
  
     [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)  
  
     [计算表达式](../../extensibility/debugger/evaluating-expressions.md)  
  
     [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)  
  
     [中断模式中的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)  
  
     [编写公共语言运行时表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
  
- 针对专有操作系统或其他一些运行时环境，需要编写自己的 DE。 提供了一个使用 ATL COM 创建简单的 DE 的教程。 有关详细信息，请参阅下列主题：  
  
     [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
  
     [教程：使用 ATL COM 构建调试引擎](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)  
  
     [实现端口提供程序](../../extensibility/debugger/implementing-a-port-supplier.md)  
  
     [示例](../../extensibility/debugger/visual-studio-debugging-samples.md)  
  
## <a name="see-also"></a>另请参阅  
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
