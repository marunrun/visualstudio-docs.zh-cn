---
title: 确定项目的默认命名空间 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- custom tools, computing default namespace
ms.assetid: 6d890676-7016-458c-8a6a-95cc0a068612
caps.latest.revision: 13
manager: jillfra
ms.openlocfilehash: 1d58c8986922c30192d6300a623a635b24c34ed5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65705769"
---
# <a name="determining-the-default-namespace-of-a-project"></a>确定项目的默认命名空间
对于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ，如果在 `CustomToolNamespace` 输入文件上设置了属性，则的值 `CustomToolNamespace` 将成为传递到该方法的默认命名空间参数的值 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> 。 否则， `wszDefaultNamespace` 传递到的参数 `Generate` 始终等于根命名空间。 有关命名空间的详细信息，请参阅 [命名空间关键字](https://msdn.microsoft.com/library/091a66eb-b10d-4f54-9102-5ac0d4bdb84b)。  
  
 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 使用基于文件夹的命名空间。 也就是说，命名空间包含根命名空间，加上包含自定义工具的任何文件夹的名称。 每个文件夹名称将转换为有效的标识符，并将所有名称隔开。 例如，如果输入文件是 FolderA\FolderB\FolderC\MyInput.txt 的，并且根命名空间为 CL9，则计算出的默认命名空间为 **CL9。FolderA. FolderB. FolderC**。  
  
 如果层次结构链包含 Web 引用文件夹，则会出现此规则的例外情况。 例如，如果：  
  
- FolderC 是一个 Web 引用文件夹，命名空间为 **CL9。FolderC**。  
  
- FolderB 是一个 Web 引用文件夹，命名空间为 **CL9。FolderB. FolderC**。  
  
  也就是说，命名空间使用以下格式：  
  
```  
rootNamespace.webReferenceFolder.containedFolder.containedFolder ...  
```  
  
## <a name="see-also"></a>另请参阅  
 [实现单文件生成器](../extensibility/internals/implementing-single-file-generators.md)   
 [注册单个文件生成器](../extensibility/internals/registering-single-file-generators.md)   
 [向可视化设计器公开类型](../extensibility/internals/exposing-types-to-visual-designers.md)