---
title: 共享点项目和项目项目模板 |微软文档
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.FirstWizardPage
- VS.SharePointTools.SPE.ListInstance
- VS.SharePointTools.SPE.ListDefinition
- VS.SharePointTools.SPE.ListDefFromContentType
- VS.SharePointTools.SPE.ContentType
- SPE.Wizard
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, project and project item templates
- SharePoint development in Visual Studio, templates
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2878bd2092e000cf63c2b4fcb531a502a470203e
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649229"
---
# <a name="sharepoint-project-and-project-item-templates"></a>共享点项目和项目项目模板
  以下各节介绍可用的 SharePoint 项目和项目项目模板及其使用方式。

## <a name="project-and-project-item-templates-overview"></a>项目和项目项目模板概述
 在 Visual Studio 中创建新的 SharePoint 项目时，SharePoint 项目将与该项目类型所需的所有项目项一起添加到解决方案中。 例如，如果创建 Silverlight Web 部件项目，Visual Studio 将创建一个解决方案，其中包含 Visual Web 部件项目项和 Silverlight 应用程序项目项以及这些项目项目所需的所有文件。 项目项模板用于将项目项添加到现有 SharePoint 项目，例如添加事件接收方、网站列或列表。

 有关 SharePoint 基础知识的信息，请参阅[SharePoint 基础构建基块](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))。 高级用户可以创建自定义项目和项目项模板。 有关详细信息，请参阅扩展[SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

## <a name="project-templates"></a>项目模板
 以下是 SharePoint 项目模板的列表。 要查看 Visual Studio 中的 SharePoint 项目模板，请在新**项目**对话框中展开**Visual C#** 或 Visual **Basic**下的**SharePoint**节点，然后选择**2010**。

### <a name="sharepoint-2010-project"></a>SharePoint 2010 项目
 *SharePoint 2010 项目*的内容包含在每个 SharePoint 项目模板中。 A SharePoint 2010 项目包含：

- 项目文件。

- 项目属性页。

- 列出项目中所有程序集引用的**引用**文件夹。

- 包含 *.功能*配置文件**的功能**文件夹，用于将功能部署到 SharePoint 服务器。

- 包含*包.包*文件的**包**文件夹，用于将解决方案部署到 SharePoint。

- 用于使用强名称对程序集进行签名的 key.snk（强名键）文件，以提高安全性。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 银光网络部分
 *SharePoint 2010 银光 Web 部件*项目使您能够为 SharePoint 创建显示银光应用程序的 Web 部件。 创建此项目时，可以指定是向它添加新 Silverlight 应用程序还是引用现有应用程序。 有关详细信息，请参阅为[SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)和演练创建 Web 部件[：创建显示共享点的 OData 的银光 Web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 可视化 Web 部件
 *SharePoint 2010 可视化 Web 部件*项目包括*元素.xml*定义文件 **、Web 部件**项和**用户控制**项。 您可以通过将控件从 Visual Studio 工具箱拖动或复制到用户控件的表面来设计可视 Web 部件的外观。 有关详细信息，请参阅[如何：使用设计器](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)和构建基块创建 SharePoint Web[部件：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="import-sharepoint-2010-solution-package"></a>导入 SharePoint 2010 解决方案包
 *导入 SharePoint 2010 解决方案包*项目允许您将现有 SharePoint 2010 站点的全部或部分（导出到 SharePoint 解决方案 *（.wsp*） 文件）导入 Visual Studio。 导入 Visual Studio 后，可以自定义其项目并重新部署它们。 有关详细信息，请参阅[从现有 SharePoint 网站导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

### <a name="import-reusable-sharepoint-2010-workflow"></a>导入可重用的 SharePoint 2010 工作流
 *导入可重用 SharePoint 2010 工作流*项目，允许您将在 SharePoint 设计器 2010 中创建的可重用声明性工作流导入 Visual Studio。 工作流从 SharePoint 站点导出为 *.wsp*文件。 导入 Visual Studio 后，可以对其进行自定义、向其添加代码，然后将其部署到 SharePoint 站点。 有关详细信息，请参阅[演练：将 SharePoint 设计器可重用工作流导入可视化工作室](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)。

## <a name="project-item-templates"></a>项目项目模板
 以下是 SharePoint 项目模板的列表。 项目项目模板将文件添加到 SharePoint 解决方案，以支持 SharePoint 功能（如网站列、列表和内容类型）。 例如，向解决方案添加网站列会添加包含*Elements.xml*定义文件的网站列项目。 添加可视 Web 部件会将可视 Web 部件项目添加到包含*Elements.xml*文件、用户控件项和可视 Web 部件项的解决方案中。

 要查看 SharePoint 项目模板，在**解决方案资源管理器**中，打开 SharePoint 项目的快捷菜单，然后选择 **"添加****""新项目**"。 在**Visual C#** 或**可视化基本**项下展开**SharePoint**节点，然后选择**2010**。

### <a name="application-page-farm-solution-only"></a>应用程序页（仅限服务器场解决方案）
 应用程序**页（仅限服务器场解决方案）** 项目使您能够为 SharePoint[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]网站设计网页。 应用程序页只能在服务器场解决方案中使用。 只能将此项目项添加到服务器场解决方案。 有关详细信息，请参阅[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)和[应用程序_layouts页面类型](/previous-versions/office/aa979604(v=office.14))。

### <a name="business-data-connectivity-model-farm-solution-only"></a>业务数据连接模型（仅限服务器场解决方案）
 **业务数据连接模型（仅限服务器场解决方案）** 项目使您能够将业务数据集成到 SharePoint 中。 业务数据可能来自后端服务器应用程序，如[!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]Siebel 和服务广告协议 （SAP）。 业务数据连接模型只能在服务器场解决方案中使用。 只能将此项目项添加到服务器场解决方案。 有关详细信息，请参阅[：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)，[如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)，以及[新增内容：业务连接服务](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))。

### <a name="content-type"></a>内容类型
 *内容类型*项目允许您基于现有（基本）内容类型（如文档、公告或任务）创建自定义内容类型。 自定义内容类型提供与基本内容类型相同的属性和字段以及定义的任何网站列（字段）。 例如，您可以创建基于 SharePoint 中的基本联系人内容类型的自定义联系人内容类型。 您可以通过更改现有网站列或将更多网站列添加到基本内容类型中已包含的网站列来自定义内容类型。

> [!NOTE]
> 由于 SharePoint 限制，您不能基于沙盒解决方案内容类型创建服务器场解决方案内容类型。

 有关详细信息，请参阅演练：为 SharePoint 和[构建基块：内容类型](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))[创建网站列、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)。

### <a name="empty-element"></a>空元素
 *空元素*最常用于定义 Visual Studio 中缺少项目或项目项模板的 SharePoint 项目项。 向项目添加空元素时，将创建名为 emptyElement_x_（其中 [x] 是唯一编号\)的节点。 空元素[x] 包含名为*Element.xml*的单个文件。 使用[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]语句在*Elements.xml*中定义所需的元素。

### <a name="event-receiver"></a>事件接收器
 *事件接收方*处理 SharePoint 站点中项目的事件，例如将项目添加到列表中时、删除 Web 项时或工作流启动时间。 事件接收器项目项模板允许您处理

- 列出事件

- 列出项目事件

- 列出电子邮件事件

- Web 事件

- 列出工作流事件

  事件接收器项目项创建一个**事件接收器**文件夹，其中包含单个类文件，其中包含您在**SharePoint 自定义向导**中创建项目时指定的所有事件的事件处理程序。 事件接收者类可以处理在添加、更新、删除或删除文件、字段、项目、列表、附件、Web 部件和工作流等项目时在 SharePoint 网站上发生的事件。 有关详细信息，请参阅[如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)和[构建基块：事件处理](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))。

### <a name="list"></a>列出
 列表是可重用的基本 SharePoint 列表定义的实例，如日历或任务列表。 将列表添加到解决方案后，列表设计器使您能够将网站列添加到列表中并创建自定义列表列。 这包括内容类型的网站列。 您可以为列表指定*视图*，该视图确定将显示在列表中的列。 有关详细信息，请参阅演练：为 SharePoint 和[构建基块：列表和文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))[创建网站列、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)。

### <a name="module"></a>模块
 *模块*（不要与[!include[vbprvb](../sharepoint/includes/vbprvb-md.md)]模块混淆）包含要部署到 SharePoint 服务器的任何文件，如图像或注释。 模块项目项包含**模块**节点。 模块节点包含两个项目项模板：一个 XML 定义文件（充当模块的清单）和一个*样板.txt*文件（占位符文件）。 有关详细信息，请参阅[Modules](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))[使用模块在解决方案和模块中包含文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)。

### <a name="sequential-workflow-farm-solution-only"></a>顺序工作流（仅限服务器场解决方案）
 *顺序工作流*是一系列业务逻辑步骤，按顺序执行，直到最后一步完成。 顺序工作流用于管理涉及 SharePoint 项（如列表和文档）的进程。 您可以创建站点级（全局）工作流或列表级（本地）工作流，也可以选择工作流是自动启动还是手动启动。 此项目项只能在服务器场解决方案中使用。 只能将此项目项添加到服务器场解决方案。 有关详细信息，请参阅创建[SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)[、SharePoint 服务器 2010 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))以及[新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="silverlight-web-part"></a>银光网部分
 *Silverlight Web 部件*项目项目项目使您能够为 SharePoint 创建显示银光应用程序的 Web 部件。 将此项目项添加到解决方案时，可以选择是添加新 Silverlight 应用程序还是稍后引用现有应用程序。 有关详细信息，请参阅为[SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)和演练创建 Web 部件[：创建显示共享点的 OData 的银光 Web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="site-column"></a>站点列
 *网站列*（也称为*字段*）是可以添加到 SharePoint 项目的最基本元素之一。 站点列表示数据类型，如电话号码、文本注释或联系人列表中联系人的城市名称。 有关详细信息，请参阅为[SharePoint 和列创建网站列、内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)。 [Columns](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))

### <a name="site-definition-farm-solution-only"></a>站点定义（仅限服务器场解决方案）
 *站点定义*项目项包含一个站点定义文件夹，其中包含以下文件：

- 默认 .aspx 页，用作网站的默认网页。

- 定义站点组件的*onet.xml*文件。

- 一个 Webtemp xml 文件，用于指定在新**SharePoint 网站**页面的 **"模板选择**"部分中显示的站点定义配置。

  添加网站定义后，添加代码和文件以引入功能。 此项目项只能在服务器场解决方案中使用。 只能将此项目项添加到服务器场解决方案。 有关详细信息，请参阅为[SharePoint](../sharepoint/creating-site-definitions-for-sharepoint.md)和[站点定义和配置](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))创建站点定义。

### <a name="state-machine-workflow-farm-solution-only"></a>状态机工作流（仅限服务器场解决方案）
 *状态机工作流*是一组业务逻辑状态、转换和操作。 状态机工作流中的步骤不按顺序执行;因此，这些步骤不会按顺序执行。相反，它们由操作和状态触发。 与顺序工作流一样，状态机工作流与 SharePoint 项（如列表和文档）相关联。 同样，您可以创建站点级（全局）工作流或列表级（本地）工作流。 您还可以选择工作流是自动启动还是手动启动。 此项目项只能在服务器场解决方案中使用。 只能将此项目项添加到服务器场解决方案。 有关详细信息，请参阅创建[SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)[、SharePoint 服务器 2010 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))以及[新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="user-control-farm-solution-only"></a>用户控制（仅限服务器场解决方案）
 *用户控件*是一种自定义的、可重用的控件，您可以将其他ASP.NET控件和 SharePoint 控件添加到其中。 可以将用户控件添加到在 SharePoint 中运行的应用程序页和 Web 部件中。 此项目项只能在服务器场解决方案中使用。 只能将此项目项添加到服务器场解决方案。 有关详细信息，请参阅为[Web 部件或应用程序页创建可重用控件](creating-reusable-controls-for-web-parts-or-application-pages.md)。

### <a name="visual-web-part"></a>可视 Web 部件
 *可视 Web 部件*项目项包括*Elements.xml*定义文件 **、Web 部件**项和**用户控制**项。 您可以通过将控件从 Visual Studio 工具箱拖动或复制到用户控件的表面来设计可视 Web 部件的外观。 有关详细信息，请参阅[如何：使用设计器](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)和构建基块创建 SharePoint Web[部件：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="web-part"></a>Web 部件
 *Web 部件*是服务器端控件，在称为 Web 部件页的特殊类型的页面内运行。 它们是显示在 SharePoint 网站上的页面构建基块。 Web 部件项提供文件，使您能够为 SharePoint 网站设计 Web 部件。 有关详细信息，请参阅[如何：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)和[构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint Products and Technologies](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))
