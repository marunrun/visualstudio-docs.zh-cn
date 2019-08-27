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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432079"
---
# <a name="solutions-overview"></a>解决方案概述
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

一种解决方案是协同工作以创建应用程序的一个或多个项目的分组。 与解决方案有关的项目和状态信息存储在两个不同的解决方案文件。 解决方案 (.sln) 文件是基于文本的并可放置在源代码管理下和用户之间共享。 解决方案用户选项 (.suo) 文件是二进制文件。 因此，.suo 文件不能放置在源代码管理下，包含特定于用户的信息。  
  
 任何 VSPackage 可以写入任一类型的解决方案文件。 由于这些文件的性质，有两个不同的接口实现来写入它们。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>接口将文本信息写入到.sln 文件和<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>接口向.suo 文件中写入二进制流。  
  
> [!NOTE]
> 项目不具有显式将一个条目为自身写入解决方案文件中;环境处理的项目。 因此，除非你想要将更多的内容添加到解决方案文件具体而言，您不必以这种方式注册你的 VSPackage。  
  
 每个 VSPackage 支持解决方案持久性使用三个接口，<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>接口，这是由环境实现，并且调用由 VSPackage，并且`IVsPersistSolutionProps`和`IVsPersistSolutionOpts`，它们是由 VSPackage 同时实现。 `IVsPersistSolutionOpts`接口仅需要如果私人信息将写入.suo 文件的 VSPackage 的实现。  
  
 如果打开解决方案时，以下过程将会发生。  
  
1. 在环境中读取该解决方案。  
  
2. 如果找到了环境`CLSID`，它将加载相应的 VSPackage。  
  
3. 如果加载 VSPackage，环境调用`QueryInterface`为<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>接口，VSPackage 需要的接口。  
  
   1. 当从.sln 文件读取，环境在调用`QueryInterface`为`IVsPersistSolutionProps`。  
  
   2. 当从.suo 文件读取，环境在调用`QueryInterface`为`IVsPersistSolutionOpts`。  
  
   使用这些文件与相关的特定信息可在[解决方案 (。Sln) 文件](../../extensibility/internals/solution-dot-sln-file.md)和[解决方案用户选项 (。Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。  
  
> [!NOTE]
> 如果你想要创建新的解决方案配置包含两个项目配置和从生成中排除第三，您需要使用属性页用户界面或自动化。 不能直接更改解决方案的生成管理器配置和其属性，但可以操作解决方案生成管理器使用`SolutionBuild`从 DTE 自动化模型中的类。 有关配置解决方案的详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
