---
title: 使用 MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c199df38f2cd51307861462af49f58996fe84fe4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722161"
---
# <a name="using-msbuild"></a>使用 MSBuild
MSBuild 提供定义完善的可扩展 XML 格式，用于创建完全描述要生成的项目项、生成任务和生成配置的项目文件。

## <a name="general-msbuild-considerations"></a>一般 MSBuild 注意事项
 MSBuild 项目文件（例如 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] .csproj 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] .vbproj 文件）包含生成时使用的数据，但也可以包含在设计时使用的数据。 生成时数据使用 MSBuild 基元进行存储，包括[Item 元素（msbuild）](../../msbuild/item-element-msbuild.md)和[Property 元素（msbuild）](../../msbuild/property-element-msbuild.md)。 设计时数据是特定于项目类型和任何相关项目子类型的数据，以其保留的任意格式存储。

 MSBuild 不具有配置对象的本机支持，但提供了用于指定特定于配置的数据的条件属性。 例如:

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 有关条件特性的详细信息，请参阅[条件构造](../../msbuild/msbuild-conditional-constructs.md)。

### <a name="extending-msbuild-for-your-project-type"></a>扩展项目类型的 MSBuild
 MSBuild 接口和 Api 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的将来版本中可能会有所更改。 因此，使用托管包框架（MPF）类是明智的，因为它们提供了更改的防护。

 项目的托管包框架（MPFProj）提供用于创建和管理新项目系统的帮助程序类。 可以在适用于项目的 MPF 上查找源代码和编译说明[-Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)。

 特定于项目的 MPF 类如下所示：

|实例|实现|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement` 类是 MSBuild 项的包装。

#### <a name="single-file-generators-vs-msbuild-tasks"></a>单个文件生成器与 MSBuild 任务
 单个文件生成器只能在设计时进行访问，但 MSBuild 任务可在设计时和生成时使用。 因此，为了最大限度地提高灵活性，请使用 MSBuild 任务来转换和生成代码。 有关详细信息，请参阅[自定义工具](../../extensibility/internals/custom-tools.md)。

## <a name="see-also"></a>请参阅
- [MSBuild 参考](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [自定义工具](../../extensibility/internals/custom-tools.md)