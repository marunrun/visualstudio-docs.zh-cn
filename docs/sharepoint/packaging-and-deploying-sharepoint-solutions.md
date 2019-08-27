---
title: 打包和部署 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- packaging [SharePoint development in Visual Studio]
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, packaging and deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c187865518c9556d63d9e5e632ec5c658fc3e0f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953499"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>打包和部署 SharePoint 解决方案
  通常情况下，SharePoint 解决方案部署到 SharePoint 服务器通过使用解决方案包 (.wsp) 文件。 若要将你的 SharePoint 项目项组织到功能并创建要部署您的 SharePoint 功能的程序包，可以使用 Visual Studio。

 本主题提供以下信息：

- [创建功能和包](#create-features-and-packages)

- [功能和打包工具支持](#feature-and-packaging-tool-support)

- [部署 SharePoint 解决方案](#deploy-sharepoint-solutions)

- [部署 SharePoint 解决方案中的文件](#deploy-files-in-sharepoint-solutions)

## <a name="create-features-and-packages"></a>创建功能和包
 可以使用 Visual Studio 到相关的 SharePoint 元素进行分组*功能*。 例如，联系人列表定义的功能可能包括列表实例和列表定义。 可以将这两个元素合并到单个功能以进行部署。 有关功能的详细信息，请参阅[构建基块：功能](http://go.microsoft.com/fwlink/?LinkID=169183)。

 接下来，可以创建 SharePoint 解决方案包 (*.wsp*) 将捆绑的多个功能，站点定义、 程序集和其他文件到一个包，它将文件存储在 SharePoint 部署的文件所需的格式在服务器中。 有关详细信息，请参阅[构建基块：解决方案](http://go.microsoft.com/fwlink/?LinkID=169186)。

## <a name="feature-and-packaging-tool-support"></a>功能和打包工具支持
 可以使用 Visual Studio 中的 SharePoint 开发工具来快速将 SharePoint 文件组织到功能和更轻松地部署的解决方案包。 可以使用以下工具来配置功能和解决方案包。

- 功能设计器和包设计器。

- 打包资源管理器，工具窗口。

- 解决方案资源管理器。

### <a name="feature-designer-and-package-designer"></a>功能设计器和包设计器
 可以创建功能、 设置作用域，并使用功能设计器将其他功能标记为依赖项。 在设计器还显示最终的 XML 文件，描述每个功能。 有关详细信息，请参阅[创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)。

 通过设置应用到特定网站或网站的组的功能及其*作用域*功能设计器中。 如果单个网站激活某个功能，该功能将仅适用于该特定的 Web 站点。 如果为站点集合激活一项功能，则该功能中的项应用于整个站点集合。 有关详细信息，请参阅[元素范围内](http://go.microsoft.com/fwlink/?LinkID=169189)。

 如果你的功能依赖于其他功能，则可以设置*功能激活依赖项*来发布该功能可用之前标记相关的功能。 功能激活依赖项检查，是否在该作用域已激活相关功能。 有关详细信息，请参阅[激活依赖项和作用域](http://go.microsoft.com/fwlink/?LinkID=169190)。

 在包设计器中，可以 SharePoint 元素分组到单个解决方案包，并配置是否在部署期间重置 Web 服务器。 若要设置部署服务器类型，请使用**属性**窗口。 在设计器还会生成用于描述包内容的 XML 文件。 有关详细信息，请参阅[创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)。

 在部署期间，Internet 信息服务 (IIS) 服务已停止，将解决方案文件复制到 SharePoint 服务器。 通过在 Visual Studio 中使用包设计器，可以选择是否应重新启动 Web 服务器。 若要配置解决方案部署到前端 Web 服务器或应用程序服务器，请使用**属性**窗口。 有关详细信息，请参阅[解决方案元素 （解决方案）](http://go.microsoft.com/fwlink/?LinkID=169191)。

### <a name="packaging-explorer"></a>打包资源管理器
 若要补充的功能设计器和包设计器，可以使用打包资源管理器将 SharePoint 文件分组到功能和包。 此外，请参阅层次结构视图的包，功能，SharePoint 项目项和文件。 打包资源管理器是一个工具窗口，可用于完成以下任务：

- 打开 SharePoint 项目项和文件。

- 拖放的 SharePoint 项目项从一个功能到另一个。

- 拖放到另一个包中的 SharePoint 项目项和功能。

- 向包中添加一项新功能。

- 打开功能或包设计器。

- 验证功能和包。

  在 Visual Studio 中的 SharePoint 开发工具具有验证规则，以帮助确保解决方案包的位置正确。 此外，这些规则确认 *.wsp*可以成功部署和 SharePoint 服务器上激活解决方案文件。 有关功能的 XML 架构的详细信息，请参阅[功能架构](http://go.microsoft.com/fwlink/?LinkID=169192)。

  可以向 SharePoint 项目系统中添加自定义功能和包验证规则。 有关详细信息，请参阅[如何：创建自定义功能和包验证规则为 SharePoint 解决方案](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)。

  有关打包资源管理器的详细信息，请参阅[如何：添加和删除使用打包资源管理器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

### <a name="solution-explorer"></a>“解决方案资源管理器”
 解决方案资源管理器可用于导航，并打开 SharePoint 项目的文件。 在解决方案资源管理器中使用上下文菜单以添加功能，功能事件接收器和功能的资源。 此外，您可以打开功能设计器和包设计器，若要配置的功能和部署的包。

## <a name="deploy-sharepoint-solutions"></a>部署 SharePoint 解决方案
 自定义功能和 Visual Studio 中的包后，可以创建 *.wsp*文件以将部署到 SharePoint 服务器。 您可以使用 Visual Studio 调试和测试。*wsp*仅在开发计算机上的 SharePoint 服务器上。 有关如何将 SharePoint 解决方案部署到远程 SharePoint 服务器的详细信息，请参阅[部署解决方案](http://go.microsoft.com/fwlink/?LinkID=169194)。

 此外可以自定义开发计算机上的部署步骤。 有关详细信息，请参阅[部署、 发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)。

## <a name="deploy-files-in-sharepoint-solutions"></a>部署 SharePoint 解决方案中的文件
 通常情况下，当您将 SharePoint 项目项添加到 SharePoint 解决方案时，所有必需将包含的文件。 可以是文件编译 （文件） 内置到解决方案的输出程序集。 但是，您可能还需要将非编辑文件，例如，添加 *.xml*， *.txt*，或资源文件，向 SharePoint 项目。 这些文件不是自动打包你的解决方案中。 若要确保它们都打包，可以将文件添加到映射的文件夹或 SharePoint 项目项。

 部署解决方案时，添加到映射的文件夹的文件会自动复制到 SharePoint 配置单元。 添加到 SharePoint 项目项文件部署到在指定的位置**部署位置**部分设置每个文件的属性基于**部署类型**属性。 默认情况下**部署类型**属性值是**NoDeployment**，这意味着不随解决方案一起部署该文件。 必须设置属性将该文件包括在包中的另一个值。

 例如，若要添加 *.xml*文件向 SharePoint 项目中，执行以下操作之一：

- 将 SharePoint"布局"映射文件夹添加到你的项目。 这将创建在**解决方案资源管理器**名为的文件夹**布局**具有项目的子文件夹。 添加 *.xml*到新的子文件夹的文件。 默认情况下，该文件将部署到 SharePoint 文件系统下 *...\TEMPLATE\LAYOUTS\\\<文件夹名称 >*。 有关如何添加映射的文件夹的信息，请参阅[如何： 添加和移除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

- 添加 *.xml*的文件权限的 SharePoint 项目项文件夹，然后将更改**部署类型**属性 *.xml*文件从**NoDeployment**到另一个设置如**RootFile**或**ElementFile**。 适当**部署类型**设置取决于文件和项目。 有关详细信息**部署类型**属性设置，请参阅[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。

  如果添加了的文件不适用于解决方案中任何特定项目，可以将一个空 SharePoint 项目添加到你的解决方案并将其他文件添加到它。 有关将文件部署到 SharePoint，尤其是对内容数据库，另一种方法是将模块添加到项目，然后将文件添加到模块。 有关详细信息，请参阅[使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
