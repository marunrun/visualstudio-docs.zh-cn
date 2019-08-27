---
title: 可替换参数 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, tokens
- tokens [SharePoint development in Visual Studio]
- replaceable parameters [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, replaceable parameters
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload: office
ms.openlocfilehash: 165ef1256a0150e0942d85c4f876c8b3f5e15c72
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422919"
---
# <a name="replaceable-parameters"></a>可替换参数
  可替换参数，或*令牌*，可以使用项目文件中为其实际值不在设计时已知的 SharePoint 解决方案项提供值。 它们类似于标准[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]模板标记。 有关详细信息，请参阅[模板参数](../ide/template-parameters.md)。

## <a name="token-format"></a>令牌格式
 令牌开始，以美元符号 （$） 字符结尾。 有关部署、 使用的任何令牌替换为实际值时为项目打包到 SharePoint 解决方案包 (*.wsp*文件)。 例如，令牌 **$SharePoint.Package.Name$** 可能解析为字符串"测试 SharePoint 包"。

## <a name="token-rules"></a>令牌的规则
 以下规则适用于标记：

- 可以在行中任意位置指定令牌。

- 令牌不能跨多个行。

- 在同一行上和在同一文件中，可能会多次指定相同的令牌。

- 可能在同一行上指定不同的令牌。

  令牌不遵循这些规则将被忽略，不会导致出现警告或错误。

  清单转换之后立即执行替换的字符串值的标记。 这种替换允许用户编辑与令牌的清单模板。

### <a name="token-name-resolution"></a>令牌名称解析
 在大多数情况下，标记会解析为无论其中包含特定值。 但是，如果令牌与包或功能，令牌的值依赖于包含它。 例如，如果一个功能是中包，则令牌`$SharePoint.Package.Name$`解析为值"包 a。" 如果相同的功能是中包 B，然后`$SharePoint.Package.Name$`解析为"包 b。"

## <a name="tokens-list"></a>标记列表
 下表列出了可用的标记。

|名称|描述|
|----------|-----------------|
|$SharePoint.Project.FileName$|名称包含的项目文件，如*NewProj.csproj*。|
|$SharePoint.Project.FileNameWithoutExtension$|包含不带文件扩展名的项目文件的名称。 例如，"NewProj"。|
|$SharePoint.Project.AssemblyFullName$|包含项目的显示名称 （强名称） 的输出程序集。|
|$SharePoint.Project.AssemblyFileName$|包含项目的名称的输出程序集。|
|$SharePoint.Project.AssemblyFileNameWithoutExtension$|包含项目的名称的输出程序集，不带文件扩展名。|
|$SharePoint.Project.AssemblyPublicKeyToken$|包含项目的公钥标记的输出程序集，转换为字符串。 ("x2"中的 16 字符十六进制格式。)|
|$SharePoint.Package.Name$|包含包的名称。|
|$SharePoint.Package.FileName$|包含包定义文件的名称。|
|$SharePoint.Package.FileNameWithoutExtension$|包含包定义文件的名称 （不带扩展名）。|
|$SharePoint.Package.Id$|包含包的 SharePoint ID。 如果多个包中使用一项功能，则将更改此值。|
|$SharePoint.Feature.FileName$|包含它的定义文件的名称功能，如*Feature1.feature*。|
|$SharePoint.Feature.FileNameWithoutExtension$|功能定义文件中，不带文件扩展名的名称。|
|$SharePoint.Feature.DeploymentPath$|包含在包中的功能文件夹的名称。 此令牌将等于功能设计器中的"部署路径"属性。 一个示例值是"Project1_Feature1"。|
|$SharePoint.Feature.Id$|包含功能的 SharePoint ID。 此令牌，因为与所有功能级别令牌，可以使用仅由一项功能，通过包中包含的文件不直接添加到一项功能之外的包。|
|$SharePoint.ProjectItem.Name$|作为从中获取项目项 （不文件名称） 的名称**ISharePointProjectItem.Name**。|
|$SharePoint.Type.\<GUID>.AssemblyQualifiedName$|与标记的 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 匹配的类型的程序集限定名。 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 的格式为小写，并与 Guid.ToString("D") 格式（即 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx）对应。|
|$SharePoint.Type.\<GUID>.FullName$|在令牌中的 GUID 匹配的类型的全名。 GUID 的格式为小写，并对应于 Guid.ToString("D") 格式 (即，xxxxxxxx xxxx-xxxx-xxxx-在左右加上)。|

## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>将扩展添加到标记替换文件扩展名列表
 虽然从理论上由属于 SharePoint 项目项包含在包中，默认情况下，任何文件使用令牌[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]令牌仅在包文件中，清单文件，并具有以下扩展名的文件中搜索：

- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]

- ASCX

- ASPX

- Web 部件

- DWP

  这些扩展定义的`<TokenReplacementFileExtensions>`Microsoft.VisualStudio.SharePoint.targets 文件中的元素位于...\\< 程序文件\>\MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools 文件夹。

  但是，可以向列表添加其他文件扩展名。 添加`<TokenReplacementFileExtensions>`之前定义到任何 SharePoint 项目文件中的 PropertyGroup 元素\<导入 > SharePoint 目标文件。

> [!NOTE]
> 编译项目后发生令牌替换，因为您不应将进行编译，如的文件类型的文件扩展名添加 *.cs*， *.vb*或 *.resx*。 仅在未编译的文件中替换标记。

 例如，若要添加的文件扩展名 (*.myextension*并 *.yourextension*) 到的标记替换文件扩展名的列表中，你会将以下代码添加到项目 (*.csproj*) 文件：

```xml
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
.
.
.
    <!-- Define the following property to add your extension to the list of token replacement file extensions.  -->
<TokenReplacementFileExtensions>myextension;yourextension</TokenReplacementFileExtensions>
</PropertyGroup>
```

 您可以直接向目标添加扩展 (*.targets*) 文件。 但是，添加该扩展会改变打包在本地系统上的所有 SharePoint 项目扩展列表，而不仅仅是自己。 当您在系统上的唯一开发人员，或者您的大多数项目需要它，此扩展可能会方便。 但是，因为它是特定于系统的这种方法不是可移植的因此，建议您添加的任何扩展到项目文件相反。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
