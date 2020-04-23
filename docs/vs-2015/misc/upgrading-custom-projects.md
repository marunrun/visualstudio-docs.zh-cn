---
title: 升级自定义项目 |微软文档
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- upgrading project systems
- projects [Visual Studio SDK], upgrading
- project system upgrades [Visual Studio]
ms.assetid: 262ada44-7689-44d8-bacb-9c6d33834d4e
caps.latest.revision: 11
manager: jillfra
ms.openlocfilehash: c91013e7d5650e82fd9e5f6e39e28c4609e4fbfe
ms.sourcegitcommit: c1339f64fbeee6f17bf80fedea81afc8dac40dc0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "82037202"
---
# <a name="upgrading-custom-projects"></a>升级自定义项目
如果你更改保留在产品的不同 Visual Studio 版本之间的项目文件中的信息，则你需要支持将项目文件从旧版本升级到新版本。 要支持升级，允许您参与**可视化工作室转换向导**，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>该接口。 此接口包含可用于复制升级的唯一机制。 项目的升级作为解决方案打开的一部分而发生。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口由项目工厂实现或至少应从项目工厂获得。  
  
 仍支持使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 接口的旧机制，但该机制将会把项目系统作为项目打开的一部分进行概念上的升级。 因此即使调用或实现了 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口，<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 接口仍由 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 环境调用。 此方法允许你使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 来实现复制、仅规划升级的部分并通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 接口委派要就地（可能在新位置）完成的剩余工作。  
  
 有关 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>实现示例，请参阅[VSSDK 示例](../misc/vssdk-samples.md)。  
  
 项目升级时出现下列情况：  
  
- 如果文件是项目不能支持的较新格式，则它必须返回一个指出此情况的错误。 这假定你产品的较旧版本（例如，Visual Studio .NET 2003）包含检查版本的代码。  
  
- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法中指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> 标志 ，则升级将在打开项目前作为就地升级而实现。  
  
- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法中指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> 标志，则升级将作为复制升级而实现。  
  
- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 调用中指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> 标志，则在项目打开后环境会提示用户以就地升级的方式对项目文件进行升级。 例如，当用户打开解决方案的较旧版本时，环境会提示用户升级。  
  
- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 调用中未指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> 标志，则必须提示用户升级项目文件。  
  
     下面是一个升级提示消息示例：  
  
     “项目“%1”由 Visual Studio 的较旧版本创建。 如果使用此版本的 Visual Studio 打开它，你将不能用较旧版本的 Visual Studio 打开它。 是否要继续并打开此项目？”  
  
### <a name="to-implement-ivsprojectupgradeviafactory"></a>实现 IVsProjectUpgradeViaFactory  
  
1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口的方法，特别是项目工厂实现中的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法，或使该实现可从项目工厂实现中调用。  
  
2. 如果你想要将就地升级作为解决方案打开的一部分而进行，则在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 实现中提供 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> 标志作为 `VSPUVF_FLAGS` 参数。  
  
3. 如果你想要将就地升级作为解决方案打开的一部分而进行，则在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 实现中提供 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> 标志作为 `VSPUVF_FLAGS` 参数。  
  
4. 对于步骤 2 和步骤 3 而言，实际文件升级步骤（使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>）可按以下“实现 `IVsProjectUpgade`”部分中所述进行实现，或可将实际文件升级委派到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>。  
  
5. 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> 的方法来为使用 Visual Studio 迁移向导的用户发布升级相关消息。  
  
6. <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileUpgrade> 接口用于实现需作为项目升级一部分而发生的任何类型的文件升级。 此接口不从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 调用，但会将其作为一种机制用来对属于项目系统、但主项目系统可能不会直接感知到的文件进行升级。 例如，如果编译器相关文件和属性未由处理项目系统其余部分的同一开发团队处理，则可能会发生这种情况。  
  
## <a name="ivsprojectupgrade-implementation"></a>IVsProjectUpgrade 实现  
 如果项目系统仅实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>，则无法参与**可视化工作室转换向导**。 但即使你实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口，仍可将文件升级委派到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 实现。  
  
#### <a name="to-implement-ivsprojectupgrade"></a>实现 IVsProjectUpgrade  
  
1. 用户尝试打开一个项目时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 方法将由环境在项目打开后、在项目上执行任何其他用户操作前调用。 如果已提示用户升级解决方案，则 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> 标志将传入 `grfUpgradeFlags` 参数。 如果用户直接打开项目（例如使用 **"添加现有项目"** 命令），则不会传递<xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS>标志，并且项目需要提示用户升级。  
  
2. 在响应 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 调用时，该项目必须评估是否升级该项目文件。 如果项目不需要将项目类型升级到新版本，则可以只返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 标志。  
  
3. 如果项目需要将项目类型升级到新版本，则它必须确定是否通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 方法和为 `rgfQueryEdit` 参数传入 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> 值来修改项目文件。 该项目接下来需要执行以下操作：  
  
   - 如果 `pfEditCanceled` 参数中返回的 `VSQueryEditResult` 值是 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult>，则升级可以继续，因为项目文件可以进行编写。  
  
   - 如果 `pfEditCanceled` 参数中返回的 `VSQueryEditResult` 值是 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> 且 `VSQueryEditResult` 值设置了 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> 位，则 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 必须返回失败，因为用户应该自己解决权限问题。 该项目接下来应执行以下操作：  
  
        通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 将错误报告给用户。 并将 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> 错误代码返回给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>。  
  
   - 如果 `VSQueryEditResult` 值是 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> 且 `VSQueryEditResultFlags` 值设置了 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> 位，则应通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>（<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>、...）签出项目文件。  
  
4. 如果项目文件上的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 调用导致文件被签出、最新版本被检索，则卸载并重新加载项目。 一旦创建了项目的另一个实例，将会再次调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 方法。 在这第二次调用上，项目文件可以写入磁盘；建议项目使用 .OLD 扩展名按以前的格式保存项目文件的副本、进行必要的升级更改，并以新格式保存项目文件。 同样，如果升级过程的任何部分失败，该方法必须通过返回 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> 指示失败。 这将导致项目无法在解决方案资源管理器中卸载。  
  
    务必了解在环境中发生的整个过程，以应对调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 方法（指定 ReportOnly 的值）将返回 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> 和 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> 标志的情况。  
  
5. 用户尝试打开项目文件。  
  
6. 环境调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> 实现。  
  
7. 如果 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> 返回 `true`，则环境将调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> 实现。  
  
8. 环境调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> 实现，以打开该文件并初始化项目对象，如 Project1。  
  
9. 环境调用你的 `IVsProjectUpgrade::UpgradeProject` 实现来确定是否需要升级项目文件。  
  
10. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 并为 `rgfQueryEdit` 参数传入 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> 值。  
  
11. 环境将为 `VSQueryEditResult` 返回 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> 且将在 `VSQueryEditResultFlags` 中设置 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> 位。  
  
12. 你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 实现调用 `IVsQueryEditQuerySave::QueryEditFiles`（<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>）。  
  
    此调用可能导致项目文件的新副本被签出、最新版本被检索，以及需要重新加载项目文件。 在这种情况下，将发生以下两种情况中的一种：  
  
- 如果你处理自己的项目重载，则环境将调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> (VSITEMID_ROOT) 实现。 当你收到此调用时，请重新加载项目的第一个实例 (Project1) 并继续升级项目文件。 如果你为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) 返回 `true`，则环境知道你将处理自己的项目重载。  
  
- 如果你不处理自己的项目重载，则需为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) 返回 `false`。 在这种情况下，在返回<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>[（QEF_ForceEdit_NoPrompting，QEF_DisallowInMemoryEdits](/dotnet/api/microsoft.visualstudio.shell.interop.tagvsqueryeditflags)）之前，环境将创建另一个新的项目实例，例如 Project2，如下所示： [QEF_DisallowInMemoryEdits](/dotnet/api/microsoft.visualstudio.shell.interop.tagvsqueryeditflags)  
  
  1. 环境在你的第一个项目对象 Project1 上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.Close%2A>，因此使此对象处于非活动状态。  
  
  2. 环境调用你的 `IVsProjectFactory::CreateProject` 实现来创建项目的第二个实例 Project2。  
  
  3. 环境调用你的 `IPersistFileFormat::Load` 实现，以打开该文件并初始化第二个项目对象 Project2。  
  
  4. 环境第二次调用 `IVsProjectUpgrade::UpgradeProject` 以确定是否应升级项目对象。 但是，此调用在项目的第二个新实例 Project2 上进行。 这就是在解决方案中打开的项目。  
  
      > [!NOTE]
      > 如果第一个项目实例 Project1 处于非活动状态，则你必须从对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 实现的首次调用中返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。 有关 的`IVsProjectUpgrade::UpgradeProject`实现，请参阅[基本项目](https://msdn.microsoft.com/385fd2a3-d9f1-4808-87c2-a3f05a91fc36)。  
  
  5. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 并为 `rgfQueryEdit` 参数传入 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> 值。  
  
  6. 环境将返回 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> 且升级可以继续，因为项目文件可以进行编写。  
  
  如果不能升级，请从 `IVsProjectUpgrade::UpgradeProject` 返回 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes>。 如果不需要升级或你选择不升级，请将 `IVsProjectUpgrade::UpgradeProject` 调用视作不执行任何操作。 如果返回 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes>，则向项目的解决方案添加占位符节点。  
  
## <a name="see-also"></a>另请参阅  
 [可视化工作室转换向导](https://msdn.microsoft.com/4acfd30e-c192-4184-a86f-2da5e4c3d83c)   
 [升级项目项](../misc/upgrading-project-items.md)   
 [项目](../extensibility/internals/projects.md)