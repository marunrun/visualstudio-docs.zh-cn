---
title: DebugBreak 和 __debugbreak |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DebugBreak
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], DebugBreak function
- DebugBreak function
- breakpoints, DebugBreak function
ms.assetid: 9787c795-df94-4f48-bc8d-3bf899b67421
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b6c4b9d780caf7589eecdc709cbede577dd7a6fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62852699"
---
# <a name="debugbreak-and-debugbreak"></a>DebugBreak 和 __debugbreak
可以在代码中的任意点调用 DebugBreak Win32 函数或 [__debugbreak](/cpp/intrinsics/debugbreak) 内部函数。 `DebugBreak` 和 `__debugbreak` 具有与在该位置设置断点相同的效果。

 由于 `DebugBreak` 是对系统函数的调用，因此必须安装系统调试符号，以确保中断后显示正确的调用堆栈信息。 否则，调试器可能在显示一条调用堆栈信息后就停止显示。 如果使用 `__debugbreak`，则不需要符号。

## <a name="see-also"></a>请参阅
- [编译器内部函数](/cpp/intrinsics/compiler-intrinsics)
- [调试器安全](../debugger/debugger-security.md)
- [调试本机代码](../debugger/debugging-native-code.md)
- [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)