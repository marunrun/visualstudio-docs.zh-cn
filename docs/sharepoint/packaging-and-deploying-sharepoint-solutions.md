---
title: 打包和部署 SharePoint 解决方案 | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015590"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>打包和部署 SharePoint 解决方案
  通常，使用解决方案包 (.wsp) 文件将 SharePoint 解决方案部署到 SharePoint 服务器。 可以使用 Visual Studio 将 SharePoint 项目项组织为功能，并创建包来部署 SharePoint 功能。

 本主题提供了下列信息：

- [创建功能和包](#create-features-and-packages)

- [功能和打包工具支持](#feature-and-packaging-tool-support)

- [部署 SharePoint 解决方案](#deploy-sharepoint-solutions)

- [在 SharePoint 解决方案中部署文件](#deploy-files-in-sharepoint-solutions)

## <a name="create-features-and-packages"></a>创建功能和包
 可以使用 Visual Studio 将相关 SharePoint 元素组合为功能。 例如，联系人列表定义功能可能包括列表实例和列表定义。 出于部署目的，可以将这两个元素合并为单个功能。 有关功能的详细信息，请参阅[构建基块：功能](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14))。

 接下来，可以创建 SharePoint 解决方案包 (.wsp)，将多个功能、站点定义、程序集和其他文件捆绑到单个包中，这些包以 SharePoint 所需的格式存储文件，以便将文件部署到服务器。 有关详细信息，请参阅[构建基块：解决方案](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14))。

## <a name="feature-and-packaging-tool-support"></a>功能和打包工具支持
 可以使用 Visual Studio 中的 SharePoint 开发工具快速将 SharePoint 文件组织为功能和解决方案包，以便更轻松地部署。 可以使用以下工具配置功能和解决方案包。

- 功能设计器和包设计器。

- 打包资源管理器（一个工具窗口）。

- 解决方案资源管理器。

### <a name="feature-designer-and-package-designer"></a>功能设计器和包设计器
 可以使用功能设计器创建功能、设置作用域并将其他功能标记为依赖项。 设计器还显示描述每个功能的最终 XML 文件。 有关详细信息，请参阅[创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)。

 通过在功能设计器中设置功能的作用域，可将功能应用于特定网站或网站组。 如果针对单个网站激活了某项功能，则该功能仅适用于该特定网站。 如果针对某个网站集激活了某项功能，则该功能中的项适用于整个网站集。 有关详细信息，请参阅[元素的作用域](/previous-versions/office/developer/sharepoint-2010/ms476615(v=office.14))。

 如果你的功能依赖于其他功能，则可以在发布功能之前先设置功能激活依赖项，以标记依赖功能。 功能激活依赖项可检查依赖功能是否已在该作用域激活。 有关详细信息，请参阅[激活依赖项和作用域](/previous-versions/office/developer/sharepoint-2010/aa543162(v=office.14))。

 在包设计器中，可以将 SharePoint 元素组合为单个解决方案包，并配置是否在部署期间重置 Web 服务器。 要设置部署服务器类型，请使用“属性”窗口。 设计器还会生成描述包内容的 XML 文件。 有关详细信息，请参阅[创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)。

 在部署期间，将停止 Internet 信息服务 (IIS) 服务，以便将解决方案文件复制到 SharePoint 服务器。 通过使用 Visual Studio 中的包设计器，可以选择是否应重启 Web 服务器。 要配置是将解决方案部署到前端 Web 服务器还是应用程序服务器，请使用“属性”窗口。 有关详细信息，请参阅[解决方案元素（解决方案）](/previous-versions/office/developer/sharepoint-2010/ms412929(v=office.14))。

### <a name="packaging-explorer"></a>打包资源管理器
 要补充功能设计器和包设计器，可以使用打包资源管理器将 SharePoint 文件组合为功能和包。 此外，还可以查看包、功能、SharePoint 项目项和文件的层次结构视图。 打包资源管理器是可用于完成以下任务的工具窗口：

- 打开 SharePoint 项目项和文件。

- 将 SharePoint 项目项从一个功能拖放到另一个功能。

- 将 SharePoint 项目项和功能从一个包拖放到另一个包。

- 向包添加新功能。

- 打开功能或包设计器。

- 验证功能和包。

  Visual Studio 中的 SharePoint 开发工具包含验证规则，可帮助确保解决方案包的格式正确。 此外，这些规则还可验证能否在 SharePoint 服务器上成功部署和激活 .wsp 解决方案文件。 有关功能的 XML 架构的详细信息，请参阅[功能架构](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))。

  可以向 SharePoint 项目系统添加自定义功能和包验证规则。 有关详细信息，请参阅[如何：为 SharePoint 解决方案创建自定义功能和包验证规则](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)。

  有关打包资源管理器的详细信息，请参阅[如何：使用打包资源管理器在包中添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)。

### <a name="solution-explorer"></a>解决方案资源管理器
 可以使用解决方案资源管理器导航和打开 SharePoint 项目的文件。 使用解决方案资源管理器中的上下文菜单添加功能、功能事件接收器和功能资源。 此外，还可以打开功能设计器和包设计器来配置用于部署的功能和包。

## <a name="deploy-sharepoint-solutions"></a>部署 SharePoint 解决方案
 在 Visual Studio 中自定义功能和包后，可以创建要部署到 SharePoint 服务器的 .wsp 文件。 可以在开发计算机上使用 Visual Studio 来调试和测试仅位于 SharePoint 服务器上的 .wsp。 有关如何将 SharePoint 解决方案部署到远程 SharePoint Server 的详细信息，请参阅[部署解决方案](/previous-versions/office/developer/sharepoint-2010/aa544500(v=office.14))。

 还可以在开发计算机上自定义部署步骤。 有关详细信息，请参阅[部署、发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)。

## <a name="deploy-files-in-sharepoint-solutions"></a>在 SharePoint 解决方案中部署文件
 在将 SharePoint 项目项添加到 SharePoint 解决方案时，项目项通常包含所有必需的文件。 可编译的文件（代码文件）内置于解决方案的输出程序集中。 但是，还必须将不可编译的文件（例如 .xml、.txt 或资源文件）添加到 SharePoint 项目 。 这些文件不会自动打包到解决方案中。 要确保打包这些文件，请将它们添加到映射文件夹或 SharePoint 项目项。

 部署解决方案时，添加到映射文件夹的文件可自动复制到 SharePoint 配置单元。 添加到 SharePoint 项目项的文件将部署到每个文件的“部署位置”属性中指定的位置，该位置部分基于“部署类型”属性进行设置 。 默认情况下，“部署类型”属性值为“NoDeployment”，这意味着该文件未与解决方案一起部署 。 必须为属性设置另一个值，才能在包中包含该文件。

 例如，要将 .xml 文件添加到 SharePoint 项目，请执行以下操作之一：

- 将 SharePoint“布局”映射文件夹添加到项目。 这会在“解决方案资源管理器”中创建一个名为“布局”的文件夹，该文件夹中包含项目的一个子文件 。 将 .xml 文件添加到新的子文件夹。 默认情况下，该文件将部署到 SharePoint 文件系统的 ..\TEMPLATE\LAYOUTS\\\<Folder Name> 下。 有关如何添加映射文件夹的信息，请参阅[如何：添加和删除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

- 将 .xml 文件添加到 SharePoint 项目项的文件夹，然后将 .xml 文件的“部署类型”属性从“NoDeployment”更改为其他设置，例如“RootFile”或“ElementFile”  。 适当的“部署类型”设置取决于文件和项目。 有关“部署类型”属性设置的详细信息，请参阅[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)。

  如果添加的文件不适用于解决方案中的任何特定项目，可以将空 SharePoint 项目添加到解决方案，然后向其中添加其他文件。 将文件部署到 SharePoint（尤其是内容数据库）的另一种替代方法是向项目添加模块，然后将文件添加到模块。 有关详细信息，请参阅[使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
