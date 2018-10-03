---
title: '调试 F # |Microsoft Docs'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Debugging [F#]
- F#, debugging
ms.assetid: 20bcd51c-2d06-4281-9a1e-ef2b91d1a779
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a5790b81eedb1a1bb9dc65b7ce053089c3bc1470
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47468640"
---
# <a name="debugging-f"></a>调试 F# #
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[调试 F #](https://docs.microsoft.com/visualstudio/debugger/debugging-f-hash)。  
  
调试 F# 与调试任何托管语言类似，但有以下几种例外情况：  
  
-   **自动**窗口不会显示 F # 变量。  
  
-   F# 不支持“编辑并继续”。 在调试会话期间编辑 F# 代码是可以的，但应避免这样做。 因为在调试会话期间无法应用代码更改，所以在调试期间编辑 F# 代码将导致源代码和正在进行调试的代码之间不匹配。  
  
-   调试器无法识别 F# 表达式。 若要在 F# 调试期间在调试器窗口或对话框中输入表达式，必须将该表达式转换为 C# 语法。 在将 F# 表达式转换为 C# 时，请务必记住 C# 使用 == 作为比较运算符中的等号，而 F# 使用单个 =。  
  
## <a name="see-also"></a>请参阅  
 [调试托管代码](../debugger/debugging-managed-code.md)


