---
title: 打包和部署 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
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
ms.openlocfilehash: 9a4bf3394cf47b4f355fbe6a330ff5374e2da1c9
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015590"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>打包和部署 SharePoint 解决方案
  通常，SharePoint 解决方案通过使用解决方案包（.wsp）文件部署到 SharePoint 服务器。 可以使用 Visual Studio 将 SharePoint 项目项组织到功能中，并创建包来部署 SharePoint 功能。

 本主题提供了下列信息：

- [创建功能和包](#create-features-and-packages)

- [功能和打包工具支持](#feature-and-packaging-tool-support)

- [部署 SharePoint 解决方案](#deploy-sharepoint-solutions)

- [在 SharePoint 解决方案中部署文件](#deploy-files-in-sharepoint-solutions)

## <a name="create-features-and-packages"></a>创建功能和包
 可以使用 Visual Studio 将相关 SharePoint 元素分组到一个*功能*中。 例如，联系人列表定义的一项功能可能包括列表实例和列表定义。 出于部署目的，可以将这两个元素合并为单个功能。 有关功能的详细信息，请参阅[构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))。

 接下来，你可以创建一个 SharePoint 解决方案包（*.wsp*），以将多个功能、站点定义、程序集和其他文件捆绑到一个包中，该包以 SharePoint 将文件部署到服务器所需的格式存储这些文件。 有关详细信息，请参阅 "[构建基块：解决方案](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))"。

## <a name="feature-and-packaging-tool-support"></a>功能和打包工具支持
 您可以使用 Visual Studio 中的 SharePoint 开发工具快速将 SharePoint 文件组织到功能和解决方案包中，以便于部署。 你可以使用以下工具配置功能和解决方案包。

- 功能设计器和包设计器。

- 打包资源管理器，一个工具窗口。

- 解决方案资源管理器。

### <a name="feature-designer-and-package-designer"></a>功能设计器和包设计器
 您可以使用功能设计器来创建功能，设置作用域，并将其他功能标记为依赖项。 设计器还会显示描述每个功能的最终 XML 文件。 有关详细信息，请参阅[创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)。

 通过在功能设计器中设置其*范围*，将功能应用到特定网站或网站组。 如果为单个网站激活了某项功能，该功能仅适用于该特定网站。 如果为网站集激活了某个功能，该功能中的项将应用于整个网站集。 有关详细信息，请参阅[元素范围](/previous-versions/office/developer/sharepoint-2010/ms476615(v=office.14))。

 如果你的功能依赖于其他功能，则可以设置一个*功能激活依赖项*，以便在功能可用之前标记依赖功能。 功能激活依赖项检查依赖功能是否已在该范围内激活。 有关详细信息，请参阅[激活依赖项和作用域](/previous-versions/office/developer/sharepoint-2010/aa543162(v=office.14))。

 在包设计器中，可以将 SharePoint 元素分组到单个解决方案包中，并配置是否在部署过程中重置 Web 服务器。 若要设置部署服务器类型，请使用 "**属性**" 窗口。 设计器还生成 XML 文件，用于描述包内容。 有关详细信息，请参阅[创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)。

 在部署期间，Internet Information Services （IIS）服务将停止，以将解决方案文件复制到 SharePoint 服务器。 通过使用 Visual Studio 中的包设计器，你可以选择是否应重新启动 Web 服务器。 若要配置是否将解决方案部署到前端 Web 服务器或应用程序服务器，请使用 "**属性**" 窗口。 有关详细信息，请参阅[解决方案元素（解决方案）](/previous-versions/office/developer/sharepoint-2010/ms412929(v=office.14))。

### <a name="packaging-explorer"></a>打包资源管理器
 若要补充功能设计器和包设计器，可以使用 "打包资源管理器" 将 SharePoint 文件分组为功能和包。 此外，你还可以看到包、功能、SharePoint 项目项和文件的层次结构视图。 打包资源管理器是可用于完成以下任务的工具窗口：

- 打开 SharePoint 项目项和文件。

- 将 SharePoint 项目项从一项功能拖放到另一个功能。

- 将 SharePoint 项目项和功能从一个包拖放到另一个包中。

- 向包中添加新功能。

- 打开功能或包设计器。

- 验证功能和包。

  Visual Studio 中的 SharePoint 开发工具具有验证规则，以帮助确保解决方案包格式正确。 此外，这些规则验证 *.wsp*解决方案文件是否可以在 SharePoint 服务器上成功部署和激活。 有关功能的 XML 架构的详细信息，请参阅[功能架构](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))。

  您可以将自定义功能和包验证规则添加到 SharePoint 项目系统。 有关详细信息，请参阅[如何：为 SharePoint 解决方案创建自定义功能和包验证规则](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)。

  有关 "打包资源管理器" 的详细信息，请参阅[如何：使用打包资源管理器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

### <a name="solution-explorer"></a>“解决方案资源管理器”
 您可以使用解决方案资源管理器导航并打开 SharePoint 项目的文件。 使用解决方案资源管理器中的上下文菜单来添加功能、功能事件接收器和功能资源。 此外，还可以打开功能设计器和包设计器来配置部署的功能和包。

## <a name="deploy-sharepoint-solutions"></a>部署 SharePoint 解决方案
 在 Visual Studio 中自定义功能和包后，你可以创建用于部署到 SharePoint 服务器的 *.wsp*文件。 可以使用 Visual Studio 调试和测试。*wsp*仅用于开发计算机上的 SharePoint 服务器。 有关如何将 SharePoint 解决方案部署到远程 SharePoint 服务器的详细信息，请参阅[部署解决方案](/previous-versions/office/developer/sharepoint-2010/aa544500(v=office.14))。

 你还可以在开发计算机上自定义部署步骤。 有关详细信息，请参阅[部署、发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)。

## <a name="deploy-files-in-sharepoint-solutions"></a>在 SharePoint 解决方案中部署文件
 通常，将 SharePoint 项目项添加到 SharePoint 解决方案时，将包括所有所需的文件。 可以编译的文件（代码文件）内置于解决方案的输出程序集。 但是，你可能还必须将不可编译的文件（如 *.xml*、 *.txt*或资源文件）添加到 SharePoint 项目中。 这些文件不会自动打包到你的解决方案中。 若要确保它们已打包，请将文件添加到映射文件夹或 SharePoint 项目项。

 部署解决方案时，添加到映射文件夹的文件会自动复制到 SharePoint 配置单元。 添加到 SharePoint 项目项的文件将部署到在每个文件的 "**部署位置**" 属性中指定的位置，该位置是根据 "**部署类型**" 属性部分设置的。 默认情况下，**部署类型**属性值为**NoDeployment**，这意味着该文件不随解决方案一起部署。 您必须为属性设置另一个值才能在包中包含该文件。

 例如，若要将 *.xml*文件添加到 SharePoint 项目，请执行以下操作之一：

- 将 SharePoint "布局" 映射文件夹添加到项目。 这将在**解决方案资源管理器**中创建一个名为 "**布局**" 的文件夹，其中包含项目的子文件夹。 将 *.xml*文件添加到新的子文件夹。 默认情况下，该文件将部署到下的 SharePoint 文件系统*中。\\\TEMPLATE\LAYOUTS \<Folder Name> *。 有关如何添加映射文件夹的信息，请参阅[如何：添加和删除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

- 将 *.xml*文件添加到 SharePoint 项目项的文件夹，然后将 *.xml*文件的 "**部署类型**" 属性从 " **NoDeployment** " 更改为其他设置，例如**RootFile**或**ElementFile**。 适当的**部署类型**设置取决于文件和项目。 有关**部署类型**属性设置的详细信息，请参阅[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。

  如果添加的文件不适用于解决方案中的任何特定项目，则可以向解决方案中添加一个空 SharePoint 项目，然后向其添加其他文件。 将文件部署到 SharePoint 的另一种方法是将文件添加到项目，然后将文件添加到该模块。 有关详细信息，请参阅[使用模块在解决方案中包含文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
