---
title: 升级项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- upgrading VSPackages
- upgrading applications, strategies
- VSPackages, upgrade support
ms.assetid: e01cb44a-8105-4cf4-8223-dfae65f8597a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9170532746dfc61cdec6636fb669676a94535de1
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848771"
---
# <a name="upgrading-projects"></a>升级项目

从 Visual Studio 的一个版本到下一版本的项目模型的更改可能要求升级项目和解决方案，以便它们能够在较新的版本上运行。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 提供了可用于在自己的项目中实现升级支持的接口。

## <a name="upgrade-strategies"></a>升级策略

若要支持升级，你的项目系统实现必须定义并实现升级策略。 在确定策略时，可以选择同时支持并行（SxS）备份和/或副本备份。

- SxS 备份表示项目仅复制那些需要就地升级的文件，并添加适当的文件名后缀，例如 ".old"。

- 复制备份是指项目将所有项目项复制到用户提供的备份位置。 然后升级原始项目位置的相关文件。

## <a name="how-upgrade-works"></a>升级的工作方式

在较新版本中打开在 Visual Studio 早期版本中创建的解决方案时，IDE 将检查解决方案文件以确定它是否需要升级。 如果需要升级，**升级向导**会自动启动，以引导用户完成升级过程。

当解决方案需要升级时，它会查询每个项目工厂的升级策略。 策略确定项目工厂是否支持复制备份或 SxS 备份。 该信息将发送到**升级向导**，后者收集备份所需的信息，并向用户提供相应的选项。

### <a name="multi-project-solutions"></a>多项目解决方案

如果解决方案包含多个项目，并且升级策略不同，例如，仅支持C++ SxS 备份的项目和仅支持复制备份的 Web 项目，则项目工厂必须协商升级策略。

解决方案会在每个项目工厂中查询 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>。 然后，它调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A> 来查看全局项目文件是否需要升级，并确定支持的升级策略。 然后，将调用**升级向导**。

用户完成向导后，会在每个项目工厂上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 以执行实际升级。 为了便于备份，IVsProjectUpgradeViaFactory 方法提供 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> 服务来记录升级过程的详细信息。 无法缓存此服务。

更新所有相关的全局文件后，每个项目工厂都可以选择实例化项目。 项目实现必须支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>。 然后调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 方法来升级所有相关的项目项。

> [!NOTE]
> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法不提供 SVsUpgradeLogger 服务。 可以通过调用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>获取此服务。

## <a name="best-practices"></a>最佳做法

使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> 服务检查是否可以在编辑文件之前对其进行编辑，并在保存之前保存文件。 这将帮助你的备份和升级实现处理源代码管理下的项目文件、权限不足的文件等。

在备份和升级的所有阶段使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> 服务，以提供有关升级过程是成功还是失败的信息。

有关备份和升级项目的详细信息，请参阅 vsshell2 中的 IVsProjectUpgrade 的注释。

## <a name="upgrading-custom-projects"></a>升级自定义项目

如果你更改保留在产品的不同 Visual Studio 版本之间的项目文件中的信息，则你需要支持将项目文件从旧版本升级到新版本。 若要支持允许你参与**Visual Studio 转换向导**的升级，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口。 此接口包含可用于复制升级的唯一机制。 项目的升级作为解决方案打开的一部分而发生。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口由项目工厂实现或至少应从项目工厂获得。

仍支持使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 接口的旧机制，但该机制将会把项目系统作为项目打开的一部分进行概念上的升级。 因此，即使调用或实现了 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口，Visual Studio 环境也会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 接口。 此方法允许你使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 来实现复制、仅规划升级的部分并通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 接口委派要就地（可能在新位置）完成的剩余工作。

有关 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>的示例实现，请参阅[VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

项目升级时出现下列情况：

- 如果文件是项目不能支持的较新格式，则它必须返回一个指出此情况的错误。 这假定你产品的较旧版本包含用于检查版本的代码。

- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法中指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> 标志 ，则升级将在打开项目前作为就地升级而实现。

- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法中指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_COPYBACKUP> 标志，则升级将作为复制升级而实现。

- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 调用中指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> 标志，则在项目打开后环境会提示用户以就地升级的方式对项目文件进行升级。 例如，当用户打开解决方案的较旧版本时，环境会提示用户升级。

- 如果在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 调用中未指定 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> 标志，则必须提示用户升级项目文件。

     下面是一个升级提示消息示例：

     “项目“%1”由 Visual Studio 的较旧版本创建。 如果使用此版本的 Visual Studio 打开它，你将不能用较旧版本的 Visual Studio 打开它。 是否要继续并打开此项目？”

### <a name="to-implement-ivsprojectupgradeviafactory"></a>实现 IVsProjectUpgradeViaFactory

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口的方法，特别是项目工厂实现中的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法，或使该实现可从项目工厂实现中调用。

2. 如果你想要将就地升级作为解决方案打开的一部分而进行，则在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 实现中提供 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> 标志作为 `VSPUVF_FLAGS` 参数。

3. 如果你想要将就地升级作为解决方案打开的一部分而进行，则在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 实现中提供 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_COPYBACKUP> 标志作为 `VSPUVF_FLAGS` 参数。

4. 对于步骤 2 和步骤 3 而言，实际文件升级步骤（使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>）可按以下“实现 `IVsProjectUpgade`”部分中所述进行实现，或可将实际文件升级委派到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>。

5. 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> 的方法来为使用 Visual Studio 迁移向导的用户发布升级相关消息。

6. <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileUpgrade> 接口用于实现需作为项目升级一部分而发生的任何类型的文件升级。 此接口不从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 调用，但会将其作为一种机制用来对属于项目系统、但主项目系统可能不会直接感知到的文件进行升级。 例如，如果编译器相关文件和属性未由处理项目系统其余部分的同一开发团队处理，则可能会发生这种情况。

### <a name="ivsprojectupgrade-implementation"></a>IVsProjectUpgrade 实现

如果项目系统仅实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>，则它不能参与**Visual Studio 转换向导**。 但即使你实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 接口，仍可将文件升级委派到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 实现。

#### <a name="to-implement-ivsprojectupgrade"></a>实现 IVsProjectUpgrade

1. 用户尝试打开一个项目时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 方法将由环境在项目打开后、在项目上执行任何其他用户操作前调用。 如果已提示用户升级解决方案，则 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> 标志将传入 `grfUpgradeFlags` 参数。 如果用户直接打开项目（例如通过使用 "**添加现有项目**" 命令），则不会传递 <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> 标志，并且项目需要提示用户进行升级。

2. 在响应 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 调用时，该项目必须评估是否升级该项目文件。 如果项目不需要将项目类型升级到新版本，则可以只返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 标志。

3. 如果项目需要将项目类型升级到新版本，则它必须确定是否通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 方法和为 `rgfQueryEdit` 参数传入 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> 值来修改项目文件。 该项目接下来需要执行以下操作：

    - 如果 `pfEditCanceled` 参数中返回的 `VSQueryEditResult` 值是 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK>，则升级可以继续，因为项目文件可以进行编写。

    - 如果 `pfEditCanceled` 参数中返回的 `VSQueryEditResult` 值是 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> 且 `VSQueryEditResult` 值设置了 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyNotUnderScc> 位，则 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 必须返回失败，因为用户应该自己解决权限问题。 该项目接下来应执行以下操作：

         通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 向用户报告错误，并将 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> 错误代码返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>。

    - 如果 `VSQueryEditResult` 值是 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> 且 `VSQueryEditResultFlags` 值设置了 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> 位，则应通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>（<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ForceEdit_NoPrompting>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_DisallowInMemoryEdits>、...）签出项目文件。

4. 如果项目文件上的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 调用导致文件被签出、最新版本被检索，则卸载并重新加载项目。 一旦创建了项目的另一个实例，将会再次调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 方法。 在这第二次调用上，项目文件可以写入磁盘；建议项目使用 .OLD 扩展名按以前的格式保存项目文件的副本、进行必要的升级更改，并以新格式保存项目文件。 同样，如果升级过程的任何部分失败，该方法必须通过返回 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> 指示失败。 这将导致项目无法在解决方案资源管理器中卸载。

     务必了解在环境中发生的整个过程，以应对调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 方法（指定 ReportOnly 的值）将返回 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> 和 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> 标志的情况。

5. 用户尝试打开项目文件。

6. 环境调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> 实现。

7. 如果 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> 返回 `true`，则环境将调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> 实现。

8. 环境调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> 实现，以打开该文件并初始化项目对象，如 Project1。

9. 环境调用你的 `IVsProjectUpgrade::UpgradeProject` 实现来确定是否需要升级项目文件。

10. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 并为 `rgfQueryEdit` 参数传入 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ReportOnly> 值。

11. 环境将为 `VSQueryEditResult` 返回 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> 且将在 `VSQueryEditResultFlags` 中设置 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> 位。

12. 你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> 实现调用 `IVsQueryEditQuerySave::QueryEditFiles`（<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ForceEdit_NoPrompting>、<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_DisallowInMemoryEdits>）。

此调用可能导致项目文件的新副本被签出、最新版本被检索，以及需要重新加载项目文件。 在这种情况下，将发生以下两种情况中的一种：

- 如果你处理自己的项目重载，则环境将调用你的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> (VSITEMID_ROOT) 实现。 当你收到此调用时，请重新加载项目的第一个实例 (Project1) 并继续升级项目文件。 如果你为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>) 返回 `true`，则环境知道你将处理自己的项目重载。

- 如果你不处理自己的项目重载，则需为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>) 返回 `false`。 在这种情况下，在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>（QEF_ForceEdit_NoPrompting，QEF_DisallowInMemoryEdits）返回之前，环境会创建项目的另一个新实例（例如 Project2），如下所示：

    1. 环境在你的第一个项目对象 Project1 上调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.Close%2A>，因此使此对象处于非活动状态。

    2. 环境调用你的 `IVsProjectFactory::CreateProject` 实现来创建项目的第二个实例 Project2。

    3. 环境调用你的 `IPersistFileFormat::Load` 实现，以打开该文件并初始化第二个项目对象 Project2。

    4. 环境第二次调用 `IVsProjectUpgrade::UpgradeProject` 以确定是否应升级项目对象。 但是，此调用在项目的第二个新实例 Project2 上进行。 这就是在解决方案中打开的项目。

        > [!NOTE]
        > 如果第一个项目实例 Project1 处于非活动状态，则你必须从对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> 实现的首次调用中返回 <xref:Microsoft.VisualStudio.VSConstants.S_OK>。

    5. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 并为 `rgfQueryEdit` 参数传入 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ReportOnly> 值。

    6. 环境将返回 <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK> 且升级可以继续，因为项目文件可以进行编写。

如果不能升级，请从 `IVsProjectUpgrade::UpgradeProject` 返回 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED>。 如果不需要升级或你选择不升级，请将 `IVsProjectUpgrade::UpgradeProject` 调用视作不执行任何操作。 如果返回 <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED>，则向项目的解决方案添加占位符节点。

## <a name="upgrading-project-items"></a>升级项目项

如果在不实现的项目系统内添加或管理项，可能需要参与项目升级过程。 Crystal Reports 是可以添加到项目系统中的项的一个示例。

通常，项目项实施人员希望利用已经完全实例化和升级的项目，因为他们需要知道项目引用是什么，以及有哪些其他项目属性来做出升级决策。

### <a name="to-get-the-project-upgrade-notification"></a>获取项目升级通知

1. 在项目项实现中设置 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading> 标志（在 vsshell80 中定义）。 当 Visual Studio shell 确定项目系统正在升级时，这会导致项目项 VSPackage 自动加载。

2. 通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A> 方法建议 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> 接口。

3. 当项目系统实现完成其升级操作并创建新的已升级项目后，将激发 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> 接口。 根据具体的方案，<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> 接口会在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> 方法之后激发。

### <a name="to-upgrade-the-project-item-files"></a>升级项目项文件

1. 你必须在项目项实现中仔细管理文件备份过程。 这特别适用于并行备份，其中，<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 方法的 `fUpgradeFlag` 参数设置为 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP>，其中已备份的文件沿着指定为 ".old" 的侧文件放置。 在升级项目之前，备份的文件早于系统时间，可以指定为过时。 而且，它们可能会被覆盖，除非你采取特定的步骤来防止出现这种情况。

2. 当项目项收到项目升级通知时，仍然会显示**Visual Studio 转换向导**。 因此，应使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> 接口的方法向向导 UI 提供升级消息。

## <a name="see-also"></a>另请参阅

- [项目](../../extensibility/internals/projects.md)
