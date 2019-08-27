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
ms.openlocfilehash: 245a6c994d87ecfa9c5ef877563b70100e5eef6f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438999"
---
# <a name="sharepoint-project-and-project-item-templates"></a>SharePoint 项目和项目项模板
  以下各节描述了可用的 SharePoint 项目和项目项模板以及如何使用它们。

## <a name="project-and-project-item-templates-overview"></a>项目和项目项模板概述
 当在 Visual Studio 中创建新的 SharePoint 项目时，SharePoint 项目添加到与该项目类型所需的项目项的所有解决方案。 例如，如果创建 Silverlight Web 部件项目时，Visual Studio 将创建包含可视 Web 部件项目项和 Silverlight 应用程序的项目项，以及所需的这些项目项的所有文件的解决方案。 项目项模板用于将项目项添加到现有的 SharePoint 项目，例如添加事件接收器、 站点列或列表。

 有关 SharePoint 基本原理的信息，请参阅[SharePoint Foundation 构建基块](http://go.microsoft.com/fwlink/?LinkId=179404)。 高级的用户可以创建自定义项目和项目项模板。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

## <a name="project-templates"></a>项目模板
 下面是 SharePoint 项目模板的列表。 若要查看 Visual Studio 中的 SharePoint 项目模板中**新的项目**对话框框中，展开**SharePoint**下**Visual C#** 或**Visual Basic**，然后选择**2010年**。

### <a name="sharepoint-2010-project"></a>SharePoint 2010 项目
 内容*SharePoint 2010 项目*都包括在每个 SharePoint 项目模板。 SharePoint 2010 项目包含：

- 项目文件。

- 项目属性页。

- 一个**引用**其中列出了所有项目中的程序集引用的文件夹。

- 一个**功能**所在的文件夹 *.feature*用于将功能部署到 SharePoint 服务器的配置文件。

- 一个**包**所在的文件夹*Package.package*用来将解决方案部署到 SharePoint 的文件。

- Key.snk （强名称密钥） 文件，用于使用强名称程序集签名的增强的安全性。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 Silverlight web 部件
 *SharePoint 2010 Silverlight Web 部件*项目使你创建的 web 部件的 SharePoint 显示 Silverlight 应用程序。 创建此项目时，可以指定是否要添加到该新的 Silverlight 应用程序或引用一个现有。 有关详细信息，请参阅[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和[演练：创建显示 SharePoint OData 的 Silverlight web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 可视 web 部件
 一个*SharePoint 2010 可视 Web 部件*项目包括*Elements.xml*定义文件**Web 部件**项，和一个**用户控件**项. 您可以通过拖动或从 Visual Studio 工具箱将控件复制到用户控件的图面设计 visual web 部件的外观。 有关详细信息，请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)和[构建基块：Web 部件](http://go.microsoft.com/fwlink/?LinkId=179438)。

### <a name="import-sharepoint-2010-solution-package"></a>导入 SharePoint 2010 解决方案包
 *导入 SharePoint 2010 解决方案包*项目，可以导入现有的 SharePoint 2010 站点，导出到 SharePoint 解决方案的全部或部分 (*.wsp*) 文件，在 Visual Studio。 一旦导入到 Visual Studio，你可以自定义其项并重新部署它们。 有关详细信息，请参阅[从现有的 SharePoint 网站导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

### <a name="import-reusable-sharepoint-2010-workflow"></a>导入可重用 SharePoint 2010 工作流
 *导入可重用 SharePoint 2010 工作流*项目让你导入到 Visual Studio 在 SharePoint Designer 2010 中创建的可重用的声明性工作流。 从与 SharePoint 站点导出工作流 *.wsp*文件。 一旦导入到 Visual Studio，可以进行自定义、 和将代码添加到它，然后将其部署到 SharePoint 站点。 有关详细信息，请参见[演练：SharePoint Designer 可重用工作流导入 Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)。

## <a name="project-item-templates"></a>项目项模板
 下面是 SharePoint 项目项模板的列表。 项目项模板将文件添加到 SharePoint 解决方案以支持 SharePoint 功能，例如网站栏、 列表和内容类型。 例如，将一个站点列添加到你的解决方案添加包含一个站点列项目*Elements.xml*定义文件。 添加可视 web 部件将可视 web 部件项目添加到包含的解决方案*Elements.xml*文件、 用户控件项目和可视 web 部件项。

 若要查看中的 SharePoint 项目项模板**解决方案资源管理器**，打开 SharePoint 项目的快捷菜单，然后选择**添加**，**新项**。 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**。

### <a name="application-page-farm-solution-only"></a>应用程序页上 （仅场解决方案）
 **（仅场解决方案） 的应用程序页上**项，您可以设计[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]的 SharePoint 网站的 web 页。 可以仅在场解决方案中使用的应用程序页。 此项目项仅向场解决方案。 有关详细信息，请参阅[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)并[应用程序 _layouts 的页类型](http://go.microsoft.com/fwlink/?LinkId=179434)。

### <a name="business-data-connectivity-model-farm-solution-only"></a>业务数据连接模型 （仅场解决方案）
 一个**业务数据连接模型 （仅场解决方案）** 项使你可以集成业务数据在 SharePoint 中。 业务数据可以来源于后端服务器应用程序，如[!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]，Siebel 和服务广告协议 (SAP)。 可以仅在场解决方案中使用业务数据连接模型。 此项目项仅向场解决方案。 有关详细信息，请参阅[如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)，[如何：使用资源文件指定本地化的名称、 属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)，和[新增功能：Business Connectivity Services](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))。

### <a name="content-type"></a>内容类型
 *内容类型*项可用于创建基于现有的 （基本） 内容类型，如文档、 公告或任务的自定义内容类型。 自定义内容类型作为基内容类型以及你定义的任何站点列 （字段） 提供相同的属性和字段。 例如，可以创建基于在 SharePoint 中涉及的基本联系人内容类型的自定义联系人内容类型。 您可以通过更改现有的站点列，或将更多的站点列添加到已包含基内容类型中的自定义内容类型。

> [!NOTE]
> 由于 SharePoint 限制，无法创建基于沙盒解决方案内容类型的场解决方案内容类型。

 有关详细信息，请参见[演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)和[构建基块：内容类型](http://go.microsoft.com/fwlink/?LinkId=179413)。

### <a name="empty-element"></a>空元素
 *空元素*通常用于定义缺少项目或项目项模板在 Visual Studio 中的 SharePoint 项目项。 当将空元素添加到你的项目时，节点名为 EmptyElement [x](where [x] is a unique number\) is created. EmptyElement [x] 包含单个文件，它是命名*Elements.xml。* 使用[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]语句来定义在所需的元素*Elements.xml*。

### <a name="event-receiver"></a>事件接收器
 *事件接收器*处理 SharePoint 站点，例如某项添加到列表时，web 项被删除时，或时启动工作流中的项的事件。 事件接收方项目项模板可让你处理

- 列出的事件

- 列表项事件

- 列出的电子邮件事件

- Web 事件

- 列表工作流事件

  事件接收方项目项创建**事件接收器**文件夹中包含的所有事件的事件处理程序创建的项目中时指定一个类文件**SharePoint 自定义项向导**。 事件接收器类可以处理添加、 更新、 删除，或移除项，如文件、 字段、 项、 列表、 附件、 web 部件和工作流时，SharePoint 站点发生的事件。 有关详细信息，请参阅[如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)和[构建基块：事件处理](http://go.microsoft.com/fwlink/?LinkId=179416)。

### <a name="list"></a>列表
 列表是可重用基 SharePoint 列表定义，如日历或任务列表的实例。 将列表添加到你的解决方案之后, 列表设计器，可将站点列添加到列表并创建自定义列表的列。 这包括从内容类型的站点列。 您可以指定*视图*有关列表，用于确定将显示在列表中的列。 有关详细信息，请参见[演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)和[构建基块：列表和文档库](http://go.microsoft.com/fwlink/?LinkId=179421)。

### <a name="module"></a>模块
 *模块*(不要与混淆[!include[vbprvb](../sharepoint/includes/vbprvb-md.md)]模块) 包含你想要部署到 SharePoint 服务器，如图像或说明的任何文件。 模块项目项包含**模块**节点。 在模块节点包含两个项目项模板： XML 定义文件，它充当模块清单，和一个*sample.txt*文件，将占位符文件。 有关详细信息，请参阅[使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)并[模块](http://go.microsoft.com/fwlink/?LinkId=179425)。

### <a name="sequential-workflow-farm-solution-only"></a>顺序工作流 （仅场解决方案）
 一个*顺序工作流*是一系列业务逻辑步骤，直到完成最后一个步骤按顺序执行。 顺序工作流用于管理涉及如列表和文档的 SharePoint 项的进程。 可以创建站点级别 （全局） 工作流或列表级别 （本地） 工作流，并可以选择是否自动或手动启动工作流。 此项目项可仅在场解决方案。 此项目项仅向场解决方案。 有关详细信息，请参阅[创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)， [SharePoint Server 2010 中的工作流](http://go.microsoft.com/fwlink/?LinkId=260555)，和[What's New:工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="silverlight-web-part"></a>Silverlight web 部件
 *Silverlight web 部件*项目项使你创建的 web 部件的 SharePoint 显示 Silverlight 应用程序。 当将此项目项添加到你的解决方案时，可以选择是否要添加新的 Silverlight 应用程序或更高版本引用一个现有。 有关详细信息，请参阅[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和[演练：创建显示 SharePoint OData 的 Silverlight web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="site-column"></a>站点列
 一个*网站栏*，也称为*字段*，是可以添加到 SharePoint 项目的最基本元素之一。 站点列所表示的数据，例如电话号码、 文本注释或联系人列表中联系人的城市名称的类型。 有关详细信息，请参阅[为 SharePoint 创建站点栏、 内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)并[列](http://go.microsoft.com/fwlink/?LinkId=226840)。

### <a name="site-definition-farm-solution-only"></a>网站定义 （仅场解决方案）
 *网站定义*项目项包含站点定义文件夹，其中包含以下文件：

- 默认的.aspx 页，为该站点用作默认的网页。

- *Onet.xml*定义的站点组件的文件。

- 指定出现在站点定义配置的 webtemp xml 文件**模板选择**一部分**新的 SharePoint 站点**页。

  添加站点定义后，你添加代码和文件来引入的功能。 此项目项可仅在场解决方案。 此项目项仅向场解决方案。 有关详细信息，请参阅[创建 SharePoint 站点定义](../sharepoint/creating-site-definitions-for-sharepoint.md)并[站点定义和配置](http://go.microsoft.com/fwlink/?LinkId=260554)。

### <a name="state-machine-workflow-farm-solution-only"></a>状态机工作流 （仅场解决方案）
 一个*状态机工作流*是一组业务逻辑状态、 转换和操作。 按顺序; 不执行状态机工作流中的步骤相反，它们触发的操作和状态。 与顺序工作流状态机工作流是与 SharePoint 项，如列表和文档相关联。 再次重申，您可以创建站点级别 （全局） 工作流或列表级别 (local) 工作流。 此外可以选择是否自动或手动启动工作流。 此项目项可仅在场解决方案。 此项目项仅向场解决方案。 有关详细信息，请参阅[创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)， [SharePoint Server 2010 中的工作流](http://go.microsoft.com/fwlink/?LinkId=260555)，和[What's New:工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="user-control-farm-solution-only"></a>用户控件 （仅场解决方案）
 一个*用户控件*是可以向其中添加其他 ASP.NET 控件和 SharePoint 控件的自定义的可重用控件。 用户控件可以添加到应用程序页和 web 部件在 SharePoint 中运行。 此项目项可仅在场解决方案。 此项目项仅向场解决方案。 有关详细信息，请参阅[为 Web 部件或应用程序页创建可重用控件](http://go.microsoft.com/fwlink/?LinkId=226841)。

### <a name="visual-web-part"></a>可视 web 部件
 一个*可视 web 部件*项目项包括*Elements.xml*定义文件**Web 部件**项，和一个**用户控件**项。 您可以通过拖动或从 Visual Studio 工具箱将控件复制到用户控件的图面设计 visual web 部件的外观。 有关详细信息，请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)和[构建基块：Web 部件](http://go.microsoft.com/fwlink/?LinkId=179438)。

### <a name="web-part"></a>Web 部件
 一个*web 部件*是特殊类型的名为 Web 部件页的页内运行的服务器端控件。 它们是 SharePoint 站点上显示的页的构建基块。 Web 部件项提供使你可以设计 web 部件的 SharePoint 站点的文件。 有关详细信息，请参阅[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)和[构建基块：Web 部件](http://go.microsoft.com/fwlink/?LinkId=179438)。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint 产品和技术](http://go.microsoft.com/fwlink/?LinkId=178818)
