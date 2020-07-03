---
title: 如何 - 调试 .NET Framework 源代码 | Microsoft Docs
ms.date: 11/19/2018
ms.topic: how-to
helpviewer_keywords:
- debugging, .NET Framework source
ms.assetid: fc12e472-ac6a-4e77-8e22-a769e13a03b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 3f043aae44231608fb514e87a05717f4aeb924bc
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350090"
---
# <a name="how-to-debug-net-framework-source"></a>如何：调试 .NET Framework 源代码

若要调试 .NET Framework 源代码，你必须：

- 启用 .NET Framework 源代码单步执行。

- 具有访问代码调试符号的权限。

  你可以选择立即下载调试符号，也可以设置相关选项以便稍后下载。 如果不立即下载符号，则在你下次开始调试应用时会下载它们。 调试时，你还可以使用“模块”或“调用堆栈”窗口下载和加载符号。

### <a name="to-enable-stepping-into-net-framework-source"></a>启用 .NET Framework 源代码单步执行

1. 在“工具”（或“调试”）>“选项” > “调试” > “常规”下，选择“启用 .NET Framework 源代码单步执行”。

   - 如果您先前启用了“仅我的代码”，则会出现一个警告对话框，提示您“仅我的代码”现在已禁用。 选择“确定”。

   - 如果没有设置本地符号缓存，则会出现一个警告对话框，提示已设置默认符号缓存。 选择“确定”。

1. 选择“确定”关闭“选项”对话框 。

### <a name="to-set-or-change-symbol-source-locations-and-loading-behavior"></a>设置或更改符号源位置和加载行为

1. 在“工具”（或“调试”）>“选项” > “调试”下选择“符号”类别。

1. 在“符号”页的”符号文件(.pdb)位置”下，选择“Microsoft 符号服务器”以访问公共 Microsoft 符号服务器中的符号。 选择工具栏按钮以添加其他符号位置并更改加载顺序。

1. 若要更改本地符号缓存，可编辑或浏览到“在此目录下缓存符号”下的其他位置。

1. 若要立即下载符号，请选择“加载所有符号”。 此按钮仅在调试时可用。

   如果现在不下载符号，则在你下次开始调试时会下载它们。

1. 选择“确定”关闭“选项”对话框 。

### <a name="to-load-symbols-from-the-modules-or-call-stack-windows"></a>从“模块”或“调用堆栈”窗口加载符号

1. 在调试期间，通过选择“调试” > “窗口” > “模块”（或按 Ctrl + Alt + U）或“调试” > “窗口” > “调用堆栈”(Ctrl + Alt + C) 打开窗口。

1. 右键单击未加载符号的模块。 在“模块”窗口中，符号加载状态位于“符号状态”列中。 在“调用堆栈”窗口中，状态位于“帧状态”列中，且帧显示为灰色。

   - 从菜单中选择“加载符号”，以从计算机上的文件夹中查找和加载符号文件。

   - 选择“符号加载信息”以显示调试器搜索符号的位置。

   - 选择“符号设置”以打开“符号”页。 在“符号”页的”符号文件(.pdb)位置”下，选择“Microsoft 符号服务器”以访问公共 Microsoft 符号服务器中的符号。 选择工具栏按钮以添加其他符号位置并更改加载顺序。 选择“确定”关闭对话框。

### <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)