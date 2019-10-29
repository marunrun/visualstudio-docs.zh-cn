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
ms.openlocfilehash: 0eaf7bda4ac4ed67dae79b8dd83bb59ba6985343
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985029"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>演练：创建 SharePoint 应用程序页

应用程序页是 ASP.NET 页的专用形式。 应用程序页包含与 SharePoint 母版页合并的内容。 有关详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

本演练演示如何创建一个应用程序页，然后使用本地 SharePoint 站点对其进行调试。 此页显示每个用户在服务器场中的所有站点中创建或修改的所有项。

本演练阐释了以下任务：

- 创建 SharePoint 项目。
- 向 SharePoint 项目中添加一个应用程序页。
- 将 ASP.NET 控件添加到应用程序页。
- 在 ASP.NET 控件后面添加代码。
- 测试应用程序页。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>Prerequisites

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-sharepoint-project"></a>创建 SharePoint 项目

首先，创建一个**空 SharePoint 项目**。 稍后，您将向此项目中添加一个**应用程序页**项。

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 打开 "**新建项目**" 对话框，展开想要使用的语言下的 " **Office/SharePoint** " 节点，然后选择 " **SharePoint 解决方案**" 节点。

3. 在 " **Visual Studio 已安装的模板**" 窗格中，选择 " **SharePoint 2010-空项目**" 模板。 将项目命名为**MySharePointProject**，然后选择 **"确定"** 按钮。

     " **SharePoint 自定义向导**" 随即出现。 使用此向导，您可以选择将用于调试项目的站点以及解决方案的信任级别。

4. 选择 "**部署为场解决方案**" 选项按钮，然后选择 "**完成**" 按钮以接受默认的本地 SharePoint 站点。

## <a name="create-an-application-page"></a>"创建应用程序" 页

若要创建应用程序页，请向项目添加 "**应用程序页**" 项。

1. 在**解决方案资源管理器**中，选择 " **MySharePointProject** " 项目。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在 "**添加新项**" 对话框中，选择 "**应用程序" 页（仅场解决方案**模板。

4. 将该页命名为**SearchItems**，然后选择 "**添加**" 按钮。

     Visual Web Developer 设计器会在**源**视图中显示应用程序页，可以在其中查看该页的 HTML 元素。 设计器将为多个 <xref:System.Web.UI.WebControls.Content> 控件显示标记。 每个控件都映射到在默认应用程序母版页中定义的 <xref:System.Web.UI.WebControls.ContentPlaceHolder> 控件。

## <a name="design-the-layout-of-the-application-page"></a>设计应用程序页的布局

使用 "应用程序页" 项可以使用设计器将 ASP.NET 控件添加到应用程序页。 此设计器与 Visual Web Developer 中使用的设计器相同。 向设计器的 "**源**" 视图添加标签、单选按钮列表和表，然后设置属性，就像设计任何标准 ASP.NET 页一样。

1. 在菜单栏上，依次选择“视图” > “工具箱”。

2. 在 "**工具箱**" 的 "标准" 节点中，执行以下步骤之一：

    - 打开**标签**项的快捷菜单，选择 "**复制**"，在设计器中的 " **PlaceHolderMain**内容" 控件下打开行的快捷菜单，然后选择 "**粘贴**"。

    - 将 "**标签**" 项从 "**工具箱**" 拖动到 " **PlaceHolderMain** " 内容控件的正文中。

3. 重复上述步骤，将**DropDownList**项和**表**项添加到**PlaceHolderMain**内容控件。

4. 在设计器中，将 "标签" 控件的 "`Text`" 属性的值更改为**显示所有项**。

5. 在设计器中，将 `<asp:DropDownList>` 元素替换为以下 XML。

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>处理页上的控件的事件

像处理任何 ASP.NET 页一样，处理应用程序页中的控件。 在此过程中，您将处理下拉列表的 `SelectedIndexChanged` 事件。

1. 在 "**视图**" 菜单上，选择 "**代码**"。

     应用程序页代码文件将在代码编辑器中打开。

2. 将以下方法添加到 `SearchItems` 类。 此代码通过调用你稍后将在本演练中创建的方法来处理 <xref:System.Web.UI.WebControls.DropDownList> 的 <xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> 事件。

     [!code-vb[SP_ApplicationPage#5](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#5)]
     [!code-csharp[SP_ApplicationPage#5](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#5)]

3. 将以下语句添加到应用程序页代码文件的顶部。

     [!code-vb[SP_ApplicationPage#1](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#1)]
     [!code-csharp[SP_ApplicationPage#1](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#1)]

4. 将以下方法添加到 `SearchItems` 类。 此方法循环访问服务器场中的所有站点，并搜索由当前用户创建或修改的项目。

     [!code-vb[SP_ApplicationPage#2](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#2)]
     [!code-csharp[SP_ApplicationPage#2](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#2)]

5. 将以下方法添加到 `SearchItems` 类。 此方法显示表中由当前用户创建或修改的项。

     [!code-vb[SP_ApplicationPage#3](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#3)]
     [!code-csharp[SP_ApplicationPage#3](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#3)]

## <a name="test-the-application-page"></a>测试应用程序页

运行该项目时，SharePoint 网站将打开，并显示应用程序页面。

1. 在**解决方案资源管理器**中，打开应用程序页的快捷菜单，然后选择 "**设为启动项**"。

2. 选择 F5。

     SharePoint 站点将打开。

3. 在 "应用程序" 页上，选择 "**由我修改**" 选项。

     应用程序页将刷新并显示您在服务器场中的所有站点中修改的所有项。

4. 在 "应用程序" 页上，在列表中选择 "**由我创建**"。

     应用程序页将刷新并显示你在服务器场中的所有站点中创建的所有项。

## <a name="next-steps"></a>后续步骤

有关 SharePoint 应用程序页的详细信息，请参阅[为 Sharepoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

可以通过以下主题中的 Visual Web Designer 来了解有关如何设计 SharePoint 页面内容的详细信息：

- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>请参阅

[如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)
[Application _layouts 页类型](/previous-versions/office/aa979604(v=office.14))
