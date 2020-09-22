---
title: 如何：使用“编辑并继续”(C#) | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840564"
---
# <a name="how-to-use-edit-and-continue-c"></a>如何：使用“编辑并继续”(C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 C# 的“编辑并继续”，可以一边进行调试一边在中断模式下更改代码。 不必停止并重新启动调试会话即可应用更改。  
  
 当你在中断模式下进行更改时，将自动调用 "编辑并继续"，然后选择一个调试器执行命令，如 " **继续**"、" **单步**执行" 或 " **设置下一语句**"，或在调试器窗口中计算函数。  
  
> [!NOTE]
> 在调试 Compact Framework、优化代码、本机/托管混合代码或 SQL Server 公共语言运行时 (CLR) 集成代码时不支持“编辑并继续”。 如果尝试在这些情况下应用代码更改，则调试器会出现一个对话框，说明不支持 "编辑并继续"。  
  
### <a name="to-invoke-edit-and-continue-automatically"></a>自动调用 "编辑并继续"  
  
1. 在中断模式下，对源代码进行更改。  
  
2. 从 "**调试**" 菜单中单击 "继续"、"**单步****执行**" 或 "**设置下一语句**" 或 "在调试器窗口中计算函数"。  
  
     将编译新代码，并继续调试新代码。 "编辑并继续" 不支持某些更改。 有关详细信息，请参阅 [c # )  (支持的代码更改 ](../debugger/supported-code-changes-csharp.md)。  
  
### <a name="to-enabledisable-edit-and-continue"></a>启用/禁用“编辑并继续”  
  
1. 在“工具”  菜单上，单击“选项” 。  
  
2. 在 " **选项** " 对话框中，展开 " **调试** " 节点，然后选择 " **编辑并继续**"。  
  
3. 在 " **选项** **" 对话框中** ，选择或清除 " **启用编辑并继续** " 复选框。  
  
     此设置在重新启动调试会话时生效。  
  
## <a name="see-also"></a>另请参阅  
 ["编辑并继续" (Visual c # ) ](../debugger/edit-and-continue-visual-csharp.md)   
 [ (c # ) 支持的代码更改 ](../debugger/supported-code-changes-csharp.md)   
 [“编辑并继续”错误和警告 (C#)](../misc/edit-and-continue-errors-and-warnings-csharp.md)
