---
title: 扩展调试器的路线图 |微软文档
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
ms.openlocfilehash: e809eeb6a1a5d2c24368932713d69c7199b5af38
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713138"
---
# <a name="roadmap-for-extending-the-debugger"></a>扩展调试器的路线图
本文档提供有关 使用 扩展调试器的[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)]指南和参考信息。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试文档包括示例、全面的参考和几个具有代表性的方案，这些方案演示了自定义调试器的典型方法。

 编译器及其输出确定在产品中设置调试所需的内容。 如果编译器：

- 以 Windows 本机操作系统为目标并写入 *。PDB*文件，您可以使用集成到 的本机代码调试引擎 （DE） 调试程序[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 不需要实现 DE 或表达式赋值器。 表达式赋值器是为C++编程语言的语法而编写的。

- 生成 Microsoft 中间语言 （MSIL） 输出，您可以使用托管代码调试引擎 DE 调试程序，该引擎[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]也集成到 中。 因此，您只需要实现表达式赋值器。 为您提供一个示例表达式赋值器。 有关详情，请参阅以下主题：

   [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [计算表达式](../../extensibility/debugger/evaluating-expressions.md)

   [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)

   [中断模式下的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [编写通用语言运行时表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- 以专有操作系统或其他运行时环境为目标，您需要编写自己的 DE。 提供了一个教程，用于使用 ATL COM 创建简单的 DE。 有关详情，请参阅以下主题：

   [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [教程：使用 ATL COM 构建调试引擎](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)

   [实施端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)

   [示例](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
