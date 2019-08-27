---
title: 调试本机代码 |Microsoft Docs
ms.date: 04/11/2017
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging native code
- debugging [C++], native code
- debugging [Visual Studio], native code
- native code, debugging
ms.assetid: d94eee90-7e0d-4cac-88c1-9831030daa5e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 5a7cf0b150c45037941010bf7e611f4bc21252c7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851909"
---
# <a name="debugging-native-code"></a>调试本机代码
本节讲述本机应用程序的一些常见调试问题和调试技术。 本节阐述的技术属于高级别技术。 使用 Visual Studio 调试器的机制，请参阅[先来看一下调试器](../debugger/debugger-feature-tour.md))。

## <a name="in-this-section"></a>本节内容
 [如何：调试优化代码](../debugger/how-to-debug-optimized-code.md)为提示提供了有关调试优化的代码，具体而言，应调试未优化的版本的程序，调试和发布配置的默认优化设置的原因和提示为查找 bug 仅出现在优化代码 （在中打开优化调试生成配置） 中。

 [DebugBreak 和 __debugbreak](../debugger/debugbreak-and-debugbreak.md)描述了 Win32`DebugBreak`函数，并提供给它的平台 SDK 中的参考主题的链接。 还描述了 `__debugbreak` 内部。

 [C /C++断言](../debugger/c-cpp-assertions.md)讨论断言语句，它们的工作原理，使用它们 （捕捉逻辑错误，检查操作的结果和测试错误情况） 的优势与它们交互`_DEBUG`，和的类型中支持断言[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

 [如何：调试内联程序集代码](../debugger/how-to-debug-inline-assembly-code.md)提供简短说明在使用反汇编窗口查看程序集指令和寄存器窗口查看寄存器内容，并提供指向关于这些窗口的主题。

 [MFC 调试技术](../debugger/mfc-debugging-techniques.md)您链接到 MFC 程序，包括的调试技术： afxDebugBreak、 TRACE 宏，检测内存泄漏在 MFC 中，MFC 断言，并减小 MFC 调试生成。

 [CRT 调试技术](../debugger/crt-debugging-techniques.md)您链接到 C 运行时库，包括使用 CRT 调试库、 用于报告的宏的调试技术、 malloc 和 _malloc_dbg，编写调试挂钩函数以及 CRT 调试堆之间的差异。

 [调试本机代码常见问题](../debugger/debugging-native-code-faqs.md)提供有关调试 Visual 常见问题的解答C++程序

 [调试 COM 和 ActiveX](../debugger/com-and-activex-debugging.md)提供有关调试 COM 和 ActiveX 应用程序，包括的工具可用于 COM 和 ActiveX 调试的信息。

 [如何：调试插入代码](../debugger/how-to-debug-injected-code.md)提供有关调试使用特性的代码的指导。 指导信息包括如何打开“源批注”、如何查看插入的代码以及如何在当前执行点查看反汇编代码。

 [演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)介绍了如何使用**并行任务**并**并行堆栈**工具窗口调试并行应用程序。

## <a name="related-sections"></a>相关章节
 [VisualC++项目类型](../debugger/debugging-preparation-visual-cpp-project-types.md)提供指向描述如何调试视觉对象创建的本机项目类型的主题C++项目模板。

 [调试 DLL 项目](../debugger/debugging-dll-projects.md)提供有关如何调试本机和托管 Dll 的信息。

 [先来看一下调试器](../debugger/debugger-feature-tour.md)提供调试文档的较大章节的链接。 涉及的信息包括：调试器的新增功能、设置和准备、断点、处理异常、编辑和继续、调试托管代码、调试本机代码、调试 SQL 以及用户界面参考。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [在 Visual Studio 中进行调试](../debugger/index.md)