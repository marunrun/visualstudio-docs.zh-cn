---
title: 调试 Windows API 函数 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.api
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], Windows API functions
- NT symbols and debugging Windows API functions
- Windows API functions, debugging
- Windows API, debugging API functions
- APIs, debugging
ms.assetid: 7c126f57-62ab-4d94-9805-632d696ba1f0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7b5f3842160f4ffc6cecd41e65dd05ab7566dd0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734353"
---
# <a name="how-can-i-debug-windows-api-functions"></a>如何调试 Windows API 函数？
如果要调试加载了 NT 符号的 Windows API 函数，必须执行以下步骤。

### <a name="to-set-a-breakpoint-on-a-windows-api-function-with-nt-symbols-loaded"></a>若要在加载了 NT 符号的 Windows API 函数中设置断点

- 输入函数名以及函数所在 DLL 的名称。 在 32 位代码中，使用函数名的修饰形式。 例如，若要给”MessageBeep” 设置断点，你必须输入如下内容。

    ```cpp
    {,,USER32.DLL}_MessageBeep@4
    ```

     若要获取修饰名称，请参阅[查看修饰名](https://msdn.microsoft.com/library/f79e2717-a4db-4d12-a689-69830cce2be0)。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)
