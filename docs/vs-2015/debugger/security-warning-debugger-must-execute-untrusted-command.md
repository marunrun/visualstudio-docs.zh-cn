---
title: 安全警告：调试器必须执行不受信任的命令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.securityalert
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: e5c004b3-b364-4098-ac98-770076ca9981
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2a29ba026f9b3c2b8839d474c2d0833eb79f7ffd
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65683301"
---
# <a name="security-warning-debugger-must-execute-untrusted-command"></a>安全警告：调试器必须执行不受信任的命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用源服务器时，将出现此警告对话框。 它指示调试器需要执行以获取源代码的命令不在 srcsvr.ini 文件所包含的源服务器的受信任命令列表中。 如果这是一个有效命令，则可将其添加到 srcsvr.ini 文件中。 否则，不应运行该命令。 有关详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。  
  
## <a name="message-text"></a>消息正文  
 调试器必须执行以下不受信任的命令以从源服务器获取源代码。  
  
 如果调试符号文件 (\*.pdb) 不是来自已知且受信任的来源，则运行此命令可能无效或不安全。  
  
 **是否希望运行此命令？**  
  
## <a name="uielement-list"></a>UIElement 列表  
 文本框  
 来自 .pdb 文件的要运行的命令。  
  
 运行  
 允许该命令运行。  
  
 不运行  
 停止执行命令并停止从源服务器下载此文件。  
  
## <a name="see-also"></a>请参阅  
 [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [调试器安全](../debugger/debugger-security.md)   
 [源服务器](https://msdn.microsoft.com/library/windows/desktop/ms680641\(v=vs.85\).aspx)
