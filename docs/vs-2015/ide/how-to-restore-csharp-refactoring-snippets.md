---
title: 如何：还原 C# 重构代码片段 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- unsafe expansion
- expansions, unsafe
ms.assetid: 12114273-7f2f-43d0-abcb-2d4711a3a68d
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9f81514db881ad26a5fa827b0bde11df2467f23d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186280"
---
# <a name="how-to-restore-c-refactoring-snippets"></a>如何：还原 C# 重构代码段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C# 重构操作依赖于在以下目录中找到的代码片段：  
  
 *安装目录*\Microsoft Visual Studio 14.0\VC#\Snippets\\*language ID*\Refactoring  
  
 如果删除或损坏了此重构目录或此目录中的任何文件，那么 C# 重构操作可能不会在 IDE 中起作用。 以下过程可帮助还原 C# 重构代码片段。  
  
### <a name="to-verify-c-refactoring-snippets-are-available-through-the-code-snippet-manager"></a>若要通过代码片段管理器验证 C# 重构代码片段是否可用  
  
1. 在“工具”  菜单中，选择“代码片段管理器”  。  
  
2. 在“代码片段管理器”  对话框中，从“语言”  下拉列表中选择“Visual C#”  。  
  
     “重构”  文件夹应出现在树视图文件夹列表中。  
  
### <a name="to-restore-refactoring-see-comment-in-code-snippet-manager"></a>若要还原重构，请参阅“代码片段管理器”中的注释  
  
1. 若“重构”  文件夹未出现在“代码片段管理器”的树视图文件夹列表中，则使用此过程将重构代码片段添加回“代码片段管理器”中。  
  
2. 在“工具”  菜单中，选择“代码片段管理器”  。  
  
3. 在“代码片段管理器”  对话框中，从“语言”  下拉列表中选择“Visual C#”  。  
  
4. 单击 **添加**。 将出现“代码片段目录”  对话框，该对话框可帮助查找和指定要添加回“代码片段管理器”的目录。  
  
5. 查找“重构”  文件夹，其目录路径为：  
  
     *安装目录*\Microsoft Visual Studio 14.0\VC#\Snippets\\*language ID*\Refactoring  
  
     实际路径类似于以下默认安装的路径：  
  
     C:\Program Files\Microsoft Visual Studio 14.0\VC#\Snippets\1033\Refactoring。  
  
6. 单击“代码片段目录”  对话框中的“打开”  ，然后在“代码片段管理器”中单击“确定”  。  
  
## <a name="see-also"></a>另请参阅  
 [Visual C# 代码片段](../ide/visual-csharp-code-snippets.md)   
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)   
 [代码片段](../ide/code-snippets.md)
