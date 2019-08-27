---
title: 解决方案用户选项 (。Suo) 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1a9825fabe08940e8950cf88a1dbf2bc149af0b2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197335"
---
# <a name="solution-user-options-suo-file"></a>解决方案用户选项 (.Suo) 文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

解决方案用户选项 (.suo) 文件包含每个用户解决方案选项。 此文件应不会签入到源代码管理。  
  
 解决方案用户选项 (.suo) 文件是结构化的存储或复合，以二进制格式存储的文件。 正在将用于标识.suo 文件中的信息的键的流的名称与保存到流的用户信息。 解决方案用户选项文件用于存储用户首选项设置，并在 Visual Studio 将保存在一个解决方案时自动创建。  
  
 当环境打开.suo 文件时，它将枚举所有当前加载的 Vspackage。 如果 VSPackage 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>接口，则环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A>上要求它的 VSPackage，.suo 文件中加载其所有数据的方法。  
  
 它是知道什么流式处理它的 VSPackage 的责任可能已写入到.suo 文件。 对于它编写了每个流，VSPackage 回拨到环境中，通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A>加载由键，这是流的名称标识的特定流。 在环境然后回拨到 VSPackage 可以读取该特定流传递的流的名称和一个`IStream`指针，指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A>方法。  
  
 此时，对另一个调用`LoadUserOptions`以查看是否具有要读取的.suo 文件的另一个部分。 此过程持续数据流.suo 文件中的所有已读取并处理由环境。  
  
 在保存或关闭，环境调用解决方案<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A>方法用一个指针指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A>方法。 `IStream`包含要保存的二进制信息传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A>方法，然后将信息写入到的.suo 文件和调用`SaveUserOptions`方法再次以查看是否存在另一个流的信息将写入.suo文件。  
  
 这两种方法`SaveUserOptions`并`WriteUserOptions`，为要保存到.suo 文件，传入指向指针的信息的每个流以递归方式调用`IVsSolutionPersistence`。 调用以递归方式以允许进行多个流的.suo 文件的写入它们。 这样一来，用户信息与解决方案一起持久保留，并保证在这里，在下次打开该解决方案。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>   
 [解决方案](../../extensibility/internals/solutions-overview.md)
