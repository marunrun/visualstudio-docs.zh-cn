---
title: 升级项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- upgrading VSPackages
- upgrading applications, strategies
- VSPackages, upgrade support
ms.assetid: e01cb44a-8105-4cf4-8223-dfae65f8597a
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8e838cb02aa1a620356f96d9e77f1752797ac409
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441237"
---
# <a name="upgrading-projects"></a>升级项目
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

从一个版本更改为项目模型[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]到下一个可能需要项目和解决方案进行升级，以便它们可以运行在较新版本。 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]提供了可用于在您自己的项目中实现升级支持的接口。  
  
## <a name="upgrade-strategies"></a>升级策略  
 若要支持升级，您的项目系统实现必须定义并实施升级策略。 在确定您的策略时，你可以选择以支持并行 (SxS) 备份、 复制备份，或两者。  
  
- SxS 备份意味着一个项目将需要升级到位，请添加合适的文件名称后缀，例如，".old 标记"这些文件复制。  
  
- 复制备份意味着一个项目将项目的所有项都复制到用户提供的备份位置。 然后升级原始项目位置的相关文件。  
  
## <a name="how-upgrade-works"></a>如何升级的工作原理  
 在早期版本中创建解决方案时[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]较新版本，该解决方案文件以确定它是否需要升级的 IDE 检查中打开。 如果升级是必需的**升级向导**引导用户完成升级过程将自动启动。  
  
 当升级需求的解决方案时，它会查询其升级策略每个项目工厂。 该策略确定项目工厂是否支持复制备份或并行备份。 信息发送到**升级向导**，来收集备份所需的信息和向用户提供的适用选项。  
  
### <a name="multi-project-solutions"></a>多项目解决方案  
 如果解决方案包含多个项目和不同的升级策略，例如C++项目仅支持并行备份和 Web 项目，仅支持复制备份，项目工厂必须协商的升级策略。  
  
 该解决方案查询的每个项目工厂<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>。 然后，它调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A>全局项目文件是否需要升级并确定受支持的升级策略。 **升级向导**然后调用。  
  
 用户完成该向导后<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A>在每个项目工厂来执行实际升级上调用。 若要简化备份，IVsProjectUpgradeViaFactory 方法提供<xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>服务记录的升级过程的详细信息。 无法缓存此服务。  
  
 在更新后所有相关的全局文件，可以选择每个项目工厂实例化一个项目。 项目实现必须支持<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A>然后调用方法来升级相关的项目的所有项。  
  
> [!NOTE]
> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A>方法不提供 SVsUpgradeLogger 服务。 此服务可以通过调用来获取<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>。  
  
## <a name="best-practices"></a>最佳做法  
 使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>服务，以检查是否可以编辑它之前, 编辑的文件，并可以将其保存在保存它之前。 这将帮助你的备份和升级实现可处理源代码管理下的项目文件中，文件没有足够的权限，等等。  
  
 使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>备份的所有阶段中，在服务和升级功能可以提供有关升级过程成功与否的信息。  
  
 有关备份和升级项目的详细信息，请参阅注释为 IVsProjectUpgrade vsshell2.idl 中。  
  
## <a name="see-also"></a>请参阅  
 [项目](../../extensibility/internals/projects.md)   
 [升级自定义项目](../../misc/upgrading-custom-projects.md)   
 [升级项目项](../../misc/upgrading-project-items.md)
