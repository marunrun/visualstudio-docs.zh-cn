---
title: 如何：使用本机运行时检查 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- c.runtime.errorchecks
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- /RTC compiler option [C++], /O compiler option
- run-time checks, native
- stack, pointer corruption
- stack pointers, corruption
- /O compiler option, /RTC option
- run-time errors, error checks
- O compiler option, /RTC option
- debugger, runtime errors
- variables [debugger], loss of data
- runtime_checks pragma
- variables [debugger], catching dependencies on uninitialized local variables
- run-time errors, debugging
- debugger, native run-time checks
- optimized build option
- RTC compiler option, /O compiler option
- native run-time checks
- run-time checks
- debugging arrays
- stack pointers
- arrays [Visual Studio], debugging
ms.assetid: dc7b2f1e-5ff6-42e0-89b3-dc9dead83ee1
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b50dda3e31e27fa5d177c3b0ba2790babd2a660f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685861"
---
# <a name="how-to-use-native-run-time-checks"></a>如何：使用本机运行时检查
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual C++ 中，可以使用本机 [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b) 捕获常见的运行时错误，例如：  
  
- 堆栈指针损坏。  
  
- 本地数组溢出。  
  
- 堆栈损坏。  
  
- 未初始化的局部变量上的依赖项。  
  
- 较短变量赋值的数据丢失。  
  
  如果使用带有优化 ( **/RTC** ) 版本的 **/O**，将导致编译器错误。 如果在优化版本中使用 `runtime_checks` 杂注，则该杂注无效。  
  
  调试启用了运行时检查的程序时，如果出现运行时错误，该程序的默认操作是停止并切换到调试器。 可以更改任何运行时检查的此默认行为。 有关详细信息，请参阅[使用调试器管理异常](../debugger/managing-exceptions-with-the-debugger.md)。  
  
  下面的过程介绍了如何在调试版本中启用本机运行时检查，以及如何修改本机运行时检查的行为。  
  
  本节的其他主题提供了有关以下方面的信息：  
  
- [用 C 运行库自定义运行时检查](../debugger/native-run-time-checks-customization.md)  
  
- [使用无 C 运行库的运行时检查](../debugger/using-run-time-checks-without-the-c-run-time-library.md)  
  
### <a name="to-enable-native-run-time-checks-in-a-debug-build"></a>在调试版本中启用本机运行时检查  
  
- 使用 **/RTC** 选项，并与 C 运行库（如 /MDd）调试版链接。  
  
### <a name="to-modify-native-run-time-check-behavior"></a>更改本机运行时检查操作  
  
- 使用 `runtime_checks` 杂注。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Studio 中调试](../debugger/debugging-in-visual-studio.md)   
 [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b)   
 [运行时错误检查](https://msdn.microsoft.com/library/c965dd01-57ad-4a3c-b1d6-5aa04f920501)
