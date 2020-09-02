---
title: 设计器初始化和元数据配置 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703068"
---
# <a name="designer-initialization-and-metadata-configuration"></a>设计器初始化和元数据配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

操作与设计器或设计器组件关联的元数据和筛选器属性提供了一种机制，应用程序可以使用该机制来定义特定设计器使用哪些工具来处理不同的 <xref:System.Type> 对象 (例如数据结构、类或图形实体) 在设计器可用时，以及如何将 Visual STUDIO IDE 配置为支持设计器 (例如， **工具箱** 类别或选项卡可用) 。  
  
 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]提供了几种机制来帮助控制设计器或设计器组件的初始化，并通过 VSPackage 来操作其元数据。  
  
## <a name="initializing-metadata-and-configuration-information"></a>初始化元数据和配置信息  
 由于它们是按需加载的，因此，在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实例化设计器之前，环境可能尚未加载 vspackage。 因此，在创建时，Vspackage 不能使用标准机制来配置设计器或设计器组件，而是处理 <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> 事件。 相反，VSPackage 实现接口的一个实例， <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 并注册其自身以提供自定义项，称为设计图面扩展。  
  
### <a name="customizing-initialization"></a>自定义初始化  
 自定义设计器、组件或设计器图面涉及：  
  
1. 修改设计器元数据，并有效地更改 <xref:System.Type> 访问或转换特定的方式。  
  
     通常通过或机制完成此 <xref:System.Drawing.Design.UITypeEditor> 操作 <xref:System.ComponentModel.TypeConverter> 。  
  
     例如，当 <xref:System.Windows.Forms> 初始化基于的设计器时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 环境将修改 <xref:System.Drawing.Design.UITypeEditor> <xref:System.Web.UI.WebControls.Image> 与设计器一起使用的对象的，以使用资源管理器来获取位图而不是文件系统。  
  
2. 与环境集成，例如，通过订阅事件或获取项目配置信息。 可以获取项目配置信息，并通过获取界面来订阅事件 <xref:System.ComponentModel.Design.ITypeResolutionService> 。  
  
3. 通过激活适当的 **工具箱** 类别来修改用户环境，或通过将类的实例应用于设计器来限制设计器的适用性 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 。  
  
### <a name="designer-initialization-by-a-vspackage"></a>VSPackage 的设计器初始化  
 VSPackage 应通过以下方式处理设计器初始化：  
  
1. 创建实现类的对象 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 。  
  
   > [!NOTE]
   > <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>类绝不应在与类相同的对象上实现 <xref:Microsoft.VisualStudio.Shell.Package> 。  
  
2. <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>通过将的实例 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> 和 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 提供 VSPackage 的实现的类，将实现的类注册为提供对 VSPackage 的设计器扩展的支持 <xref:Microsoft.VisualStudio.Shell.Package> 。  
  
   每次创建设计器或设计器组件时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 环境：  
  
3. 访问每个注册的设计图面扩展提供程序。  
  
4. 实例化并初始化每个设计图面扩展提供程序的 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 对象的实例  
  
5.  (适当的) 调用每个设计图面扩展提供程序的 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> 方法或 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> 方法。  
  
   <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>作为 VSPackage 的成员实现对象时，请务必了解：  
  
6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]环境不提供对特定 `DesignSurfaceExtension` 提供程序修改的元数据或其他配置设置的任何控制。 两个或多个 `DesignSurfaceExtension` 提供程序在冲突的方式下修改相同的设计器功能，最后一项修改是有可能的。 这是不确定的。  
  
7. 可以 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 通过将的实例应用于该实现，将对象的实现显式限制为特定设计器 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 。 有关 **工具箱** 项筛选的详细信息，请参阅 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 和 <xref:System.ComponentModel.ToolboxItemFilterType> 。  
  
## <a name="additional-metadata-provisioning"></a>其他元数据预配  
 在设计时，VSPackage 可以更改设计器或设计器组件的配置。  
  
 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>可以通过编程方式使用类，也可以将其应用于提供设计器的 VSPackage。  
  
 类的实例 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 用于修改设计图面上创建的组件的元数据。 例如，可以 <xref:System.Windows.Forms.CommonDialog> 使用自定义属性浏览器替换对象使用的默认属性浏览器。  
  
 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>应用到 VSPackage 的实现的实例提供的修改 <xref:Microsoft.VisualStudio.Shell.Package> 可以具有以下两个范围之一：  
  
- 全局--对于给定组件的所有新实例  
  
- Local--仅与在当前 VSPackage 提供的设计图面上创建的组件的实例相关。  
  
  `IsGlobal` <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 应用到 VSPackage 的实现的实例的属性 <xref:Microsoft.VisualStudio.Shell.Package> 决定了此范围。  
  
  将特性应用到的实现 <xref:Microsoft.VisualStudio.Shell.Package> ，并将 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> 对象的属性 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 设置为 `true` ，如下所示，更改整个环境的浏览器 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ：  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
  如果全局标志设置为，则 `false` 元数据更改将在当前 VSPackage 支持的当前设计器的本地：  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
> [!NOTE]
> 目前，设计图面仅支持创建组件，因此仅组件可以具有本地元数据。 在上面的示例中，我们尝试修改属性，如 `Color` 对象的属性。 如果 `false` 为 global 标志传入了，则 `CustomBrowser` 永远不会出现，因为设计器实际上不会创建的实例 `Color` 。 将全局标志设置为 `false` 对于组件（如控件、计时器和对话框）很有用。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>   
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>   
 <xref:System.ComponentModel.ToolboxItemFilterType>   
 [扩展设计时支持](https://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)
