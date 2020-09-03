---
title: 用于调试的语言服务支持 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c61f7fa7e698e2c01cadb1dbb36a321c6e656e35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194997"
---
# <a name="language-service-support-for-debugging"></a>用于调试的语言服务支持
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

语言服务可以提供通过接口支持调试器的功能 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo> 。 这些功能包括验证断点并向 **自动窗口提供** 表达式列表。  
  
 但是，您需要使用表达式计算器来调试您的语言。 表达式计算器负责计算在调试时生成值的表达式。 有关实现 CLR 表达式计算器的信息，请参阅：  
  
- [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)  
  
- [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)  
  
## <a name="compiler-output"></a>编译器输出  
 编译器的类型决定了为语言实现调试需要执行的操作。 如果编译器以 Windows 操作系统为目标并写入 .pdb 文件，则可以使用集成到 Visual Studio 中的本机代码调试引擎调试程序。 如果编译器)  (MSIL 生成 Microsoft 中间语言，则可以通过托管代码调试引擎（也集成到 Visual Studio）调试程序。 如果编译器面向的是专用操作系统或不同的运行时环境，则需要编写自己的调试引擎。  
  
 若要深入了解如何实现语言调试，请参阅 Visual Studio 调试 SDK 中的 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) 。
