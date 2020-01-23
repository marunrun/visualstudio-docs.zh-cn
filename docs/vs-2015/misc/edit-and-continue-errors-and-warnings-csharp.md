---
title: "\"编辑并继续\" 错误和C#警告（） |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
f1_keywords:
- vs.csharp.enc.error_4001
- vs.csharp.enc.error_4034
- vs.csharp.enc.error_4003
- vs.csharp.enc.error_4026
- vs.csharp.enc.error_4032
- vs.csharp.enc.error_4017
- vs.csharp.enc.error_4053
- vs.csharp.enc.error_4024
- vs.csharp.enc.error_4012
- vs.csharp.enc.error_4066
- vs.csharp.enc.error_4020
- vs.csharp.enc.error_4008
- vs.csharp.enc.error_4033
- vs.csharp.enc.error_4014
- vs.csharp.enc.error_4023
- vs.csharp.enc.error_4011
- vs.csharp.enc.error_4006
- vs.csharp.enc.error_4059
- vs.csharp.enc.error_4015
- vs.csharp.enc.error_4018
- vs.csharp.enc.error_4028
- vs.csharp.enc.error_4013
- vs.csharp.enc.error_4009
- vs.csharp.enc.error_4021
- vs.csharp.enc.error_4065
- vs.csharp.enc.error_4029
- vs.csharp.enc.error_4058
- vs.csharp.enc.error_4019
- vs.csharp.enc.error_4007
- vs.csharp.enc.error_4052
- vs.csharp.enc.error_4025
- vs.csharp.enc.error_4055
- vs.csharp.enc.error_4022
- vs.csharp.enc.error_4002
- vs.csharp.enc.error_4016
- vs.csharp.enc.error_4043
- vs.csharp.enc.error_4027
- vs.csharp.enc.error_4054
- vs.csharp.enc.error_4004
- vs.csharp.enc.error_4010
- vs.csharp.enc.error_4030
- vs.csharp.enc.error_4005
- vs.csharp.enc.error_4035
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], errors and warnings
- errors [C#], debugging
- errors [debugger], Edit and Continue
ms.assetid: c0e12b0a-8009-4a4a-979f-c804a91a5d9b
caps.latest.revision: 11
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eec40bc584e831f8b43b79c9bc7cee5a48a291aa
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850977"
---
# <a name="edit-and-continue-errors-and-warnings-c"></a>“编辑并继续”错误和警告 (C#)
已对 Visual C#“编译并继续”中不允许的代码段进行了编辑。  
  
 利用 [!INCLUDE[csharp_current_short](../includes/csharp-current-short-md.md)]“编辑并继续”，您可以在中断模式下停止程序执行，对执行代码进行更改，然后继续执行新合并了更改后的程序。  
  
 通常情况下，影响类的公共结构的声明性代码编辑是禁止的，但对类内部的方法、属性体或私有声明进行某些编辑是允许的。 “编辑并继续”会尽可能将不可编辑的代码标记为浅灰色并显示错误消息。  
  
 有关 [!INCLUDE[csharp_current_short](../includes/csharp-current-short-md.md)]的 "编辑并继续" 中支持的编辑的详细信息，请参阅[支持的代码更改（C#）](../debugger/supported-code-changes-csharp.md)。 如果需要有关特定错误或警告的详细信息，可以在 MSDN [Visual C# IDE 论坛](https://social.msdn.microsoft.com/Forums/en-US/csharpide/threads)上搜索或发布。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
1. 在 **“调试”** 菜单上，选择 **“撤消”** 可撤消更改。  
  
     或  
  
2. 停止调试会话，进行编辑并启动新的调试会话。  
  
## <a name="see-also"></a>请参阅  
 [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
