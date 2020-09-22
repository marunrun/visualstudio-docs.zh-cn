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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840726"
---
# <a name="replaceable-parameters"></a>可替换参数
  可替换参数（或 *标记*）可用于项目文件中，以提供在设计时实际值未知的 SharePoint 解决方案项的值。 它们在功能上类似于标准 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 模板标记。 有关详细信息，请参阅 [模板参数](../ide/template-parameters.md)。

## <a name="token-format"></a>令牌格式
 标记以美元符号 ($) 字符开始和结束。 部署时，如果项目打包到 SharePoint 解决方案包 (*.wsp* 文件) 中，则使用实际值替换任何使用的标记。 例如，令牌 **$SharePoint Package.Name $** 可能解析为字符串 "Test SharePoint Package"。

## <a name="token-rules"></a>标记规则
 以下规则适用于标记：

- 可以在行中的任意位置指定令牌。

- 令牌不能跨多个行。

- 同一标记可以在同一行和同一文件中指定多次。

- 可以在同一行中指定不同的令牌。

  不遵循这些规则的标记将被忽略，并且不会导致警告或错误。

  在清单转换后立即用字符串值替换标记。 此替换功能允许用户用标记编辑清单模板。

### <a name="token-name-resolution"></a>令牌名称解析
 在大多数情况下，令牌解析为特定值，而不考虑它的包含位置。 但是，如果令牌与包或功能相关，则令牌的值将取决于它的包含位置。 例如，如果某个功能在包 A 中，则该标记 `$SharePoint.Package.Name$` 解析为 "包 a" 值。 如果同一功能在包 B 中，则 `$SharePoint.Package.Name$` 解析为 "包 b"。

## <a name="tokens-list"></a>标记列表
 下表列出了可用标记。

|名称|说明|
|----------|-----------------|
|$SharePoint. FileName $|包含项目文件的名称，如 *NewProj*。|
|$SharePoint FileNameWithoutExtension $|不包含文件扩展名的包含项目文件的名称。 例如 "NewProj"。|
|$SharePoint AssemblyFullName $|包含项目的输出程序集的显示名称 (强名称) 。|
|$SharePoint p $|包含项目的输出程序集的名称。|
|$SharePoint AssemblyFileNameWithoutExtension $|包含项目的输出程序集的名称，没有文件扩展名。|
|$SharePoint AssemblyPublicKeyToken $|包含项目的输出程序集的公钥标记，已转换为字符串。  ("x2" 十六进制格式的16个字符。 ) |
|$SharePoint. Package.Name $|包含包的名称。|
|$SharePoint. FileName $|包含包的定义文件的名称。|
|$SharePoint FileNameWithoutExtension $|不包含包定义文件的扩展名)  (名称。|
|$SharePoint. Package.Id $|包含包的 SharePoint ID。 如果在多个包中使用某一功能，则此值将更改。|
|$SharePoint. FileName $|包含功能的定义文件的名称，如 *Feature1*。|
|$SharePoint FileNameWithoutExtension $|功能定义文件的名称，没有文件扩展名。|
|$SharePoint DeploymentPath $|包中包含功能的文件夹的名称。 此标记等同于功能设计器中的 "部署路径" 属性。 示例值为 "Project1_Feature1"。|
|$SharePoint. Feature.Id $|包含功能的 SharePoint ID。 与所有功能级令牌一样，此令牌只能由包中包含的文件使用，而不会直接添加到功能外部的包中。|
|$SharePoint. ProjectItem.Name $|项目项的名称不 (其文件名) ，从 **ISharePointProjectItem.Name**获取。|
|$SharePoint \<GUID> . 类型。AssemblyQualifiedName $|与标记的 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 匹配的类型的程序集限定名。 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 的格式为小写，并与 Guid.ToString("D") 格式（即 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx）对应。|
|$SharePoint \<GUID> . 类型。FullName $|与令牌中的 GUID 匹配的类型的完整名称。 GUID 的格式为小写，并对应于 Guid.empty ( "D" ) 格式 (也就是说，xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) 为 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx。|

## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>向标记替换文件扩展名列表添加扩展
 尽管任何属于包中包含的 SharePoint 项目项的文件都可以使用理论，但默认情况下， [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 仅在包文件、清单文件和具有以下扩展名的文件中搜索标记：

- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]

- ASCX

- DEFAULT.ASPX

- 图片

- REPORTVIEWER.DWP

  这些扩展由 `<TokenReplacementFileExtensions>` VisualStudio 文件中的元素定义，该元素位于 ... \\<program files \> \MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools 文件夹中。

  但是，您可以向列表中添加其他文件扩展名。 向 `<TokenReplacementFileExtensions>` sharepoint 项目文件中的任何 PropertyGroup 添加一个元素，该元素在 \<Import> sharepoint 目标文件的之前定义。

> [!NOTE]
> 因为标记替换在项目编译后发生，所以不应为编译的文件类型（如 *.cs*、 *.vb* 或 *.resx*）添加文件扩展名。 标记仅替换为未编译的文件。

 例如，若要将文件 *扩展名 (和* *Yourextension*) 添加到令牌替换文件扩展名的列表中，请将以下内容添加到项目 (*.csproj*) 文件中：

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

 可以将扩展添加 *到 (目标*) 文件中。 但是，添加扩展会改变在本地系统上打包的所有 SharePoint 项目的扩展列表，而不只是您自己的扩展列表。 如果你是系统上的唯一开发人员，或者你的大多数项目需要它，则此扩展可能很方便。 但是，因为它是特定于系统的，所以此方法是不可移植的，因此建议您改为将任何扩展添加到项目文件。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
