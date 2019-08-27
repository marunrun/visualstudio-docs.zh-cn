---
title: 公开到可视化设计器的类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4d6c0e163b751f1873fdb941e85c273dcc4fde5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691208"
---
# <a name="exposing-types-to-visual-designers"></a>向可视化设计器公开类型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 必须具有访问的类和类型定义在设计时才能显示一个可视化设计器。 从一组预定义的包含完整的依赖项集的当前项目 （引用以及其依赖项） 的程序集加载的类。 可能还会对访问类和自定义工具生成的文件中定义的类型所需的可视化设计器。  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]和[!INCLUDE[csprcs](../../includes/csprcs-md.md)]项目系统提供了支持访问生成的类和类型通过临时可移植可执行文件 (临时 PEs)。 在自定义工具生成的任何文件可以编译到一个临时程序集，以便可以从这些程序集加载和设计器向公开类型。 每个自定义工具的输出编译到单独的临时 PE，并且此临时编译成功与否仅取决于可编译生成的文件。 虽然项目可能无法生成作为一个整体，各个临时 Pe 可能仍是可用于设计器。  
  
 项目系统提供完全支持跟踪以更改到的输出文件的自定义工具，前提是这些更改是正在运行的自定义工具的结果。 每次运行自定义工具时，生成新的临时 PE，并相应通知发送到设计器。  
  
> [!NOTE]
> 因为临时程序可执行文件的生成文件在后台发生，所以在编译失败，向用户未不报告任何错误。  
  
 自定义工具，它们利用临时 PE 支持必须遵循以下规则：  
  
- `GeneratesDesignTimeSource` 必须设置为 1 在注册表中。  
  
     如果没有此设置没有程序可执行文件编译发生。  
  
- 生成的代码必须在全局项目设置相同的语言。  
  
     临时 PE 编译而不考虑自定义工具报告为在请求的扩展<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>前提`GeneratesDesignTimeSource`在注册表中设置为 1。 该扩展不需要为.vb、.cs 或.jsl;它可以是任何扩展。  
  
- 自定义工具生成的代码必须是有效的并且它必须在其自身仅存在于项目中引用的集时使用编译<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>完成执行。  
  
     编译的临时 PE 后，仅提供给编译器的源文件是自定义工具输出。 因此，使用临时 PE 的自定义工具必须生成可以独立于项目中的其他文件编译的输出文件。  
  
## <a name="see-also"></a>请参阅  
 [BuildManager 对象介绍](https://msdn.microsoft.com/50080ec2-c1c9-412c-98ef-18d7f895e7fa)   
 [实现单个文件生成器](../../extensibility/internals/implementing-single-file-generators.md)   
 [确定项目的默认 Namespace](../../misc/determining-the-default-namespace-of-a-project.md)   
 [注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)
