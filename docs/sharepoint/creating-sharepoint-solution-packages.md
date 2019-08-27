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
ms.openlocfilehash: 8f7afee863d36796bb481f9aca2c24a9ba891ae7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62952713"
---
# <a name="create-sharepoint-solution-packages"></a>创建 SharePoint 解决方案包
  通过使用包设计器，可以创建和自定义部署包。 例如，可以添加 SharePoint 项目项和功能，重置 IIS 服务器、 设置功能激活作用域，并识别功能依赖关系。 在设计器还会生成一个清单，描述每个包的 XML 文件。

## <a name="packaging-tools"></a>打包工具
 可以使用**包设计器**以自定义的包，并生成清单。 可以包括多个 SharePoint 项目项、 配置是否应重置，请在 Web 服务器，并将其设置部署服务器类型。 有关详细信息，请参阅[如何：添加和删除使用包设计器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

 或者，可以使用**打包资源管理器**若要修改的功能和包文件中的项 (*.wsp*)。 有关详细信息，请参阅[如何：添加和删除使用打包资源管理器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

 可以使用 Visual Studio 和 MSBuild 创建包 (*.wsp*) 要部署 SharePoint 解决方案的文件。 此过程会生成所需的 SharePoint 部署清单文件。 有关详细信息，请参阅[如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)。

## <a name="package-designer-options"></a>包设计器选项
 下表显示的属性可以自定义中使用的 SharePoint 包**包设计器**。

|包设计器属性|默认设置的说明|
|-------------------------------|------------------------------------|
|名称|必需。 包的默认名称设置为*ProjectName*。|
|重置 web 服务器|可选。 如果你想要重新启动 Web 服务器后的，请选择 *.wsp*文件安装在 SharePoint 服务器上。|
|部署服务器类型|必需。 默认情况下，作用域设置为应用程序服务器。<br /><br /> ApplicationServer:描述承载服务的服务器。<br /><br /> WebFrontEnd:描述承载网站的服务器。|
|解决方案中的项|所有 SharePoint 项目项和可以添加到包的功能。|
|包中的项|可选。 所有 SharePoint 项目和想要部署包中的功能。|

## <a name="configure-the-packaging-process"></a>配置在打包过程
 开发 Visual Studio 中的 SharePoint 解决方案后，你可以自定义项目的打包。

 下表显示了两个可用于自定义的 MSBuild 目标如何 *.wsp*创建文件。

|Target|描述|
|------------|-----------------|
|BeforeLayout|文件被复制到中间目录前立即执行任务的目标。 可以在创建包文件之前修改文件 (*.wsp*)。|
|AfterLayout|将文件复制到中间目录后立即执行任务的目标。|

 有关详细信息，[如何：使用 MSBuild 目标自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)。

## <a name="packaging-architecture"></a>打包体系结构
 创建 SharePoint 包时将执行以下步骤 (*.wsp*) 在 Visual Studio 中。

1. 功能和包进行验证以确保包的物理和语义结构正确。

2. 枚举功能、 项目项和包中的包文件。 为包和功能清单文件进行转换以包含部署和激活的所有必要信息。 令牌替换为完全限定的值。

3. 执行可自定义 BeforeLayout MSBuild 目标。 可以创建此步骤以使对之前的包进行任何自定义修改 *.wsp*创建文件。

4. 枚举的文件复制到中间目录。

5. 执行可自定义 AfterLayout MSBuild 目标。 可以创建此步骤以使对之前的包进行任何自定义修改 *.wsp*创建文件。

6. 中间目录中的文件添加到 *.wsp*文件。

## <a name="package-folder-structure"></a>包文件夹结构
 当您打包您的 SharePoint 项目时 *.wsp*为你在创建文件*SolutionFolder\bin\\\<BuildConfiguration >* 文件夹。 例如，如果您的解决方案是在*C:\Visual Studio 2013\Projects\ListDefinition1*和生成配置设置为版本中， *.wsp*文件位于*C:\Visual Studio 2013\Projects\ListDefinition1\bin\Release*。

## <a name="see-also"></a>请参阅
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：添加和删除使用包设计器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
- [如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [如何：使用 MSBuild 任务创建 SharePoint 解决方案包](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [如何：使用 MSBuild 目标自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)
