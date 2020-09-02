---
title: 创建 SharePoint 解决方案包 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
- packages [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b250be3b61cdfc524f049f952f0cf7e65f1c295a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "74876059"
---
# <a name="create-sharepoint-solution-packages"></a>创建 SharePoint 解决方案包
  使用包设计器，可以创建和自定义部署包。 例如，你可以添加 SharePoint 项目项和功能、重置 IIS 服务器、设置功能激活范围以及标识功能依赖项。 设计器还会生成一个清单，该清单是描述每个包的 XML 文件。

## <a name="packaging-tools"></a>打包工具
 你可以使用 **包设计器** 来自定义包并生成清单。 您可以包括 SharePoint 项目项、配置是否应重置 Web 服务器以及设置部署服务器类型。 有关详细信息，请参阅 [如何：使用包设计器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

 或者，你可以使用 " **打包资源管理器** " 来修改包文件 (*.wsp*) 中的功能和项。 有关详细信息，请参阅 [如何：使用打包资源管理器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

 你可以使用 Visual Studio 和 MSBuild 创建包 (*.wsp*) 文件来部署 SharePoint 解决方案。 此过程将生成 SharePoint 部署所需的清单文件。 有关详细信息，请参阅 [如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。

## <a name="package-designer-options"></a>包设计器选项
 下表显示了可在 SharePoint 包中通过 **包设计器**自定义的属性。

|包设计器属性|默认设置说明|
|-------------------------------|------------------------------------|
|名称|必需。 包的默认名称设置为 " *项目*名称"。|
|重置 Web 服务器|可选。 如果在 SharePoint 服务器上安装 *.wsp* 文件后要重新启动 Web 服务器，请选择 "否"。|
|部署服务器类型|可选。 表示承载包的服务器的类型。 如果未设置，则默认值为 WebFrontEnd。<br /><br /> ApplicationServer：描述承载服务的服务器。<br /><br /> WebFrontEnd：描述承载网站的服务器。|
|解决方案中的项|所有可添加到包中的 SharePoint 项目项和功能。|
|包中的项|可选。 要在包中部署的所有 SharePoint 项和功能。|

## <a name="configure-the-packaging-process"></a>配置打包过程
 在 Visual Studio 中开发 SharePoint 解决方案后，您可以自定义项目的打包方式。

 下表显示了可用于自定义 *.wsp* 文件创建方式的两个 MSBuild 目标。

|目标|描述|
|------------|-----------------|
|BeforeLayout|在文件被复制到中间目录之前立即执行任务的目标。 您可以在创建包文件 (*.wsp*) 之前修改这些文件。|
|AfterLayout|在将文件复制到中间目录之后立即执行任务的目标。|

 有关详细信息，请 [操作方法：使用 MSBuild 目标自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)。

## <a name="packaging-architecture"></a>打包体系结构
 在 Visual Studio 中 *创建 (的* SharePoint 包) 时，会执行以下步骤。

1. 验证功能和包以确保包的物理结构和语义结构正确。

2. 枚举包中的功能、项目项和包文件。 包和功能的清单文件会转换为包含部署和激活所需的所有信息。 标记将替换为完全限定的值。

3. 执行可自定义的 BeforeLayout MSBuild 目标。 你可以创建此步骤，以便在创建 *.wsp* 文件之前对包进行任何自定义修改。

4. 枚举的文件将复制到中间目录。

5. 执行可自定义的 AfterLayout MSBuild 目标。 你可以创建此步骤，以便在创建 *.wsp* 文件之前对包进行任何自定义修改。

6. 将中间目录中的文件添加到 *.wsp* 文件。

## <a name="package-folder-structure"></a>包文件夹结构
 打包 SharePoint 项目时，会在*SolutionFolder\bin \\ \<BuildConfiguration> *文件夹中为你创建一个 *.wsp*文件。 例如，如果你的解决方案位于 *C:\Visual Studio 2013 \ Projects\ListDefinition1* ，而你的生成配置设置为 "发布"，则 *.Wsp* 文件位于 *C:\Visual Studio 2013 \ Projects\ListDefinition1\bin\Release*中。

## <a name="see-also"></a>另请参阅
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
- [如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [如何：使用 MSBuild 目标自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)
