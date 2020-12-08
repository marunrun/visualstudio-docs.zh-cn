---
title: 扩展调试器的路线图 |Microsoft Docs
description: Visual Studio 调试文档包括示例、引用以及演示自定义调试器的典型方法的几个方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2574fe76faadf4284088c0d47592d0c5ba0d38f9
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96848334"
---
# <a name="roadmap-for-extending-the-debugger"></a>扩展调试器的路线图
此文档提供了用来扩展调试器的指南和参考信息 [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试文档包括示例、全面的参考和多个代表方案，这些方案演示了自定义调试器的典型方式。

 编译器及其输出确定在产品中设置调试所需的内容。 如果编译器：

- 面向 Windows 本机操作系统并写入 *。PDB* 文件，你可以通过将集成到中的本机代码调试引擎 (DE) 调试程序 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 不需要实现 "DE" 或 "表达式计算器"。 表达式计算器是用 c + + 编程语言的语法编写的。

-  (MSIL) 输出生成 Microsoft 中间语言，你可以用托管代码调试引擎 DE 调试程序，该程序也集成到中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 因此，只需实现表达式计算器。 提供了一个示例表达式计算器。 有关详细信息，请参阅下列主题：

   [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [计算表达式](../../extensibility/debugger/evaluating-expressions.md)

   [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)

   [中断模式下的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [编写公共语言运行时表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- 针对专有操作系统或其他一些运行时环境，需要编写自己的 DE。 提供了一个使用 ATL COM 创建简单的 DE 的教程。 有关详细信息，请参阅下列主题：

   [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [教程：使用 ATL COM 构建调试引擎](/previous-versions/bb147024(v=vs.90))

   [实现端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)

   [示例](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>另请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)