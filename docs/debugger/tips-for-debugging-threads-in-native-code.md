---
title: 调试本机代码中的线程的提示 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], threads
ms.assetid: 0374c8c6-57a3-4cfe-8047-2effef5ff5dc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 8ee1f1f2f2029325e3d3b87ca44d05d800a62c07
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901870"
---
# <a name="tips-for-debugging-threads-in-native-code"></a>调试本机代码中的线程时的提示
下面是在调试本机代码中的线程时可以使用的一些提示：

- 可以通过在“监视”窗口或“快速监视”对话框中键入 `@TIB` 来查看“线程信息块”的内容。

- 可以通过在“监视”窗口或“快速监视”对话框中输入 `@Err` 来查看当前线程的上一个错误代码。

- 可以使用 C 运行库 (CRT) 函数来调试多线程应用程序。 有关详细信息，请参阅 [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)。

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [调试本机代码](../debugger/debugging-native-code.md)