---
title: 使用 MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f961249ff584f7767dc2505bb20b1fb0961b7dd3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704291"
---
# <a name="using-msbuild"></a>使用 MSBuild
MSBuild 提供了定义良好的可扩展 XML 格式，用于创建项目文件，这些文件完全描述要生成的项目项、生成任务和生成配置。

## <a name="general-msbuild-considerations"></a>一般 MS 构建注意事项
 MSBuild 项目文件（例如[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)].csproj[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]和 .vbproj 文件）包含在生成时使用的数据，但也可能包含在设计时使用的数据。 生成时间数据使用 MSBuild 基元存储，包括[项目元素 （MSBuild）](../../msbuild/item-element-msbuild.md)和[属性元素 （MSBuild）。](../../msbuild/property-element-msbuild.md) 设计时数据（特定于项目类型的数据和任何相关的项目子类型）存储在为其保留的自由格式 XML 中。

 MSBuild 对配置对象没有本机支持，但确实提供了用于指定特定于配置的数据的条件属性。 例如：

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 有关条件属性的详细信息，请参阅[条件构造](../../msbuild/msbuild-conditional-constructs.md)。

### <a name="extending-msbuild-for-your-project-type"></a>扩展项目类型的 MSBuild
 MSBuild 接口和 API 可能会在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的未来版本中更改 。 因此，谨慎使用托管包框架 （MPF） 类，因为它们提供屏蔽，使其免受更改。

 项目管理包框架 （MPFProj） 提供用于创建和管理新项目系统的帮助程序类。 您可以在[项目 MPF - Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)找到源代码和编译说明。

 特定于项目的 MPF 类如下所示：

|类|实现|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement`类是 MSBuild 项的包装器。

#### <a name="single-file-generators-vs-msbuild-tasks"></a>单个文件生成器与 MS 构建任务
 单个文件生成器仅在设计时访问，但 MSBuild 任务可以在设计时间和生成时使用。 因此，为了获得最佳灵活性，请使用 MSBuild 任务来转换和生成代码。 有关详细信息，请参阅[自定义工具](../../extensibility/internals/custom-tools.md)。

## <a name="see-also"></a>请参阅
- [MSBuild 参考](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [自定义工具](../../extensibility/internals/custom-tools.md)
