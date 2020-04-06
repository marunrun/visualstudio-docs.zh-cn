---
title: VS包设置方案 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01279666642adb729d4350b8a497c42d78159120
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703974"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage 安装方案

设计 VSPackage 安装程序以获得灵活性非常重要。 例如，您可能需要在将来发布安全修补程序，或者可能更改需要全面并行版本控制支持的业务策略。

在[支持 Visual Studio 的多个版本中](../../extensibility/supporting-multiple-versions-of-visual-studio.md)，您可以阅读有关[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过 VSPackage 的共享或并行安装支持并行安装的优势和问题。 简而言之，并排 VSPackages 使您能够最灵活地支持 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]新功能。

本主题中讨论的方案不是您唯一的选择，而是作为建议的最佳做法呈现的。

## <a name="components-privacy-and-sharing"></a>组件、隐私和共享

### <a name="make-your-components-independent"></a>使组件独立

标识和填充组件、分配 和`GUID`部署组件后，无法更改其组合。 如果确实更改了组件的合成，则生成的组件必须是具有新`GUID`的新组件。 鉴于这些事实，通过使每个组件独立、自力更生的单元，提供了最大的版本控制灵活性。 有关管理组件的规则的详细信息，请参阅[更改组件代码](/windows/desktop/Msi/changing-the-component-code)，[以及如果组件规则断开会发生什么情况？](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>不要将共享资源和私有资源混合在组件中

引用计数发生在组件级别。 因此，将共享和私有资源混合到一个组件中，使得无需覆盖共享资源即可更新私有资源（如可执行文件）。因此，在一个组件中混合共享资源和私有资源时，无法更新私有资源。 此方案会产生向后兼容性问题，并限制您创建并行功能。

例如，用于将 VSPackage 注册到 的[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]注册表值应保存在与用于在 Visual Studio 注册 VSPackage 的组件分开的组件中。 共享文件或注册表值进入另一个组件。

## <a name="scenario-1-shared-vspackage"></a>方案 1：共享 VS 包

在这种情况下，共享 VS 包（支持多个版本的 Visual Studio 的单个二进制文件）在 Windows 安装程序包中提供。 注册到每个版本的 Visual Studio 都由用户可选择的功能控制。 这也意味着，当分配给单独的功能时，可以单独选择每个组件进行安装或卸载，从而使用户能够控制将 VSPackage 集成到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不同版本的 中。 （有关在 Windows 安装程序包中使用功能的详细信息，请参阅[Windows 安装程序功能](/windows/desktop/Msi/windows-installer-features)。

![VS 共享 VS 包安装程序](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

如图所示，共享组件是Feat_Common功能的一部分，该功能始终安装。 通过使Feat_VS2002和Feat_VS2003功能可见，用户可以在安装时选择要将 VSPackage 集成到哪些版本的 Visual Studio。 用户还可以使用 Windows 安装程序维护模式添加或删除功能，在这种情况下，这些功能会从 Visual Studio 的不同版本添加或删除 VSPackage 注册信息。

> [!NOTE]
> 将要素的"显示"列设置为 0 会隐藏它。 低级别列值（如 1）可确保始终安装该列。 有关详细信息，请参阅[INSTALLLEVEL 属性](/windows/desktop/Msi/installlevel)和[功能表](/windows/desktop/Msi/feature-table)。

## <a name="scenario-2-shared-vspackage-update"></a>方案 2：共享 VS 包更新

在这种情况下，方案 1 中的 VSPackage 安装程序的更新版本已发运。 为了讨论，该更新增加了对 Visual Studio 的支持，但它也可以是一个更简单的安全修补程序或错误修复服务包。 Windows 安装程序安装较新组件的规则要求不复制系统上已有的未更改组件。 在这种情况下，已有版本 1.0 的系统将覆盖更新的组件 Comp_MyVSPackage.dll，并允许用户选择Feat_VS2005添加新功能及其组件Comp_VS2005_Reg。

> [!CAUTION]
> 每当 VSPackage 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]多个版本之间共享时，VSPackage 的后续版本必须保持与 Visual Studio 的早期版本的向后兼容性。 如果无法保持向后兼容性，则必须并行使用私有 VSPackages。 有关详细信息，请参阅[支持可视化工作室的多个版本](../../extensibility/supporting-multiple-versions-of-visual-studio.md)。

![VS 共享 VS 软件包更新安装程序](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

此方案提供了新的 VSPackage 安装程序，利用 Windows 安装程序对次要升级的支持。 用户只需安装版本 1.1，即可升级版本 1.0。 但是，系统上没有必要使用版本 1.0。 同一安装程序将在没有版本 1.0 的系统上安装版本 1.1。 以这种方式提供次要升级的优点是，无需完成开发升级安装程序和完整产品安装程序的工作。 一个安装程序执行两个作业。 安全修补程序或服务包可能会利用 Windows 安装程序修补程序。 有关详细信息，请参阅[修补和升级](/windows/desktop/Msi/patching-and-upgrades)。

## <a name="scenario-3-side-by-side-vspackage"></a>方案 3：并排 VS 包

此方案提供两个 VSPackage 安装程序 - 每个版本的 Visual Studio .NET 2003 和 Visual Studio 一个。 每个安装程序都安装并排或私有的 VSPackage（专为特定版本的 Visual Studio 构建和安装的 VSPackage）。 每个 VS 包都位于其自己的组件中。 因此，每个都可以使用修补程序或维护版本单独提供服务。 由于 VSPackage DLL 现在特定于版本，因此可以安全地将其注册信息包含在与 DLL 相同的组件中。

![VS 并排 VS 软件包安装程序](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

每个安装程序还包括两个安装程序之间共享的代码。 如果共享代码安装到公共位置，则安装两个 .msi 文件将仅安装一次共享代码。 第二个安装程序只是增加组件上的引用计数。 引用计数可确保，如果卸载了其中一个 VS 包，则共享代码将保留为另一个 VSPackage。 如果卸载第二个 VSPackage，则将删除共享代码。

## <a name="scenario-4-side-by-side-vspackage-update"></a>方案 4：并排 VS 包更新

在这种情况下，适用于 Visual Studio 的 VSPackage 存在安全漏洞，您需要发布更新。 与方案 2 一样，您可以创建一个新的 .msi 文件，该文件会更新现有安装以包括安全修补程序，并在安全修补程序已到位的情况下部署新安装。

在这种情况下，VSPackage 是安装在全局程序集缓存 （GAC） 中的托管 VS 包。 重新生成它以包括安全修补程序时，必须更改程序集版本号的修订号部分。 新程序集版本号的注册信息覆盖以前的版本，从而导致[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载固定程序集。

![VS 并排 VS 软件包更新安装程序](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

有关并行程序集部署的详细信息，请参阅[使用 .NET 框架简化部署和解决 DLL 地狱](https://msdn.microsoft.com/library/ms973843.aspx)。

## <a name="see-also"></a>请参阅

- [Windows 安装程序](/windows/desktop/Msi/windows-installer-portal)
- [支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
