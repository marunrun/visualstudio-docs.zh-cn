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
ms.openlocfilehash: f53083c49504146aca545da73bd38950493efcd8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63429208"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>SharePoint 支持的 MsBuild 属性
  任何[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]Microsoft.VisualStudio.SharePoint.targets 文件、 项目文件或项目用户文件中定义的属性可在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 项目。 除了常见[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]由项目中，SharePoint 提供的属性定义是特定于 SharePoint 项目的其他属性。

 有关一系列常见[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]属性，请参阅[常用的 MSBuild 项目属性](http://go.microsoft.com/fwlink/?LinkID=168687)。 对于您的编程语言支持的属性的完整列表，请查看 *.targets*文件，将项目文件 (*.csproj*或 *.vbproj*)，或项目用户文件 （*csproj.user*或 *。 vbproj.user*)。

## <a name="msbuild-properties-specific-to-sharepoint"></a>特定于 SharePoint 的 MsBuild 属性
 下表列出[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]仅适用于 SharePoint 项目中的属性[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 其他属性存在，但它们仅供内部使用。

|属性名|描述|
|-------------------|-----------------|
|SharePointSiteUrl|一个字符串，表示[!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]到 SharePoint 站点。|
|SandboxedSolution|一个布尔值，该值指示解决方案是否为沙盒解决方案。|
|ActiveDeploymentConfiguration|活动部署配置。|
|IncludeAssemblyInPackage|一个布尔值，该值指示是否在包文件中包含程序集。|
|PreDeploymentCommand|一个字符串值，该值表示在预先部署命令步骤中执行的命令。|
|PostDeploymentCommand|一个字符串值，该值表示要在后期部署命令步骤中执行的命令。|
|CustomBeforeSharePointTargets|一个字符串，表示的路径[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]目标文件。 如果目标文件存在并且定义，它是之前导入任何 SharePoint 目标数据。 此属性允许你自定义的预定义打包相关的属性，而无需修改已发布的 SharePoint 目标文件，包过程，但仍然适用于所有 SharePoint 项目的目标文件。|
|CustomAfterSharePointTargets|一个字符串，表示的路径[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]目标文件。 如果目标文件存在，并且定义，则导入所有的 SharePoint 目标数据。 此属性，可以通过重写了与打包相关的属性和目标，而无需修改已发布的 SharePoint 目标文件，自定义包过程，但仍然适用于所有 SharePoint 项目的目标文件。|
|LayoutPath|一个字符串，表示每个要打包的文件的临时存放添加到之前的根目录 *.wsp*文件。 此路径可以是有助于了解当您重写 BeforeLayout 和 AfterLayout 目标，以添加、 删除或修改文件打包，因为可以使用它来更改的内容 *.wsp*文件。|
|BasePackagePath|一个字符串，表示在其中放置包的文件夹。 此值将使用项目，例如 Bin\Debug 输出的目录。|
|PackageExtension|一个字符串，表示要追加到包的文件扩展名。 默认值为 wsp。|
|AssemblyDeploymentTarget|一个字符串，表示项目程序集在 SharePoint 服务器的部署位置的位置。 其值为 GlobalAssemblyCache （默认值） 或 web 应用程序。 此外可以在属性窗口中设置此属性。|
|PackageWithValidation|一个布尔值，该值指定是否在打包之前执行验证。 此属性允许您在生成包时忽略验证错误。|
|ValidatePackageDependsOn|一个字符串，定义要 ValidatePackage 目标之前执行的其他目标。|
|TokenReplacementFileExensions|一个字符串，定义在打包过程替换为其标记的文件。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>在属性页中使用 MsBuild 属性
 对于大的灵活性，而不是使用硬编码的字符串中**预先部署命令行**并**后期部署命令行**框在 SharePoint 属性页上，可以使用 SharePoint作为自变量的属性。 例如，而不是指定一个特定[!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]字符串的 SharePoint 站点，则可以使用`$(SharePointSiteUrl)`。

> [!NOTE]
> 你可以使用[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]的变量语法`$(` *propertyName* `)`或环境变量语法`%` *propertyName* `%`若要指定的属性。

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)