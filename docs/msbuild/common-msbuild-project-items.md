---
title: 常用的 MSBuild 项目项 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, common project items
ms.assetid: 1eba3721-cc12-4b80-9987-84923ede5e2e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b10768d5ab291981dc77af650de61eb9496dfda5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596146"
---
# <a name="common-msbuild-project-items"></a>常用的 MSBuild 项目项
在 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 中，项是对一个或多个文件的命名引用。 项包含元数据（如文件名、路径和版本号）。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的所有项目类型具有几个通用项。 在文件 Microsoft.Build.CommonTypes.xsd 中定义了这些项  。

## <a name="common-items"></a>常用项
 以下是所有通用项目项的列表。

### <a name="reference"></a>参考
 表示项目中的程序集（托管）引用。

|项元数据名称|描述|
|---------------|-----------------|
|HintPath|可选的字符串。 程序集的相对或绝对路径。|
|“属性”|可选的字符串。 程序集的显示名称，例如“System.Windows.Forms”。|
|FusionName|可选的字符串。 指定项的简单或强合成名称。<br /><br /> 此特性存在时，可以节省时间，因为程序集文件不必打开即可获取合成名称。|
|SpecificVersion|可选的布尔值。 指定是否应仅引用合成名称中的版本。|
|别名|可选的字符串。 引用的任何别名。|
|Private|可选的布尔值。 指定是否应将引用复制到输出文件夹。 此特性与 Visual Studio IDE 中的引用的“复制本地”  属性相匹配。|

### <a name="comreference"></a>COMReference
 表示项目中的 COM（非托管）组件引用。 此项仅适用于 .NET 项目。

|项元数据名称|描述|
|---------------|-----------------|
|“属性”|可选的字符串。 组件的显示名称。|
|GUID|必选字符串。 组件的 GUID，形式为 {12345678-1234-1234-1234-1234567891234}。|
|VersionMajor|必选字符串。 组件版本号的主要部分。 例如，如果完整版本号是“5.46”，则显示“5”。|
|VersionMinor|必选字符串。 组件版本号的次要部分。 例如，如果完整版本号是“5.46”，则显示“46”。|
|LCID|可选的字符串。 组件的 LocaleID。|
|WrapperTool|可选的字符串。 对组件使用的包装工具的名称，例如“tlbimp”。|
|Isolated|可选的布尔值。 指定组件是否为免注册组件。|

### <a name="comfilereference"></a>COMFileReference
 表示传递到 [ResolveComReference](resolvecomreference-task.md) 目标的 `TypeLibFiles` 参数的类型库的列表。 此项仅适用于 .NET 项目。

|项元数据名称|描述|
|---------------|-----------------|
|WrapperTool|可选的字符串。 对组件使用的包装工具的名称，例如“tlbimp”。|

### <a name="nativereference"></a>NativeReference
 表示本机清单文件或对此类文件的引用。

|项元数据名称|描述|
|---------------|-----------------|
|“属性”|必选字符串。 清单文件基名称。|
|HintPath|必选字符串。 清单文件的相对路径。|

### <a name="projectreference"></a>ProjectReference
 表示对另一个项目的引用。

|项元数据名称|描述|
|---------------|-----------------|
|“属性”|可选的字符串。 引用的显示名称。|
|项目|可选的字符串。 引用的 GUID，形式为 {12345678-1234-1234-1234-1234567891234}。|
|Package|可选的字符串。 所引用的项目文件的路径。|
|ReferenceOutputAssembly|可选的布尔值。 如果设置为 `false`，则不包括引用项目的输出作为此项目的[引用](#reference)，但仍可确保在此项目之前生成其他项目。 默认为 `true`。|

### <a name="compile"></a>Compile
 表示编译器的源文件。

| 项元数据名称 | 描述 |
|-----------------------| - |
| DependentUpon | 可选的字符串。 指定该文件正确编译所依赖的文件。 |
| AutoGen | 可选的布尔值。 指示是否已由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 集成开发环境 (IDE) 为项目生成了文件。 |
| 链接 | 可选的字符串。 文件在物理上处于项目文件的影响范围之外时要显示的符号路径。 |
| 可见 | 可选的布尔值。 指示是否要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的“解决方案资源管理器”  中显示文件。 |
| CopyToOutputDirectory | 可选的字符串。 确定是否将文件复制到输出目录。 值为：<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |

### <a name="embeddedresource"></a>EmbeddedResource
 表示要在生成的程序集中嵌入的资源。

| 项元数据名称 | 描述 |
|-----------------------| - |
| DependentUpon | 可选的字符串。 指定该文件正确编译所依赖的文件 |
| Generator | 必选字符串。 在此项上运行的任何文件生成器的名称。 |
| LastGenOutput | 必选字符串。 在此项上运行的任何文件生成器创建的文件的名称。 |
| CustomToolNamespace | 必选字符串。 在此项上运行的任何文件生成器应在其中创建代码的命名空间。 |
| 链接 | 可选的字符串。 如果文件在物理上处于项目的影响范围之外，则显示符号路径。 |
| 可见 | 可选的布尔值。 指示是否要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的“解决方案资源管理器”  中显示文件。 |
| CopyToOutputDirectory | 可选的字符串。 确定是否将文件复制到输出目录。 值为：<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |
| LogicalName | 必选字符串。 嵌入资源的逻辑名称。 |

### <a name="content"></a>内容
 表示不会编译到项目中，但可能会嵌入到其中或随其一起发布的文件。

| 项元数据名称 | 描述 |
|-----------------------| - |
| DependentUpon | 可选的字符串。 指定该文件正确编译所依赖的文件。 |
| Generator | 必选字符串。 在此项上运行的任何文件生成器的名称。 |
| LastGenOutput | 必选字符串。 在此项上运行的任何文件生成器创建的文件的名称。 |
| CustomToolNamespace | 必选字符串。 在此项上运行的任何文件生成器应在其中创建代码的命名空间。 |
| 链接 | 可选的字符串。 文件在物理上处于项目的影响范围之外时要显示的符号路径。 |
| PublishState | 必选字符串。 内容的发布状态，为以下任一项：<br /><br /> -   默认<br />-   已包括<br />-   已排除<br />-   数据文件<br />-   必备组件 |
| IsAssembly | 可选的布尔值。 指定文件是否为程序集。 |
| 可见 | 可选的布尔值。 指示是否要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的“解决方案资源管理器”  中显示文件。 |
| CopyToOutputDirectory | 可选的字符串。 确定是否将文件复制到输出目录。 值为：<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |

### <a name="none"></a>None
 表示不应在生成过程中具有角色的文件。

| 项元数据名称 | 描述 |
|-----------------------| - |
| DependentUpon | 可选的字符串。 指定该文件正确编译所依赖的文件。 |
| Generator | 必选字符串。 在此项上运行的任何文件生成器的名称。 |
| LastGenOutput | 必选字符串。 在此项上运行的任何文件生成器创建的文件的名称。 |
| CustomToolNamespace | 必选字符串。 在此项上运行的任何文件生成器应在其中创建代码的命名空间。 |
| 链接 | 可选的字符串。 文件在物理上处于项目的影响范围之外时要显示的符号路径。 |
| 可见 | 可选的布尔值。 指示是否要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的“解决方案资源管理器”  中显示文件。 |
| CopyToOutputDirectory | 可选的字符串。 确定是否将文件复制到输出目录。 值为：<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |

### <a name="assemblymetadata"></a>AssemblyMetadata
 表示要生成为 `[AssemblyMetadata(key, value)]` 的程序集特性。

| 项元数据名称 | 描述 |
|-----------------------| - |
| 包括 | 成为 `AssemblyMetadataAttribute` 特性构造函数中的第一个参数（键）。 |
| “值” | 必选字符串。 成为 `AssemblyMetadataAttribute` 特性构造函数中的第二个参数（值）。 |

> [!NOTE]
> 这仅适用于使用 .NET Core SDK 的项目。

### <a name="baseapplicationmanifest"></a>BaseApplicationManifest
 表示用于生成的基本应用程序清单，包含 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署安全信息。

### <a name="codeanalysisimport"></a>CodeAnalysisImport
 表示要导入的 FxCop 项目。

### <a name="import"></a>导入
 表示应由 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编译器导入其命名空间的程序集。

## <a name="see-also"></a>请参阅
- [常用的 MSBuild 项目属性](../msbuild/common-msbuild-project-properties.md)
