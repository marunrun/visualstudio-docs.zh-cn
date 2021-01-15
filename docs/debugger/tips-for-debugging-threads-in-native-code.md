---
title: 调试本机代码中的线程时的提示 | Microsoft Docs
description: 如果要在 Visual Studio 中调试多线程应用，请阅读有关调试本机代码中的线程的提示列表。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 9249e1527a7dd2ae720ab575b1d443c10b85376e
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98150049"
---
# <a name="tips-for-debugging-threads-in-native-code"></a>调试本机代码中的线程时的提示
下面是在调试本机代码中的线程时可以使用的一些提示：

- 可以通过在“监视”窗口或“快速监视”对话框中键入 `@TIB` 来查看“线程信息块”的内容 。

- 可以通过在“监视”窗口或“快速监视”对话框中输入 `@Err` 来查看当前线程的上一个错误代码 。

- 可以使用 C 运行库 (CRT) 函数来调试多线程应用程序。 有关详细信息，请参阅 [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)。

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [调试本机代码](../debugger/debugging-native-code.md)