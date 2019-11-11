---
title: SharePoint 支持的 MSBuild 属性 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, MSBuild properties
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5470160c6b0af1af39238a14319ad497e1541a43
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985163"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>SharePoint 支持的 MsBuild 属性
  VisualStudio 文件、项目文件或项目用户文件中定义的任何 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性都可用于 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 项目。 除了项目提供的通用 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性，SharePoint 还定义了特定于 SharePoint 项目的其他属性。

 有关常见 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性的列表，请参阅[常见的 MSBuild 项目属性](/previous-versions/dotnet/netframework-4.0/bb629394(v=vs.100))。 有关编程语言支持的属性的完整列表，请查看 *.targets*文件、项目文件（ *.csproj*或 *.vbproj*）或项目用户文件（ *.csproj. user* ， *.vbproj*）。

## <a name="msbuild-properties-specific-to-sharepoint"></a>特定于 SharePoint 的 MsBuild 属性
 下表列出了特定于 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中的 SharePoint 项目的 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性。 存在其他属性，但它们供内部使用。

|属性名|描述|
|-------------------|-----------------|
|SharePointSiteUrl|一个字符串，表示 SharePoint 站点的 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]。|
|SandboxedSolution|指示解决方案是否为沙盒解决方案的布尔值。|
|ActiveDeploymentConfiguration|活动部署配置。|
|IncludeAssemblyInPackage|指示程序集是否包含在包文件中的布尔值。|
|PreDeploymentCommand|一个字符串值，该值表示要在预先部署命令步骤中执行的命令。|
|PostDeploymentCommand|一个字符串值，该值表示要在后期部署命令步骤中执行的命令。|
|CustomBeforeSharePointTargets|表示 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 目标文件的路径的字符串。 如果目标文件存在并且已定义，则在任何 SharePoint 目标数据之前将其导入。 此属性使你可以通过预定义与打包相关的属性来自定义包过程，而无需修改已发布的 SharePoint 目标文件，但目标文件仍适用于所有 SharePoint 项目。|
|CustomAfterSharePointTargets|表示 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 目标文件的路径的字符串。 如果目标文件存在并且已定义，则在所有 SharePoint 目标数据之后导入它。 此属性可让你通过以下方式自定义包进程：重写与包装相关的属性和目标，而无需修改已发布的 SharePoint 目标文件，但目标文件仍适用于所有 SharePoint 项目。|
|LayoutPath|一个字符串，表示在将每个要打包的文件添加到 *.wsp*文件之前，要将其打包的根目录。 当你重写 BeforeLayout 和 AfterLayout 目标以便添加、删除或修改要打包的文件时，可以使用此路径来了解，因为你可以使用它来更改 *.wsp*文件的内容。|
|BasePackagePath|一个字符串，表示在其中放置包的文件夹。 此值使用项目的输出目录，例如 Bin\debug。|
|PackageExtension|一个字符串，表示要追加到包的文件扩展名。 默认值为 wsp。|
|AssemblyDeploymentTarget|一个字符串，该字符串表示在 SharePoint 服务器上部署项目程序集的位置。 其值为 GlobalAssemblyCache （默认值）或 WebApplication。 还可以在属性窗口中设置此属性。|
|PackageWithValidation|一个布尔值，指定在打包之前是否执行验证。 此属性可让你在生成包时忽略验证错误。|
|ValidatePackageDependsOn|一个字符串，定义要在 ValidatePackage 目标之前执行的其他目标。|
|TokenReplacementFileExensions|一个字符串，用于定义打包期间替换其标记的文件。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>在 "属性" 页中使用 MsBuild 属性
 出于灵活性，你可以使用 SharePoint 属性作为参数，而不是在 SharePoint "属性" 页上的 "**预先部署命令行**" 和 "**后期部署命令行**" 框中使用硬编码的字符串。 例如，可以改为使用 `$(SharePointSiteUrl)`，而不是为 SharePoint 站点指定特定的 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 字符串。

> [!NOTE]
> 您可以使用 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 变量语法 `$(`*propertyname*`)` 或环境变量语法 `%`*propertyname*`%` 来指定属性。

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)