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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840394"
---
# <a name="upgrading-projects"></a>升级项目
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将项目模型从的一个版本更改 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 为下一个版本可能要求升级项目和解决方案，以便它们能够在较新的版本上运行。 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]提供可用于在你自己的项目中实现升级支持的接口。  
  
## <a name="upgrade-strategies"></a>升级策略  
 若要支持升级，你的项目系统实现必须定义并实现升级策略。 在确定策略时，可以选择同时支持并行 (SxS) 备份和/或副本备份。  
  
- SxS 备份表示项目仅复制那些需要就地升级的文件，并添加适当的文件名后缀，例如 ".old"。  
  
- 复制备份是指项目将所有项目项复制到用户提供的备份位置。 然后升级原始项目位置的相关文件。  
  
## <a name="how-upgrade-works"></a>升级的工作方式  
 在的早期版本中创建的解决方案 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 在较新版本中打开时，IDE 将检查解决方案文件以确定它是否需要升级。 如果需要升级， **升级向导** 会自动启动，以引导用户完成升级过程。  
  
 当解决方案需要升级时，它会查询每个项目工厂的升级策略。 策略确定项目工厂是否支持复制备份或 SxS 备份。 该信息将发送到 **升级向导**，后者收集备份所需的信息，并向用户提供相应的选项。  
  
### <a name="multi-project-solutions"></a>多项目解决方案  
 如果解决方案包含多个项目，并且升级策略不同，例如，仅支持 SxS 备份的 c + + 项目和仅支持复制备份的 Web 项目，则项目工厂必须协商升级策略。  
  
 解决方案将查询每个项目工厂 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 。 然后，它调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A> 以查看全局项目文件是否需要升级，并确定支持的升级策略。 然后，将调用 **升级向导** 。  
  
 用户完成向导后， <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 将在每个项目工厂上调用以执行实际升级。 为了便于备份，IVsProjectUpgradeViaFactory 方法提供 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> 服务来记录升级过程的详细信息。 无法缓存此服务。  
  
 更新所有相关的全局文件后，每个项目工厂都可以选择实例化项目。 项目实现必须支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A>然后调用方法来升级所有相关的项目项。  
  
> [!NOTE]
> 该 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法不提供 SVsUpgradeLogger 服务。 可以通过调用来获取此服务 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 。  
  
## <a name="best-practices"></a>最佳实践  
 使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> 服务检查是否可以在编辑文件之前对其进行编辑，并在保存之前保存文件。 这将帮助你的备份和升级实现处理源代码管理下的项目文件、权限不足的文件等。  
  
 在 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> 备份和升级过程中使用服务，提供有关升级过程是成功还是失败的信息。  
  
 有关备份和升级项目的详细信息，请参阅 vsshell2 中的 IVsProjectUpgrade 的注释。  
  
## <a name="see-also"></a>另请参阅  
 [投射](../../extensibility/internals/projects.md)   
 [升级自定义项目](../../misc/upgrading-custom-projects.md)   
 [升级项目项](../../misc/upgrading-project-items.md)
