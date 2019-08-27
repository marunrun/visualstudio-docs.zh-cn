---
title: 如何：调试.NET Framework 源代码 |Microsoft Docs
ms.date: 11/19/2018
ms.topic: conceptual
helpviewer_keywords:
- debugging, .NET Framework source
ms.assetid: fc12e472-ac6a-4e77-8e22-a769e13a03b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 25f40b0528b794863aabdb13ed9785d2b0c551b8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894269"
---
# <a name="how-to-debug-net-framework-source"></a>如何：调试 .NET Framework 源代码

若要调试.NET Framework 源代码，您必须：

- 启用执行.NET Framework 源代码单步执行。

- 有权访问的调试符号的代码。

  您可以选择下载调试符号立即，或设置选项，以后再下载。 如果不立即下载符号，它们将下载的下次开始调试您的应用程序。 调试时，还可以使用**模块**或**调用堆栈**windows 下载并加载符号。

### <a name="to-enable-stepping-into-net-framework-source"></a>若要启用到.NET Framework 源单步执行

1. 下**工具**(或**调试**) >**选项** > **调试** > **常规**，选择**启用.NET Framework 源代码单步执行**。

   - 如果您先前启用了“仅我的代码”，则会出现一个警告对话框，提示您“仅我的代码”现在已禁用。 选择 **确定**。

   - 如果您没有设置的本地符号缓存，警告对话框将提示您默认符号缓存已设置。 选择 **确定**。

1. 选择**确定**以关闭**选项**对话框。

### <a name="to-set-or-change-symbol-source-locations-and-loading-behavior"></a>若要设置或更改符号源位置和加载行为

1. 选择**符号**类别下的**工具**(或**调试**) >**选项** > **调试**.

1. 上**符号**页面上，在**符号文件 (.pdb) 位置**，选择**Microsoft 符号服务器**从公共 Microsoft 符号服务器访问符号。 选择要添加其他符号位置和更改加载顺序的工具栏按钮。

1. 若要更改你的本地符号缓存，可以编辑或浏览到其他位置下**在此目录下缓存符号**。

1. 若要立即下载符号，请选择**加载所有符号**。 只有在调试时，此按钮才可用。

   如果不立即下载符号，它们将在下一步时下载开始调试。

1. 选择**确定**以关闭**选项**对话框。

### <a name="to-load-symbols-from-the-modules-or-call-stack-windows"></a>若要加载的符号从模块或调用堆栈窗口

1. 在调试期间，打开选择窗口**调试** > **Windows** > **模块**(或按**Ctrl + Alt + U**)或**调试** > **Windows** > **调用堆栈**(**Ctrl + Alt + C**)。

1. 右键单击的模块未加载符号。 在中**模块**窗口中，符号加载状态处于**符号状态**列。 在中**调用堆栈**窗口中，状态不**帧状态**列，并在帧是灰显。

   - 选择**加载符号**菜单来查找并加载符号文件从你的计算机上的文件夹中。

   - 选择**符号加载信息**显示调试器搜索符号的位置。

   - 选择**符号设置**以打开**符号**页。 上**符号**页面上，在**符号文件 (.pdb) 位置**，选择**Microsoft 符号服务器**从公共 Microsoft 符号服务器访问符号。 选择要添加其他符号位置和更改加载顺序的工具栏按钮。 选择**确定**关闭对话框。

### <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)