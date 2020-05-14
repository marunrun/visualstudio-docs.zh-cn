---
title: 语言服务对调试的支持 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c80e8e1f584b1728f342cb596b689f6a22c9297
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707434"
---
# <a name="language-service-support-for-debugging"></a>用于调试的语言服务支持
语言服务可以提供通过接口支持调试器的功能<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>。 这些功能包括验证断点和向 **"自动"** 窗口提供表达式列表。

 但是，您需要有一个表达式赋值器来调试您的语言。 表达式赋值器负责在调试时评估表达式以生成值。 有关实现 CLR 表达式赋值器的信息，请参阅：

- [CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)

- [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

## <a name="compiler-output"></a>编译器输出
 编译器类型确定需要执行哪些操作来实现语言的调试。 如果编译器以 Windows 操作系统为目标并编写 .pdb 文件，则可以使用集成到 Visual Studio 的本机代码调试引擎来调试程序。 如果编译器生成 Microsoft 中间语言 （MSIL），则可以使用托管代码调试引擎调试程序，该引擎也将集成到 Visual Studio 中。 如果编译器以专有操作系统或不同的运行时环境为目标，则需要编写自己的调试引擎。

 有关实现语言调试的详细信息，请参阅在可视化工作室调试 SDK 中[入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)。
