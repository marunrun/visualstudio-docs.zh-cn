---
title: VSPackage 安装方案 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
ms.assetid: d2928498-f27c-46b4-a9cd-cba41fd85a10
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a09b794a6cd81966df45a1b30182040d7ab9335e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696746"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage 安装方案
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要设计 VSPackage 安装程序的灵活性至关重要。 例如，可能需要在将来发布的安全修补程序或可能更改业务策略需要全面的并行版本控制支持。  
  
 在中[支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)，你可以阅读的优点和问题的支持由并行安装的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]与你的 VSPackage 的共享或通过并行安装。 简单地说，通过并行 Vspackage 提供最大的灵活性以支持新功能的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 本主题中讨论的方案不是唯一的选择，但它们显示为建议的最佳方法。  
  
## <a name="components-privacy-and-sharing"></a>组件、 隐私和共享  
  
##### <a name="make-your-components-independent"></a>使您的组件独立  
 一旦识别并填充一个组件，将分配`GUID`，和部署组件，则不能更改其构成。 如果您更改组件的组合，生成的组件必须具有一个新的新组件`GUID`。 给定这些事实，每个组件独立、 以及独自单位，从而能够提供最大的版本控制灵活性。 有关用于管理组件的规则的详细信息，请参阅[更改组件代码](https://msdn.microsoft.com/library/aa367849\(VS.85\).aspx)并[会发生什么情况组件规则被破坏？](https://msdn.microsoft.com/library/aa372795\(VS.85\).aspx)。  
  
##### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>不混用在组件中的共享和专用资源  
 引用计数会在组件级别上发生。 因此，混合使用一个组件中的共享和专用资源会导致无法更新专用资源，如可执行文件，而不会还覆盖共享的资源。 这种情况下创建向后兼容性问题，并会限制您只能从创建的并行功能。  
  
 例如，注册表值用于注册与你的 VSPackage[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]应始终在组件中独立于用来注册你的 VSPackage 使用[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 共享的文件或注册表值进入另一个组件。  
  
## <a name="scenario-1-shared-vspackage"></a>方案 1:共享的 VSPackage  
 在此方案中，共享的 VSPackage (支持多个版本的单一二进制文件[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]) 在 Windows 安装程序包中提供。 注册的每个版本[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]受用户可选功能。 这还意味着，当分配给单独的功能，每个组件选择单独的安装或卸载，使用户具有控制集成到不同版本的 VSPackage 的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 (请参阅[Windows 安装程序功能](https://msdn.microsoft.com/library/aa372840\(VS.85\).aspx)有关使用 Windows Installer 程序包中的功能的详细信息。)  
  
 ![VS 共享 vs 包图](../../extensibility/internals/media/vs-sharedpackage.gif "VS_SharedPackage")  
共享的 VSPackage 安装程序  
  
 图中所示，共享的组件进行 Feat_Common 功能，始终安装的一部分。 通过使 Feat_VS2002 和 Feat_VS2003 功能可见，用户可以选择在安装时的版本到[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]他们想 VSPackage 进行集成。 用户还可以使用 Windows 安装程序维护模式来添加或删除功能，在这种情况下添加或删除来自不同版本的 VSPackage 注册信息[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
> [!NOTE]
> 将功能的显示列设置为 0 可隐藏它。 低级别的列的值，如 1，可确保始终在安装。 有关详细信息，请参阅[INSTALLLEVEL 属性](https://msdn.microsoft.com/library/aa369536\(VS.85\).aspx)并[功能表](https://msdn.microsoft.com/library/aa368585.aspx)。  
  
## <a name="scenario-2-shared-vspackage-update"></a>方案 2:共享的 VSPackage 更新  
 在此方案中，随附方案 1 中的 VSPackage 安装程序的更新的版本。 为了便于讨论，更新增加了对支持[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，但它也可能是更简单安全修补程序或修复 bug 的 service pack。 安装较新的组件的 Windows 安装程序的规则需要已在系统上不变的组件不会再次复制。 在这种情况下，使用版本 1.0 已存在的系统将覆盖更新的组件 Comp_MyVSPackage.dll，并使用户可以选择添加新功能 Feat_VS2005 Comp_VS2005_Reg 与其组件。  
  
> [!CAUTION]
> 每当在的多个版本间共享 VSPackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，很重要的 vspackage 的后续版本保持与早期版本的向后兼容性[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 其中不能保持向后兼容，则必须使用通过并行、 专用的 Vspackage。 有关详细信息，请参阅[支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)。  
  
 ![VS 共享 VS 包更新图像](../../extensibility/internals/media/vs-sharedpackageupdate.gif "VS_SharedPackageUpdate")  
共享的 VSPackage 更新安装程序  
  
 此方案提供了一个新的 VSPackage 安装程序，充分利用对于次要升级的 Windows 安装程序的支持。 用户只需安装版本 1.1 和 1.0 版，它将升级。 但是，不需要具有在系统上的版本 1.0。 相同的安装程序将没有 1.0 版的系统上安装版本 1.1。 若要提供次要升级以这种方式的优点是不需要经历的开发升级安装程序和完整产品安装程序的工作。 一个安装程序执行这两个作业。 安全修补程序或服务包可能会改为利用 Windows Installer 修补程序。 有关详细信息，请参阅[修补和升级](https://msdn.microsoft.com/library/aa370579\(VS.85\).aspx)。  
  
## <a name="scenario-3-side-by-side-vspackage"></a>方案 3:通过并行 VSPackage  
 此方案提供了两个 VSPackage 安装程序 — 一个用于每个版本的 Visual Studio.NET 2003年和[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 每个安装程序安装的并排方案或专用，VSPackage (一个用于专门构建并为特定版本的安装[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)])。 每个 VSPackage 位于其自己的组件。 因此，每个可以在单独提供修补程序或维护释放。 VSPackage DLL 现在是特定于版本的因为它是安全地将其注册信息包括在与 DLL 相同的组件。  
  
 ![VS 端&#45;的&#45;端 VS 包图](../../extensibility/internals/media/vs-sbys-package.gif "VS_SbyS_Package")  
通过并行 VSPackage 安装程序  
  
 每个安装程序还包括两个安装程序之间共享的代码。 如果共享的代码安装到常见位置，安装这两个.msi 文件将仅一次安装共享的代码。 第二个安装程序只是递增引用计数在组件上。 引用计数可确保如果卸载了其中一个 Vspackage，共享的代码将保持为其他 VSPackage。 如果也卸载了第二个 VSPackage，将删除的共享的代码。  
  
## <a name="scenario-4-side-by-side-vspackage-update"></a>方案 4:通过并行 VSPackage 更新  
 在此方案中，为你的 VSPackage[!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]之间发生从安全漏洞，并且需要发出更新。 如方案 2，可以创建新的.msi 文件更新现有安装来包括安全修复程序，以及部署新安装与已到位的安全修补程序。  
  
 在这种情况下，VSPackage 是安装在全局程序集缓存 (GAC) 中托管的 VSPackage。 当您重新生成使之包括安全修补程序时，则必须更改程序集版本号的修订号部分。 注册信息的新的程序集版本号会覆盖以前的版本，从而导致[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]固定的程序集加载。  
  
 ![VS 端&#45;的&#45;端 VS 包更新图形](../../extensibility/internals/media/vs-sbys-packageupdate.gif "VS_SbyS_PackageUpdate")  
通过并行 VSPackage 更新安装程序  
  
 **请注意**部署的并行程序集的详细信息，请参阅[简化部署和使用.NET Framework 解决 DLL Hell](https://msdn.microsoft.com/library/ms973843.aspx)。  
  
## <a name="see-also"></a>请参阅  
 [Windows 安装程序](https://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)   
 [支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
