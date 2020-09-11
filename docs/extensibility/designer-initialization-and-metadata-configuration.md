---
title: 设计器初始化和元数据配置 |Microsoft Docs
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
ms.openlocfilehash: f48d8ebb285bdc8211f590f49e615042b7029d70
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011704"
---
# <a name="designer-initialization-and-metadata-configuration"></a>设计器初始化和元数据配置

操作与设计器或设计器组件关联的元数据和筛选器属性提供了一种机制，应用程序可以使用该机制来定义特定设计器使用哪些工具来处理不同的 <xref:System.Type> 对象 (例如数据结构、类或图形实体) 在设计器可用时，以及如何将 Visual STUDIO IDE 配置为支持设计器 (例如， **工具箱** 类别或选项卡可用) 。

[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]提供了几种机制来帮助控制设计器或设计器组件的初始化，并通过 VSPackage 来操作其元数据。

## <a name="initialize-metadata-and-configuration-information"></a>初始化元数据和配置信息
 由于它们是按需加载的，因此，在实例化设计器之前，Visual Studio 环境可能未加载 Vspackage。 因此，在创建时，Vspackage 不能使用标准机制来配置设计器或设计器组件，而是处理 <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> 事件。 相反，VSPackage 实现接口的一个实例， <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 并注册其自身以提供自定义项，称为设计图面扩展。

### <a name="customize-initialization"></a>自定义初始化

自定义设计器、组件或设计器图面涉及：

1. 修改设计器元数据，并有效地更改 <xref:System.Type> 访问或转换特定的方式。

    通常通过或机制完成此 <xref:System.Drawing.Design.UITypeEditor> 操作 <xref:System.ComponentModel.TypeConverter> 。

    例如，当 <xref:System.Windows.Forms> 初始化基于的设计器时，Visual Studio 环境会修改 <xref:System.Drawing.Design.UITypeEditor> <xref:System.Web.UI.WebControls.Image> 与设计器一起使用的对象的，以使用资源管理器来获取位图，而不是文件系统。

2. 与环境集成，例如，通过订阅事件或获取项目配置信息。 可以获取项目配置信息，并通过获取界面来订阅事件 <xref:System.ComponentModel.Design.ITypeResolutionService> 。

3. 通过激活适当的 **工具箱** 类别来修改用户环境，或通过将类的实例应用于设计器来限制设计器的适用性 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 。

### <a name="designer-initialization-by-a-vspackage"></a>VSPackage 的设计器初始化

VSPackage 应通过以下方式处理设计器初始化：

1. 创建实现类的对象 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 。

   > [!NOTE]
   > <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>类绝不应在与类相同的对象上实现 <xref:Microsoft.VisualStudio.Shell.Package> 。

2. 注册类，该类实现 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 为 VSPackage 的设计器扩展提供支持。 通过  <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 向提供 VSPackage 的实现的类应用、和的实例来注册该类 <xref:Microsoft.VisualStudio.Shell.Package> 。

每当创建设计器或设计器组件时，Visual Studio 环境：

- 访问每个注册的设计图面扩展提供程序。

- 实例化并初始化每个设计图面扩展提供程序的 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> 对象的实例。

-  (适当的) 调用每个设计图面扩展提供程序的 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> 方法或 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> 方法。

<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>作为 VSPackage 的成员实现对象时，请务必了解：

- Visual Studio 环境不提供对特定提供程序修改的元数据或其他配置设置的任何控制 `DesignSurfaceExtension` 。 两个或多个 `DesignSurfaceExtension` 提供程序在冲突的方式下修改相同的设计器功能，最后一项修改是有可能的。 这是不确定的。

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>通过将的实例应用于特定设计器，可以将对象的实现显式限制为特定设计器 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 。 有关 **工具箱** 项筛选的详细信息，请参阅 <xref:System.ComponentModel.ToolboxItemFilterAttribute> 和 <xref:System.ComponentModel.ToolboxItemFilterType> 。

## <a name="additional-metadata-provisioning"></a>其他元数据预配

在设计时，VSPackage 可以更改设计器或设计器组件的配置。

<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>类可以编程方式使用，也可以应用于提供设计器的 VSPackage。

类的实例 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 用于修改设计图面上创建的组件的元数据。 例如，可以将对象使用的默认属性浏览器替换为 <xref:System.Windows.Forms.CommonDialog> 自定义属性浏览器。

<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>应用到 VSPackage 的实现的实例提供的修改 <xref:Microsoft.VisualStudio.Shell.Package> 可以具有以下两个范围之一：

- 全局--对于给定组件的所有新实例

- Local--仅与在当前 VSPackage 提供的设计图面上创建的组件的实例相关。

`IsGlobal` <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 应用到 VSPackage 的实现的实例的属性 <xref:Microsoft.VisualStudio.Shell.Package> 决定了此范围。

将特性应用到的实现 <xref:Microsoft.VisualStudio.Shell.Package> ，并将 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> 对象的属性 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> 设置为 `true` ，如下所示，更改整个 Visual Studio 环境的浏览器：

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

如果全局标志设置为，则 `false` 元数据更改将在当前 VSPackage 支持的当前设计器的本地：

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> 设计图面仅支持创建组件，因此，仅组件可以有本地元数据。 在上面的示例中，我们尝试修改属性，如 `Color` 对象的属性。 如果 `false` 为 global 标志传入了，则 `CustomBrowser` 永远不会出现，因为设计器实际上不会创建的实例 `Color` 。 将全局标志设置为 `false` 对于组件（如控件、计时器和对话框）很有用。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [扩展设计时支持](/previous-versions/37899azc(v=vs.140))