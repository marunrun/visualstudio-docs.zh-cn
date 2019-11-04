---
title: SharePoint 项目和项目项模板 |Microsoft Docs
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
ms.openlocfilehash: 825e985820ac7a4d72bf321133491e312adb0a0e
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981952"
---
# <a name="sharepoint-project-and-project-item-templates"></a>SharePoint 项目和项目项模板
  以下各节描述了可用的 SharePoint 项目和项目项模板以及如何使用它们。

## <a name="project-and-project-item-templates-overview"></a>项目和项目项模板概述
 在 Visual Studio 中创建新的 SharePoint 项目时，SharePoint 项目将与该项目类型所需的所有项目项一起添加到解决方案中。 例如，如果创建 Silverlight Web 部件项目，则 Visual Studio 将创建一个解决方案，该解决方案包含一个可视 Web 部件项目项和一个 Silverlight 应用程序项目项以及这些项目项所需的所有文件。 项目项模板用于将项目项添加到现有 SharePoint 项目，如添加事件接收器、网站列或列表。

 有关 SharePoint 基础知识的信息，请参阅[Sharepoint Foundation 构建基块](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))。 高级用户可以创建自定义项目和项目项模板。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

## <a name="project-templates"></a>项目模板
 下面是 SharePoint 项目模板的列表。 若要在 visual Studio 中查看 SharePoint 项目模板，请在 "**新建项目**" 对话框中，展开 "**视觉对象C#**  " 或 " **Visual Basic**" 下的 " **sharepoint** " 节点，然后选择 " **2010**"。

### <a name="sharepoint-2010-project"></a>SharePoint 2010 项目
 *Sharepoint 2010 项目*的内容包括在每个 sharepoint 项目模板中。 SharePoint 2010 项目包含：

- 项目文件。

- 项目属性页。

- 一个 "**引用**" 文件夹，其中列出了项目中的所有程序集引用。

- 一个包含*功能*配置文件的**功能**文件夹，用于将功能部署到 SharePoint server。

- 一个**包**文件夹，其中包含用于将解决方案部署到 SharePoint 的包文件 *。*

- 使用强名称为程序集签名的密钥 .snk （强名称密钥）文件，用于增强安全性。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 Silverlight web 部件
 使用*sharepoint 2010 Silverlight Web 部件*项目，可以创建显示 Silverlight 应用程序的 sharepoint Web 部件。 创建此项目时，可以指定是向其添加新的 Silverlight 应用程序还是引用现有的 Silverlight 应用程序。 有关详细信息，请参阅[创建 SharePoint web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和 [演练：创建显示 OData for SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)的 Silverlight web 部件。

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 可视 web 部件
 *SharePoint 2010 可视 Web 部件*项目包括*元素 .xml*定义文件、 **Web 部件**项和**用户控件**项。 您可以通过将控件从 Visual Studio "工具箱" 拖放到用户控件的表面上来设计可视 web 部件的外观。 有关详细信息，请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) 和 [构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="import-sharepoint-2010-solution-package"></a>导入 SharePoint 2010 解决方案包
 *导入 SharePoint 2010 解决方案包*项目允许将现有 sharepoint 2010 网站的全部或部分导入到 Visual Studio 中，并将其导出到 sharepoint 解决方案（ *.wsp*）文件。 导入到 Visual Studio 后，可以自定义其项并对其进行重新部署。 有关详细信息，请参阅[从现有 SharePoint 站点导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

### <a name="import-reusable-sharepoint-2010-workflow"></a>导入可重用的 SharePoint 2010 工作流
 *导入可重用的 SharePoint 2010 工作流*项目允许您将在 SharePoint Designer 2010 中创建的可重用的声明性工作流导入到 Visual Studio。 工作流从 SharePoint 站点导出为 *.wsp*文件。 导入到 Visual Studio 后，可以对其进行自定义、向其添加代码，然后将其部署到 SharePoint 站点。 有关详细信息，请参见[演练：将 SharePoint Designer 可重用工作流导入 Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)。

## <a name="project-item-templates"></a>项目项模板
 下面是 SharePoint 项目项模板的列表。 项目项模板将文件添加到 SharePoint 解决方案以支持 SharePoint 功能，如网站列、列表和内容类型。 例如，将网站列添加到解决方案中将添加一个包含*元素 .xml*定义文件的网站列项目。 添加可视 web 部件会将可视 web 部件项目添加到解决方案中，其中包含*元素 .xml*文件、用户控件项和可视 web 部件项。

 若要查看 SharePoint 项目项模板，请在**解决方案资源管理器**中打开 sharepoint 项目的快捷菜单，然后选择 "**添加**"、"**新建项**"。 展开 "**视觉对象C#**  " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010**"。

### <a name="application-page-farm-solution-only"></a>应用程序页（仅场解决方案）
 **应用程序页（仅场解决方案）** 项可用于设计 SharePoint 站点的 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 网页。 应用程序页只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[如何：](../sharepoint/how-to-create-an-application-page.md) 和[应用程序 _Layouts 页面类型](/previous-versions/office/aa979604(v=office.14))创建应用程序页。

### <a name="business-data-connectivity-model-farm-solution-only"></a>业务数据连接模型（仅场解决方案）
 "**业务数据连接模型（仅场解决方案）** " 项可用于将业务数据集成到 SharePoint 中。 业务数据可以来自后端服务器应用程序，如 [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]、Siebel 和服务广告协议（SAP）。 业务数据连接模型只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[如何：](../sharepoint/how-to-create-a-bdc-model.md)创建 BDC 模型，[如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)，并 [新增内容：Business Connectivity Services](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))。

### <a name="content-type"></a>内容类型
 *内容类型*项使你可以基于现有（基本）内容类型（如文档、公告或任务）创建自定义内容类型。 自定义内容类型提供与基内容类型相同的属性和字段以及您定义的任何站点列（字段）。 例如，你可以创建一个基于 SharePoint 中的基本联系人内容类型的自定义联系人内容类型。 您可以通过更改现有网站列或将更多的网站列添加到已包含在基内容类型中的网站列来自定义内容类型。

> [!NOTE]
> 由于存在 SharePoint 限制，因此无法基于沙盒解决方案内容类型创建场解决方案内容类型。

 有关详细信息，请参见[演练：为 SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) 和 [构建基块创建网站列、内容类型和列表：内容类型](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))。

### <a name="empty-element"></a>空元素
 *空元素*通常用于定义在 Visual Studio 中缺少项目或项目项模板的 SharePoint 项目项。 将空元素添加到项目中时，将创建一个名为 EmptyElement [x] （其中 [x] 为唯一编号\) 的节点。 EmptyElement [x] 包含一个名为 "*元素 .xml* " 的文件。 使用 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 语句在*元素 .xml*中定义所需元素。

### <a name="event-receiver"></a>事件接收器
 *事件接收器*处理 SharePoint 站点中的项的事件，例如，在将项添加到列表时、在删除 web 项或工作流启动时。 事件接收器项目项模板允许处理

- 列出事件

- 列出项事件

- 列出电子邮件事件

- Web 事件

- 列出工作流事件

  事件接收器项目项使用单个类文件创建一个**事件接收器**文件夹，其中包含你在**SharePoint 自定义向导**中创建项目时指定的所有事件的事件处理程序。 当添加、更新、删除或删除项目（例如文件、字段、项、列表、附件、web 部件和工作流）时，事件接收器类可以处理 SharePoint 站点上发生的事件。 有关详细信息，请参阅[如何：](../sharepoint/how-to-create-an-event-receiver.md) 和 [构建基块创建事件接收器：事件处理](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))。

### <a name="list"></a>列表
 列表是可重用的基本 SharePoint 列表定义的实例，如日历或任务列表。 将列表添加到解决方案后，可通过列表设计器将网站列添加到列表中，并创建自定义列表列。 这包括内容类型中的网站列。 您可以指定列表的视图，该*视图*确定将出现在列表中的列。 有关详细信息，请参见[演练：为 SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) 和 [构建基块创建网站列、内容类型和列表：列表和文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))。

### <a name="module"></a>模块
 *模块*（不要与 [!include[vbprvb](../sharepoint/includes/vbprvb-md.md)] 模块混淆）包含要部署到 SharePoint 服务器的任何文件，例如图像或注释。 模块项目项包含**module**节点。 Module 节点包含两个项目项模板：一个 XML 定义文件，它充当模块的清单，一个*示例 .txt*文件是一个占位符文件。 有关详细信息，请参阅[使用模块在解决方案](../sharepoint/using-modules-to-include-files-in-the-solution.md)和[模块](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))中包含文件。

### <a name="sequential-workflow-farm-solution-only"></a>顺序工作流（仅场解决方案）
 *顺序工作流*是一系列按顺序执行的业务逻辑步骤，直到完成最后一个步骤。 顺序工作流用于管理涉及 SharePoint 项（如列表和文档）的进程。 你可以创建站点级（全局）工作流或列表级别（本地）工作流，并且可以选择工作流是自动启动还是手动启动。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建 sharepoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)、 [sharepoint Server 2010 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))和 [新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="silverlight-web-part"></a>Silverlight web 部件
 使用*silverlight web 部件*项目项可以创建用于显示 Silverlight 应用程序的 SharePoint web 部件。 将此项目项添加到解决方案中时，可以选择是添加新的 Silverlight 应用程序还是稍后引用现有的 Silverlight 应用程序。 有关详细信息，请参阅[创建 SharePoint web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和 [演练：创建显示 OData for SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)的 Silverlight web 部件。

### <a name="site-column"></a>网站列
 *网站列*也称为*字段*，是可添加到 SharePoint 项目中的最基本的元素之一。 网站列代表一种类型的数据，例如电话号码、文本注释或联系人列表中联系人的城市名称。 有关详细信息，请参阅[创建网站栏、内容类型和 SharePoint](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)和[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))列表。

### <a name="site-definition-farm-solution-only"></a>网站定义（仅场解决方案）
 *网站定义*项目项包含包含以下文件的站点定义文件夹：

- Default.aspx 页，用作站点的默认网页。

- 定义站点组件的*onet.xml*文件。

- 一个 webtemp xml 文件，该文件指定在 "**新建 SharePoint 网站**" 页的 "**模板选择**" 部分中显示的站点定义配置。

  添加站点定义后，添加代码和文件以引入功能。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅为 SharePoint 和[站点定义和配置](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))[创建站点定义](../sharepoint/creating-site-definitions-for-sharepoint.md)。

### <a name="state-machine-workflow-farm-solution-only"></a>状态机工作流（仅场解决方案）
 *状态机工作流*是一组业务逻辑状态、转换和操作。 不按顺序执行状态机工作流中的步骤;相反，它们由操作和状态触发。 与顺序工作流一样，状态机工作流与 SharePoint 项（如列表和文档）相关联。 同样，您可以创建站点级（全局）工作流或列表级别（本地）工作流。 你还可以选择工作流是自动启动还是手动启动。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建 sharepoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)、 [sharepoint Server 2010 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))和 [新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="user-control-farm-solution-only"></a>用户控件（仅场解决方案）
 *用户控件*是一个自定义的可重用控件，可以将其他 ASP.NET 控件和 SharePoint 控件添加到该控件。 用户控件可以添加到在 SharePoint 中运行的应用程序页和 web 部件。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅为[Web 部件或应用程序页创建可重用控件](/visualstudio/sharepoint/creating-reusable-controls-for-web-parts-or-application-pages&view=vs-2019)。

### <a name="visual-web-part"></a>可视 web 部件
 *可视 web 部件*项目项包括*元素 .xml*定义文件、 **Web 部件**项和**用户控件**项。 您可以通过将控件从 Visual Studio "工具箱" 拖放到用户控件的表面上来设计可视 web 部件的外观。 有关详细信息，请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) 和 [构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="web-part"></a>Web 部件
 *Web 部件*是在一种称为 Web 部件页的特殊类型的页中运行的服务器端控件。 它们是显示在 SharePoint 站点上的页面的构建基块。 Web 部件项提供的文件可用于设计 SharePoint 站点的 web 部件。 有关详细信息，请参阅[如何：](../sharepoint/how-to-create-a-sharepoint-web-part.md) 和 [构建基块创建 SharePoint web 部件：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint 产品和技术](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))
