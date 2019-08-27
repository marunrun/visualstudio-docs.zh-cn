---
title: 演练：创建 SharePoint 应用程序页 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 749ec5f7f7bd68911accb33e4e8631b42de8e630
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778627"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>演练：创建 SharePoint 应用程序页

应用程序页是 ASP.NET 页面的一种专用的形式。 应用程序页包含与 SharePoint 母版页合并的内容。 有关详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

本演练演示如何创建应用程序页并调试使用本地 SharePoint 站点。 此页显示每个用户具有创建或修改中的所有网站服务器场中的所有项。

本演练阐释了以下任务：

- 创建 SharePoint 项目。
- 将应用程序页添加到 SharePoint 项目。
- 将 ASP.NET 控件添加到应用程序页。
- 添加代码隐藏的 ASP.NET 控件。
- 测试应用程序页。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-sharepoint-project"></a>创建 SharePoint 项目

首先，创建**空 SharePoint 项目**。 更高版本，您将添加**应用程序页**到此项目项。

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 打开**新的项目**对话框框中，展开**Office/SharePoint**节点下你想要使用，然后选择的语言**SharePoint 解决方案**节点。

3. 在中**Visual Studio 已安装的模板**窗格中，选择**SharePoint 2010-空项目**模板。 将项目命名**MySharePointProject**，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。 此向导，可选择将用于调试该项目和解决方案的信任级别的站点。

4. 选择**部署为场解决方案**选项按钮，然后选择**完成**按钮以接受默认的本地 SharePoint 站点。

## <a name="create-an-application-page"></a>创建应用程序页

若要创建的应用程序页，添加**应用程序页**到项目的项。

1. 在中**解决方案资源管理器**，选择**MySharePointProject**项目。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在中**添加新项**对话框框中，选择**应用程序页上 (仅场解决方案**模板。

4. 将该页命名为**SearchItems**，然后选择**添加**按钮。

     Visual Web Developer 设计器将显示在应用程序页上**源**视图，可从中查看此页的 HTML 元素。 设计器会显示多个标记<xref:System.Web.UI.WebControls.Content>控件。 每个控件均映射到<xref:System.Web.UI.WebControls.ContentPlaceHolder>默认应用程序母版页中定义的控件。

## <a name="design-the-layout-of-the-application-page"></a>设计应用程序页的布局

应用程序页项，您可以使用设计器将 ASP.NET 控件添加到应用程序页。 此设计器是在 Visual Web Developer 中使用的同一设计器。 添加标签、 单选按钮列表中和将表**源**视图设计器中，并像设计任何标准 ASP.NET 页时一样，然后设置属性。

1. 在菜单栏上，依次选择“视图” > “工具箱”。

2. 在标准节点**工具箱**，执行以下步骤之一：

    - 打开快捷菜单**标签**项中，选择**副本**，打开下方的行的快捷菜单**PlaceHolderMain**内容控件在设计器，然后选择**粘贴**。

    - 拖动**标签**项从**工具箱**到正文**PlaceHolderMain**内容控件。

3. 重复上述步骤以添加**DropDownList**项和一个**表**项**PlaceHolderMain**内容控件。

4. 在设计器中，将更改的值`Text`到标签控件的特性**显示所有项**。

5. 在设计器中，将为`<asp:DropDownList>`具有下面的 XML 元素。

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>处理的页上的控件的事件

处理应用程序页中的控件，像任何 ASP.NET 页面一样。 在此过程中，将处理`SelectedIndexChanged`下拉列表的事件。

1. 上**视图**菜单中，选择**代码**。

     应用程序页代码文件将在代码编辑器中打开。

2. 将以下方法添加到 `SearchItems` 类。 此代码处理<xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged>事件的<xref:System.Web.UI.WebControls.DropDownList>通过调用将稍后在本演练中创建的方法。

     [!code-vb[SP_ApplicationPage#5](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#5)]
     [!code-csharp[SP_ApplicationPage#5](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#5)]

3. 将以下语句添加到应用程序页代码文件的顶部。

     [!code-vb[SP_ApplicationPage#1](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#1)]
     [!code-csharp[SP_ApplicationPage#1](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#1)]

4. 将以下方法添加到 `SearchItems` 类。 此方法循环访问的服务器场中所有站点，并搜索由当前用户创建或修改的项。

     [!code-vb[SP_ApplicationPage#2](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#2)]
     [!code-csharp[SP_ApplicationPage#2](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#2)]

5. 将以下方法添加到 `SearchItems` 类。 此方法显示由当前用户在表中创建或修改的项。

     [!code-vb[SP_ApplicationPage#3](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#3)]
     [!code-csharp[SP_ApplicationPage#3](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#3)]

## <a name="test-the-application-page"></a>测试应用程序页

运行项目时，SharePoint 网站将打开，并显示应用程序页。

1. 在中**解决方案资源管理器**，打开应用程序页的快捷菜单，然后选择**设置为启动项**。

2. 选择 F5。

     SharePoint 网站将打开。

3. 在应用程序页上，选择**由我修改**选项。

     刷新应用程序页，并显示中的所有网站服务器场中已修改的所有项。

4. 在应用程序页上，选择**由我创建**列表中。

     刷新应用程序页，并显示已在服务器场中所有站点中创建的所有项。

## <a name="next-steps"></a>后续步骤

有关 SharePoint 应用程序页的详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

您可以详细了解如何使用 Visual Web 设计器从下面这些主题设计 SharePoint 页内容：

- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [创建的 web 部件或应用程序页的可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>请参阅

[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)
[Application _layouts 的页类型](http://go.microsoft.com/fwlink/?LinkID=169274)
