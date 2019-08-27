---
title: 如何：使用编辑并继续 (C#) |Microsoft Docs
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
- Edit and Continue [C#], about Edit and Continue
ms.assetid: 40e136d8-a08c-43bd-b313-fb821c55eb3c
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 39137d5fe60a3c91c8fd3904e797eb83420a8f5d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384027"
---
# <a name="how-to-use-edit-and-continue-c"></a>如何：使用“编辑并继续”(C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 C# 的“编辑并继续”，可以一边进行调试一边在中断模式下更改代码。 不必停止并重新启动调试会话即可应用更改。  
  
 编辑并继续自动调用时在中断模式下进行更改，然后选择调试程序执行命令，如**继续**，**步骤**，或**设置下一语句**，或计算在调试器窗口函数。  
  
> [!NOTE]
> 在调试 Compact Framework、优化代码、本机/托管混合代码或 SQL Server 公共语言运行时 (CLR) 集成代码时不支持“编辑并继续”。 如果你尝试应用代码更改在其中一种情形中的，则调试器将显示一个对话框，其中说明编辑并继续不受支持。  
  
### <a name="to-invoke-edit-and-continue-automatically"></a>若要调用编辑并继续自动  
  
1. 在中断模式下对源代码进行更改。  
  
2. 从**调试**菜单上，单击**继续**，**步骤**，或者**设置下一语句**或调试器窗口中计算函数。  
  
     新的代码编译和调试将继续执行新的代码。 编辑并继续不支持某些更改。 有关详细信息，请参阅[支持的代码更改 (C#)](../debugger/supported-code-changes-csharp.md)。  
  
### <a name="to-enabledisable-edit-and-continue"></a>启用/禁用“编辑并继续”  
  
1. 在 **“工具”** 菜单上，单击 **“选项”**。  
  
2. 在中**选项**对话框框中，展开**调试**节点，然后选择**编辑并继续**。  
  
3. 在中**选项**对话框中**编辑并继续**页上，选中或清除**启用编辑并继续**复选框。  
  
     重新启动调试会话时，该设置将生效。  
  
## <a name="see-also"></a>请参阅  
 [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)   
 [受支持的代码更改 (C#)](../debugger/supported-code-changes-csharp.md)   
 [“编辑并继续”错误和警告 (C#)](../misc/edit-and-continue-errors-and-warnings-csharp.md)
