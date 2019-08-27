---
title: 安全警告：调试器必须执行不受信任的命令 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.securityalert
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: e5c004b3-b364-4098-ac98-770076ca9981
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7c4ab45feeae409a1951e1a57e964eaaa5963896
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902579"
---
# <a name="security-warning-debugger-must-execute-untrusted-command"></a>安全警告：调试器必须执行不受信任的命令
使用源服务器时，将出现此警告对话框。 它指示调试器需要执行以获取源代码的命令不在 srcsvr.ini 文件所包含的源服务器的受信任命令列表中。 如果这是一个有效命令，则可将其添加到 srcsvr.ini 文件中。 否则，不应运行该命令。 有关详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="message-text"></a>消息正文
 调试器必须执行以下不受信任的命令以从源服务器获取源代码。

 如果调试符号文件 (\*.pdb) 不是来自已知且受信任的来源，则运行此命令可能无效或不安全。

 **是否希望运行此命令？**

## <a name="uielement-list"></a>UIElement 列表
 从.pdb 文件文本框命令来运行。

 运行允许运行的命令。

 不运行停止执行命令和下载的源服务器中的文件。

## <a name="see-also"></a>请参阅
- [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [调试器安全](../debugger/debugger-security.md)
- [源服务器](/windows/desktop/Debug/source-server-and-source-indexing)