---
title: 确定项目的默认 Namespace |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705769"
---
# <a name="determining-the-default-namespace-of-a-project"></a>确定项目的默认命名空间
有关[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，如果`CustomToolNamespace`输入文件，然后的值上设置属性`CustomToolNamespace`成为传递给的默认命名空间参数的值<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>方法。 否则为`wszDefaultNamespace`参数传递给`Generate`也始终等于根命名空间。 命名空间的详细信息，请参阅[Namespace 关键字](https://msdn.microsoft.com/library/091a66eb-b10d-4f54-9102-5ac0d4bdb84b)。  
  
 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 使用基于文件夹的命名空间。 也就是说，该命名空间由根命名空间和包含自定义工具的任何文件夹的名称组成。 每个文件夹名称转换为有效的标识符，并且所有名称用逗号都分开。 例如，如果输入的文件为 FolderA\FolderB\FolderC\MyInput.txt，并且根命名空间为 CL9，则计算的默认命名空间应**CL9。FolderA.FolderB.FolderC**。  
  
 此规则的例外发生时的层次结构链包含 Web 引用文件夹。 例如，如果：  
  
- FolderC Web 引用文件夹，命名空间为**CL9。FolderC**。  
  
- FolderB Web 引用文件夹，命名空间为**CL9。FolderB.FolderC**。  
  
  也就是说，该命名空间使用的格式如下：  
  
```  
rootNamespace.webReferenceFolder.containedFolder.containedFolder ...  
```  
  
## <a name="see-also"></a>请参阅  
 [实现单个文件生成器](../extensibility/internals/implementing-single-file-generators.md)   
 [注册单个文件生成器](../extensibility/internals/registering-single-file-generators.md)   
 [向可视化设计器公开类型](../extensibility/internals/exposing-types-to-visual-designers.md)