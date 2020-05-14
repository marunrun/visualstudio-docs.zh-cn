---
title: 设计器初始化和元数据配置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e876dd9e6fa95bbe180d1737bc8c4911f16e1e9a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712216"
---
# <a name="designer-initialization-and-metadata-configuration"></a>设计器初始化和元数据配置

操作与设计器或设计器组件关联的元数据和筛选器属性为应用程序提供了一种机制，用于定义特定设计器在设计器可用时使用哪些<xref:System.Type>工具来处理不同的对象（如数据结构、类或图形实体），以及 Visual Studio IDE 如何配置为支持设计器（例如，可用的**工具箱**类别或选项卡）。

提供了[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]几种机制，便于控制设计器或设计器组件的初始化，并通过 VSPackage 操作其元数据。

## <a name="initialize-metadata-and-configuration-information"></a>初始化元数据和配置信息
 由于它们是按需加载的，因此在设计器实例化之前，Visual Studio 环境可能尚未加载 VSPackages。 因此，VSPackages 不能使用标准机制在创建时配置设计器或设计器组件，即处理<xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated>事件。 相反，VSPackage 实现<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>接口的实例并注册自身以提供自定义项，称为设计曲面扩展。

### <a name="customize-initialization"></a>自定义初始化

自定义设计器、组件或设计器表面涉及：

1. 修改设计器元数据并有效更改访问或转换<xref:System.Type>某个特定内容的方式。

    这通常是通过<xref:System.Drawing.Design.UITypeEditor>或<xref:System.ComponentModel.TypeConverter>机制完成的。

    例如，当初始<xref:System.Windows.Forms>化基于 的设计人员时，Visual Studio 环境将修改<xref:System.Drawing.Design.UITypeEditor><xref:System.Web.UI.WebControls.Image>与设计器一起使用的对象，以使用资源管理器获取位图而不是文件系统。

2. 通过订阅事件或获取项目配置信息来与环境集成。 您可以通过获取<xref:System.ComponentModel.Design.ITypeResolutionService>接口获取项目配置信息并订阅事件。

3. 通过激活适当的**工具箱**类别或通过将类的实例应用于设计器来限制设计器的适用性来<xref:System.ComponentModel.ToolboxItemFilterAttribute>修改用户环境。

### <a name="designer-initialization-by-a-vspackage"></a>按 VSPackage 初始化设计器

VSPackage 应按以下操作处理设计器初始化：

1. 创建实现<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>类的对象。

   > [!NOTE]
   > 不应<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>在类的同一对象上实现<xref:Microsoft.VisualStudio.Shell.Package>类。

2. 注册实现<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>为 VSPackage 的设计器扩展提供支持的类。 通过<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>应用 的 实例 来注册<xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute>类，<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>并注册提供 VSPackage 实现 的类<xref:Microsoft.VisualStudio.Shell.Package>。

每当创建设计器或设计器组件时，可视化工作室环境：

- 访问每个已注册的设计曲面扩展提供程序。

- 实例化和初始化每个设计曲面扩展提供程序对象的<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>实例。

- 调用每个设计曲面扩展提供程序<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A>的方法或<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A>方法（视适用）。

当作为<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>VSPackage 的成员实现该对象时，请务必了解：

- Visual Studio 环境不提供对特定`DesignSurfaceExtension`提供程序修改的元数据或其他配置设置的任何控制。 两个或多个`DesignSurfaceExtension`提供程序可能会以冲突的方式修改同一设计器功能，最终修改是决定性的。 最后应用的是哪个修改是不确定的。

- 通过将 对象的<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension><xref:System.ComponentModel.ToolboxItemFilterAttribute>实例应用于该实现，可以显式将对象的实现限制为特定设计器。 有关**工具箱**项目筛选的详细信息，请参阅 和<xref:System.ComponentModel.ToolboxItemFilterAttribute><xref:System.ComponentModel.ToolboxItemFilterType>。

## <a name="additional-metadata-provisioning"></a>其他元数据预配

VSPackage 可以更改设计器或设计器组件的配置，而不是在设计时。

类<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>可以以编程方式使用，也可以应用于提供设计器的 VSPackage。

<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>类的实例用于修改在设计图面上创建的组件的元数据。 例如，可以将<xref:System.Windows.Forms.CommonDialog>对象使用的默认属性浏览器替换为自定义属性浏览器。

应用于 VSPackage 实现<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>的实例提供的修改<xref:Microsoft.VisualStudio.Shell.Package>可以具有两个作用域之一：

- 全局 - 给定组件的所有新实例

- 本地 - 仅与当前 VSPackage 提供的设计表面上创建的组件实例相关。

应用于`IsGlobal`VSPackage<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>实现 的实例的属性<xref:Microsoft.VisualStudio.Shell.Package>决定了此范围。

<xref:Microsoft.VisualStudio.Shell.Package>将属性应用于<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A>对象<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>属性设置为`true`的 实现，如下所示，将更改整个 Visual Studio 环境的浏览器：

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

如果全局标志设置为`false`，则元数据更改是当前 VSPackage 支持的当前设计器的本地：

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> 设计图面仅支持创建组件，因此只有组件可以具有本地元数据。 在上面的示例中，我们尝试修改属性，例如对象`Color`的属性。 如果`false`为全局标志传入，`CustomBrowser`则永远不会出现，因为设计器从未实际创建 的`Color`实例。 将全局标志`false`设置为 对组件（如控件、计时器和对话框）很有用。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [扩展设计时支持](https://msdn.microsoft.com/Library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)
