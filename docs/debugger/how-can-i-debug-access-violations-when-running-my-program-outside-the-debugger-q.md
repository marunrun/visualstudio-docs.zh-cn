---
title: 在 Visual Studio 外部运行应用时调试访问冲突
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.access
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 780a298a-132e-4245-8370-8c82ca27c6c1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5bbc129c4f5f4aa4d3ed1c6e346f9f8ab0395230
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852173"
---
# <a name="how-can-i-debug-access-violations-when-running-my-program-outside-the-debugger"></a>在调试器外部运行程序时如何调试访问冲突？

## <a name="problem-description"></a>问题描述
 我的程序在 Visual Studio 环境中运行良好，但在 Windows 操作系统中独立运行时发生访问冲突。 如何调试该问题？

## <a name="solution"></a>解决方案
 设置[实时调试](../debugger/just-in-time-debugging-in-visual-studio.md)选项并运行独立程序，直到发生访问冲突。 然后，在”访问冲突”对话框中，你可以单击”取消”以启动调试器 。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)