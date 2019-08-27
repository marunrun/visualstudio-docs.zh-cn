---
title: 设计器的初始化和元数据配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2dec3937616c712c56b7012949e044702e6b11f2
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703068"
---
# <a name="designer-initialization-and-metadata-configuration"></a>设计器初始化和元数据配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

与设计器或设计器组件关联的元数据和筛选器特性的操作提供了应用程序定义将哪些工具由特定的设计器，以处理不同的机制<xref:System.Type>对象 （如数据结构类或图形实体），在设计器不可用时，以及如何配置 Visual Studio IDE 以支持在设计器 (对于实例这**工具箱**类别或选项卡上的可用)。  
  
 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]提供多种机制来促进设计器或设计器组件的初始化的控件和操作的 vspackage 及其元数据。  
  
## <a name="initializing-metadata-and-configuration-information"></a>初始化元数据和配置信息  
 由于它们是按需加载，不可能已通过加载 Vspackage[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]之前在设计器的实例化的环境。 因此，Vspackage 不能使用标准机制，用于配置设计器或设计器组件在创建时，它将处理<xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated>事件。 相反，VSPackage 实现的实例<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>接口，并注册自己以提供自定义项，称为设计图面上扩展。  
  
### <a name="customizing-initialization"></a>自定义初始化  
 自定义设计器、 组件或设计器图面，包括：  
  
1. 修改设计器元数据和有效地更改如何在特定<xref:System.Type>访问属性或转换。  
  
     这通常是通过<xref:System.Drawing.Design.UITypeEditor>或<xref:System.ComponentModel.TypeConverter>机制。  
  
     例如，当<xref:System.Windows.Forms>-基于设计器进行了初始化，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]环境修改<xref:System.Drawing.Design.UITypeEditor>为<xref:System.Web.UI.WebControls.Image>与设计器使用，以使用资源管理器获取位图而不是文件系统对象。  
  
2. 将与集成环境，例如，通过订阅事件，或获取项目的配置信息。 可以获取项目的配置信息和订阅事件，通过获取<xref:System.ComponentModel.Design.ITypeResolutionService>接口。  
  
3. 通过激活相应的用户环境修改**工具箱**类别或通过限制通过应用的实例的设计器的适用性<xref:System.ComponentModel.ToolboxItemFilterAttribute>到设计器的类。  
  
### <a name="designer-initialization-by-a-vspackage"></a>设计器初始化的 vspackage  
 VSPackage 应处理由设计器初始化：  
  
1. 创建一个对象，实现<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>类。  
  
   > [!NOTE]
   > <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>类应永远不会在与相同的对象上实现<xref:Microsoft.VisualStudio.Shell.Package>类。  
  
2. 注册类实现<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>作为 VSPackage 的设计器扩展提供支持，通过应用的实例<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>，<xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute>并<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>到提供的 VSPackage 的实现类<xref:Microsoft.VisualStudio.Shell.Package>.  
  
   每当创建任何设计器或设计器组件时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]环境：  
  
3. 访问每个已注册的设计图面上的扩展提供程序。  
  
4. 实例化并初始化每个设计面扩展提供程序实例的<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>对象  
  
5. 调用每个设计面扩展提供商<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A>方法或<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A>（根据需要） 的方法。  
  
   在实现时<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>对象作为自己的 VSPackage，成员是重要的：  
  
6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]环境不提供任何控制哪些元数据或其他配置设置的特定`DesignSurfaceExtension`提供程序的修改。 可以为两个或多个`DesignSurfaceExtension`进行最终修改要明确冲突的方式修改相同的设计器功能的提供程序。 它是不确定上次应用的修改。  
  
7. 可以显式限制的实现<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>到特定设计器中，通过应用的实例对象<xref:System.ComponentModel.ToolboxItemFilterAttribute>到该实现。 有关详细信息**工具箱**项筛选，请参阅<xref:System.ComponentModel.ToolboxItemFilterAttribute>和<xref:System.ComponentModel.ToolboxItemFilterType>。  
  
## <a name="additional-metadata-provisioning"></a>预配其他元数据  
 VSPackage 可以更改在设计时设计器或设计器以外的其他组件的配置。  
  
 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>类可用于以编程方式，或应用于 VSPackage 提供设计器。  
  
 实例<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>类用于修改设计图面上创建的组件的元数据。 例如，一个可以替换默认属性浏览器使用的<xref:System.Windows.Forms.CommonDialog>具有自定义属性浏览器对象。  
  
 修改提供的实例<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>应用于的 VSPackage 的实现<xref:Microsoft.VisualStudio.Shell.Package>可以具有两个作用域之一：  
  
- 全局-的所有新实例的给定组件  
  
- 本地-与有关仅对当前的 VSPackage 提供的设计图面上创建的组件的实例。  
  
  `IsGlobal`的属性<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>应用到 VSPackage 的实现的实例<xref:Microsoft.VisualStudio.Shell.Package>确定此作用域。  
  
  将特性应用到的实现<xref:Microsoft.VisualStudio.Shell.Package>与<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A>的属性<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>对象设置为`true`，如下所示，更改浏览器，以便整个[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]环境：  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
  如果全局标志已设置为`false`，则此元数据更改当前设计器支持的当前 VSPackage 的本地：  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
> [!NOTE]
> 在存在时，设计图面上仅支持创建组件，因此只有组件可以使本地元数据。 在上面的示例中，我们已尝试修改一个属性，如`Color`对象的属性。 如果`false`传入的全局标志`CustomBrowser`将永远不会显示，因为在设计器永远不会实际创建的实例`Color`。 全局标志设置为`false`对于组件，如控件、 计时器和对话框很有用。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>   
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>   
 <xref:System.ComponentModel.ToolboxItemFilterType>   
 [扩展设计时支持](https://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)
