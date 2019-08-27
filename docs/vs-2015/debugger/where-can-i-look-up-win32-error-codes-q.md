---
title: 可以在哪里查阅 Win32 错误代码？ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vc.errors
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- error codes, Win32
- Win32, error codes
ms.assetid: 8fb4ff42-b8eb-4152-b49e-b802d194b05e
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d403315a2320589f69174109d55c8726ffd5f673
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149403"
---
# <a name="where-can-i-look-up-win32-error-codes"></a>可以在哪里查阅 Win32 错误代码？
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认系统安装的 INCLUDE 目录中的 WINERROR.H 包含 Win32 API 函数的错误代码定义。  
  
 可以通过在“监视”窗口或“快速监视”对话框中键入错误代码来查阅该代码   。 例如:  
  
```  
0x80000004,hr  
```  
  
## <a name="see-also"></a>请参阅  
 [调试本机代码常见问题](../debugger/debugging-native-code-faqs.md)   
 [调试本机代码](../debugger/debugging-native-code.md)
