---
title: 扩展调试器的路线图 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89788f97937d05a3ca4858ed35fd854593ce3357
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315892"
---
# <a name="roadmap-for-extending-the-debugger"></a>扩展调试器的路线图
本文档提供了指南和参考信息，用于扩展[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)]调试器与[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试文档包括示例、 全面参考和几个有代表性的方案，展示了自定义调试器的典型方法。

 你的编译器和其输出确定所需设置在您的产品中进行调试。 如果您的编译器：

- 面向 Windows 本机操作系统并将写入 *。PDB*文件中，您可以使用本机代码调试引擎 (DE)，其集成到调试程序[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 不需要实现 DE 或表达式计算器。 表达式计算器编写其语法的C++编程语言。

- 生成的 Microsoft 中间语言 (MSIL) 输出，可以通过托管的代码调试引擎 DE，这也集成到调试程序[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 因此，只需实现的表达式计算器。 示例表达式计算器会为您提供。 有关详细信息，请参阅下列主题：

   [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [计算表达式](../../extensibility/debugger/evaluating-expressions.md)

   [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)

   [在中断模式下的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [编写公共语言运行时表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- 一个专有操作系统或某些其他运行时环境的目标，您需要编写您自己 DE。 提供创建简单的部署使用 ATL COM 的教程。 有关详细信息，请参阅下列主题：

   [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [教程：生成使用 ATL COM 的调试引擎](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)

   [实现端口提供程序](../../extensibility/debugger/implementing-a-port-supplier.md)

   [示例](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)