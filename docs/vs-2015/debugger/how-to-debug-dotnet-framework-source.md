---
title: 如何：调试.NET Framework 源代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, .NET Framework source
ms.assetid: fc12e472-ac6a-4e77-8e22-a769e13a03b8
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 49b13b8406dc96e8e7ebe5e79e26c5da02e8a53a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205445"
---
# <a name="how-to-debug-net-framework-source"></a>如何：调试 .NET Framework 源
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

最新版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]提供的新功能[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]调试。 若要调试[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]源，您必须有权调试符号的代码。 此外需要启用单步执行[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]源。  
  
 可以让[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]单步执行和符号中下载**选项**对话框。 启用符号下载功能时，可以选择立即下载符号，也可以仅启用该选项，以后再下载。 如果不立即下载符号，这些符号将在下次您开始调试应用程序时下载。 您还可以执行从手动下载**模块**窗口或**调用堆栈**窗口。  
  
### <a name="to-enable-net-framework-source-debugging"></a>启用 .NET Framework 源代码调试  
  
1. 在 **“工具”** 菜单上，单击 **“选项”** 。  
  
2. 在中**选项**对话框中，单击**调试**类别。  
  
3. 在中**常规**框中，设置**启用.NET Framework**源代码单步执行。  
  
    1. 如果您先前启用了“仅我的代码”，则会出现一个警告对话框，提示您“仅我的代码”现在已禁用。 单击 **“确定”** 。  
  
    2. 如果您没有设置符号缓存位置，则会出现另一个警告对话框，提示您默认符号缓存位置现在已设置。 单击 **“确定”** 。  
  
4. 下**调试**类别中，单击**符号**。  
  
5. 若要更改符号缓存位置，请执行以下操作：  
  
    1. 打开**调试**左侧框中的节点。  
  
    2. 下**调试**节点中，单击**符号**。  
  
    3. 编辑中的位置**符号从符号服务器缓存到此目录**或单击**浏览**选择一个位置。  
  
6. 如果你想要立即下载符号，请单击**使用上面的位置加载符号**。  
  
     此按钮在设计模式下不可用。  
  
     如果选择不立即下载符号，则这些符号将在您下次开始调试程序时自动下载。  
  
7. 单击“确定”关闭“选项”对话框   。  
  
### <a name="to-load-framework-symbols-using-the-modules-window"></a>使用“模块”窗口加载 Framework 符号  
  
1. 在中**模块**窗口中，右击还未加载符号的模块的。 如果已加载符号或不是通过在查看可以告诉**符号状态**列。  
  
2. 指向**符号加载从**然后单击**Microsoft 符号服务器**若要从 Microsoft 公共符号服务器下载符号或**符号路径**从一个目录中加载以前存储的符号。  
  
### <a name="to-load-framework-symbols-using-the-call-stack-window"></a>使用“调用堆栈”窗口加载 Framework 符号  
  
1. 在中**调用堆栈**窗口中，右击还未加载符号的帧的。 此帧将显示为灰色。  
  
2. 指向**负载从符号**然后单击**Microsoft 符号服务器**或**符号路径**。  
  
## <a name="see-also"></a>请参阅  
 [调试托管代码](../debugger/debugging-managed-code.md)   
 [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
