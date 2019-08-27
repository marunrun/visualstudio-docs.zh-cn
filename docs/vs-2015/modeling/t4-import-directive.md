---
title: T4 导入指令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 713ca975-b9aa-4210-bf6d-b7660f5b193b
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 00033640ec7810f97785b38437795906500a7866
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163663"
---
# <a name="t4-import-directive"></a>T4 导入指令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] T4 文本模板的代码块中，`import` 指令允许你在不提供完全限定名称的情况下引用另一个命名空间中的元素。 它等效于 C# 中的 `using` 或 `imports` 中的 [!INCLUDE[vb_current_short](../includes/vb-current-short-md.md)]。  
  
 有关编写 T4 文本模板的一般概述，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。  
  
## <a name="using-the-import-directive"></a>使用 Import 指令  
  
```  
<#@ import namespace="namespace" #>  
```  
  
 在此示例中，模板代码可为 System.IO 的成员省略显式命名空间：  
  
```  
<#@ import namespace="System.IO" #>  
<#   
   string fileContent = File.ReadAllText("C:\x.txt"); // System.IO.File  
#>   
The file contains: <#=  fileContent #>  
```  
  
## <a name="standard-imports"></a>标准导入  
 将自动导入以下命名空间，您无需为其编写导入指令：  
  
- `System`  
  
  另外，如果您使用自定义指令，则指令处理器可能会自动导入一些命名空间。  
  
  例如，如果您为域特定语言 (DSL) 编写模板，则无需为下列命名空间编写导入指令：  
  
- `Microsoft.VisualStudio.Modeling`  
  
- DSL 的命名空间  
  
## <a name="see-also"></a>请参阅  
 [T4 程序集指令](../modeling/t4-assembly-directive.md)
