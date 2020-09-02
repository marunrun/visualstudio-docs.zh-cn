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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696746"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage 安装方案
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设计 VSPackage 安装程序以获得灵活性，这一点很重要。 例如，你可能需要在未来发布安全修补程序，或者可以更改需要完全并行版本控制支持的业务策略。  
  
 在 [支持 Visual Studio 的多个版本](../../extensibility/supporting-multiple-versions-of-visual-studio.md)中，你可以阅读有关支持并行安装的优点和问题，其中包括 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPackage 的共享或并行安装。 简而言之，并行 Vspackage 为你提供了支持的新功能的最大灵活性 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 本主题中讨论的方案并不是您唯一的选择，但将作为建议的最佳实践提供。  
  
## <a name="components-privacy-and-sharing"></a>组件、隐私和共享  
  
##### <a name="make-your-components-independent"></a>使组件独立  
 标识并填充组件后，分配并 `GUID` 部署组件，无法更改其组合。 如果更改了组件的组合，则生成的组件必须是新的包含新组件的组件 `GUID` 。 考虑到这些事实，通过使每个组件独立于独立的单元，实现最大版本的灵活性。 有关控制组件规则的详细信息，请参阅 [更改组件代码](https://msdn.microsoft.com/library/aa367849\(VS.85\).aspx) 和 [如果组件规则损坏会发生什么情况？](https://msdn.microsoft.com/library/aa372795\(VS.85\).aspx)。  
  
##### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>不要将共享资源和专用资源混合到组件中  
 引用计数发生在组件级别上。 因此，将共享资源和专用资源混合到一个组件中，无法更新专用资源（如可执行文件），也不会覆盖共享资源。 此方案会创建向后兼容性问题，并限制你创建并行功能。  
  
 例如，用于注册 VSPackage 的注册表值 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 应保留在独立于用于向注册 VSPackage 的组件中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 共享的文件或注册表值还会出现在另一个组件中。  
  
## <a name="scenario-1-shared-vspackage"></a>方案1：共享 VSPackage  
 在这种情况下，共享 VSPackage (单个二进制文件，该二进制文件支持) 的多个版本， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 并随附 Windows Installer 包。 使用的每个版本 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 进行注册都是由用户选择的功能控制的。 这也意味着，当分配给不同的功能时，可以单独选择每个组件以进行安装或卸载，使用户能够控制将 VSPackage 集成到不同版本的中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  (参阅 [Windows Installer 功能](https://msdn.microsoft.com/library/aa372840\(VS.85\).aspx) ，以获取有关在 Windows Installer 包中使用功能的详细信息 )   
  
 ![VS 共享 VS 包图](../../extensibility/internals/media/vs-sharedpackage.gif "VS_SharedPackage")  
共享的 VSPackage 安装程序  
  
 如图所示，共享组件成为 Feat_Common 功能的一部分，该功能始终是安装的。 通过使 Feat_VS2002 和 Feat_VS2003 功能可见，用户可以在安装时选择 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 要将 VSPackage 集成到其中的版本。 用户还可以使用 Windows Installer 维护模式来添加或删除功能，在这种情况下，将从不同版本的中添加或删除 VSPackage 注册信息 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
> [!NOTE]
> 将功能的显示列设置为0会隐藏该功能。 较低级别的列值（例如1）可确保始终安装该值。 有关详细信息，请参阅 [INSTALLLEVEL 属性](https://msdn.microsoft.com/library/aa369536\(VS.85\).aspx) 和 [功能表](https://msdn.microsoft.com/library/aa368585.aspx)。  
  
## <a name="scenario-2-shared-vspackage-update"></a>方案2：共享的 VSPackage 更新  
 在此方案中，将提供方案1中 VSPackage 安装程序的更新版本。 为了进行讨论，更新添加了对的支持 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，但它也可能是更简单的安全修补程序或 bug 修复 Service Pack。 Windows Installer 用于安装更新的组件的规则要求系统上已有的未更改组件不重新复制。 在这种情况下，版本为1.0 的系统将覆盖更新的组件 Comp_MyVSPackage.dll 并让用户选择添加新功能 Feat_VS2005 及其组件 Comp_VS2005_Reg。  
  
> [!CAUTION]
> 每当在多个版本的中共享 VSPackage 时 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，VSPackage 的后续版本都必须保持与以前版本的向后兼容性 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 如果你不能维护向后兼容性，则必须使用并行的私有 Vspackage。 有关详细信息，请参阅 [支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)。  
  
 ![VS 共享 VS 包更新图像](../../extensibility/internals/media/vs-sharedpackageupdate.gif "VS_SharedPackageUpdate")  
共享 VSPackage 更新安装程序  
  
 此方案提供了一个新的 VSPackage 安装程序，利用 Windows Installer 对次要升级的支持。 用户只需安装版本1.1，版本1.0。 但是，系统不需要安装版本1.0。 同一安装程序将在没有版本1.0 的系统上安装版本1.1。 以这种方式提供小升级的优点是不需要完成开发升级安装程序和完整产品安装程序的工作。 一个安装程序将执行两个作业。 安全修补程序或 Service Pack 可能会改用 Windows Installer 修补程序。 有关详细信息，请参阅 [修补和升级](https://msdn.microsoft.com/library/aa370579\(VS.85\).aspx)。  
  
## <a name="scenario-3-side-by-side-vspackage"></a>方案3：并行 VSPackage  
 此方案提供了两个 VSPackage 安装程序-每个版本的 Visual Studio .NET 2003 和 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 每个安装程序都安装了一种并行或专用的 VSPackage (专门为) 的特定版本构建和安装的安装程序 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 每个 VSPackage 都在其自己的组件中。 因此，每个可以单独提供修补程序或维护版本。 因为 VSPackage DLL 现在是特定于版本的，所以在与 DLL 相同的组件中包含其注册信息是安全的。  
  
 ![通过&#45;端 VS 包图形&#45;VS 端](../../extensibility/internals/media/vs-sbys-package.gif "VS_SbyS_Package")  
并行 VSPackage 安装程序  
  
 每个安装程序还包括在两个安装程序之间共享的代码。 如果共享代码已安装到常见位置，则安装这两个 .msi 文件将只安装一次共享代码。 第二个安装程序只会递增组件上的引用计数。 引用计数可确保在卸载其中一个 Vspackage 时，共享代码仍适用于其他 VSPackage。 如果同时卸载第二个 VSPackage，则将删除共享代码。  
  
## <a name="scenario-4-side-by-side-vspackage-update"></a>方案4：并行 VSPackage 更新  
 在这种情况下，你的 VSPackage [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)] 会遭受安全漏洞的攻击，你需要发出更新。 例如，在方案2中，你可以创建一个新的 .msi 文件，用于更新现有的安装以包含安全修补程序，以及部署已有安全修补程序的新安装。  
  
 在这种情况下，VSPackage 是安装在全局程序集缓存中的托管 VSPackage (GAC) 。 重新生成它以包括安全修补程序时，必须更改程序集版本号的修订号部分。 新程序集版本号的注册信息将覆盖以前的版本，从而导致 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 加载固定程序集。  
  
 ![&#45;端 VS 包更新图形的 VS&#45;](../../extensibility/internals/media/vs-sbys-packageupdate.gif "VS_SbyS_PackageUpdate")  
并行 VSPackage 更新安装程序  
  
 **注意** 有关部署并行程序集的详细信息，请参阅 [使用 .NET Framework 简化部署和解决 DLL Hell](https://msdn.microsoft.com/library/ms973843.aspx)。  
  
## <a name="see-also"></a>另请参阅  
 [Windows Installer](https://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)   
 [支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
