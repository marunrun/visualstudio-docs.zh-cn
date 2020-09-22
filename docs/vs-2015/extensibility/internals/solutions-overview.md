---
title: 解决方案概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb3bb85ab172404262c147cce285cebaf756afc9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840776"
---
# <a name="solutions-overview"></a>解决方案概述
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

解决方案是一个或多个项目的分组，它们一起工作以创建应用程序。 与解决方案有关的项目和状态信息存储在两个不同的解决方案文件中。 解决方案 ( .sln) 文件是基于文本的，可置于源代码控制下并在用户之间共享。 解决方案用户选项 ( .suo) 文件是二进制文件。 因此，不能将 .suo 文件置于源代码管理下，而是包含用户特定的信息。  
  
 任何 VSPackage 都可以写入任一类型的解决方案文件。 由于文件的性质，实现了两个不同的接口来写入它们。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>接口将文本信息写入 .sln 文件，并且 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 接口会将二进制流写入 .suo 文件中。  
  
> [!NOTE]
> 项目无需显式地将条目写入解决方案文件;环境将处理该项目的。 因此，除非您想要专门添加特定于解决方案文件的其他内容，否则不需要以这种方式注册您的 VSPackage。  
  
 每个支持解决方案持久性的 VSPackage 都使用三个接口， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 接口由环境实现并由 VSPackage、和 `IVsPersistSolutionProps` `IVsPersistSolutionOpts` （均由 VSPackage 实现）调用。 `IVsPersistSolutionOpts`仅当 VSPackage 向 .suo 文件写入私有信息时，才需要实现接口。  
  
 打开解决方案时，将发生以下过程。  
  
1. 环境将读取解决方案。  
  
2. 如果环境找到 `CLSID` ，则会加载相应的 VSPackage。  
  
3. 如果加载了 VSPackage，则环境将 `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 为 VSPackage 所需的接口调用 interface。  
  
   1. 从 .sln 文件读取时，环境将调用 `QueryInterface` `IVsPersistSolutionProps` 。  
  
   2. 从 .suo 文件中读取时，环境会调用 `QueryInterface` `IVsPersistSolutionOpts` 。  
  
   解决方案 ( 中可以找到与这些文件的使用相关的特定信息 [。.Sln) 文件](../../extensibility/internals/solution-dot-sln-file.md) 和 [解决方案用户选项 (。.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。  
  
> [!NOTE]
> 如果要创建包含两个项目的配置的新解决方案配置，并从生成中排除第三个，则需要使用属性页 UI 或自动化。 不能直接更改解决方案生成管理器的配置和属性，但可以使用 `SolutionBuild` 自动化模型中的 DTE 类操作解决方案生成管理器。 有关配置解决方案的详细信息，请参阅 [解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
