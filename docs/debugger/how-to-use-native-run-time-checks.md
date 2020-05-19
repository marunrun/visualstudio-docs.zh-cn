---
title: 如何：使用本机运行时检查 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- c.runtime.errorchecks
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 954cf8436a9f0653685b41920cad84698ae50abb
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732158"
---
# <a name="how-to-use-native-run-time-checks"></a>如何：使用本机运行时检查
在 Visual Studio C++ 项目中，可以使用本机 [runtime_checks](/cpp/preprocessor/runtime-checks) 捕获常见的运行时错误，例如：

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

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [初探调试器](../debugger/debugger-feature-tour.md)
- [runtime_checks](/cpp/preprocessor/runtime-checks)
- [运行时错误检查](/cpp/c-runtime-library/run-time-error-checking)