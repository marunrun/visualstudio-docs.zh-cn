---
title: 导入自定义母版页 & 包含图像的网站页面
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 311124b2e0b81e70c4c2a7b40754207e6c66b749
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015681"
---
# <a name="walkthrough-import-a-custom-master-page-and-site-page-with-an-image"></a>演练：导入带有图像的自定义母版页和网站页面
  本演练演示如何将 SharePoint 自定义母版页和包含图像的网站页面导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 项目中。

 此演练演示如何完成以下任务：

- 使用 SharePoint 设计器中的图像创建自定义母版页和网站页。

- 将自定义母版页、图像和网站页导出到 SharePoint 解决方案（*.wsp*）文件。

- *.wsp* [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用 "导入 sharepoint 解决方案包" 项目将 .wsp 文件导入并部署到 SharePoint 项目中。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 若要完成本演练，必须具有以下组件：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

- SharePoint Designer 2010。

## <a name="create-items-in-sharepoint-designer"></a>在 SharePoint 设计器中创建项
 此示例演示如何在 SharePoint Designer 中创建三个用于导出的项：自定义母版页、引用自定义母版页的网站页，以及要在网站页上显示的图像文件。 该图像将添加到 SharePoint 中的/images/文件夹。

#### <a name="to-create-a-custom-master-page-in-sharepoint-designer"></a>在 SharePoint 设计器中创建自定义母版页

1. 在 SharePoint 设计器的导航窗格中，选择 "**母版页**" 网站对象。

2. 在 "**母版页**" 功能区上，选择 "**空白母版页**"。

3. 选择新的母版页，然后在 "**母版页**" 功能区上选择 "**编辑文件**"。

4. 在 SharePoint 设计器的底部，选择 "**代码**" 选项卡。

5. 将现有标记替换为以下标记。

    ```aspx-csharp
    <%@ Master Language="C#" %>
    <%@ Register tagprefix="SharePoint" namespace="Microsoft.SharePoint.WebControls" assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <html dir="ltr">
    <head runat="server">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <SharePoint:RobotsMetaTag runat="server" __designer:Preview="" __designer:Values="<P N='InDesign' T='False' /><P N='ID' T='ctl00' /><P N='Page' ID='1' /><P N='TemplateControl' ID='2' /><P N='AppRelativeTemplateSourceDirectory' R='-1' />"></SharePoint:RobotsMetaTag>
    <title>Web Page</title>
    </head>
    <body>
    <form id="form1" runat="server">
    <asp:ContentPlaceHolder id="ContentPlaceHolderMain"
            runat="server">
          </asp:ContentPlaceHolder>
    </form>
    </body>
    </html>
    ```

6. 保存页面，选择 "**母版页**" 选项卡，然后将母版页重命名为 " **mybasic1**"。

## <a name="add-an-image-to-the-content-database-in-sharepoint-designer"></a>在 SharePoint 设计器中将图像添加到内容数据库
 现在，可以添加要在 "网站" 页上显示的图像。 该映像将部署到 SharePoint 内容数据库。

#### <a name="to-add-an-image-to-the-content-database-in-sharepoint-designer"></a>在 SharePoint 设计器中将图像添加到内容数据库

1. 在导航窗格中，选择 "**所有文件**" 站点对象，然后在树视图中选择 "**图像**" 文件夹。

2. 在 "**所有文件**" 功能区上，选择 "**导入文件**"，选择所选文件，然后选择 **"确定"** 按钮。 在此示例中，该文件的名称为**myimg1.png**。

     （可选）可以创建子文件夹来帮助组织图像。

3. 关闭 "**导入**" 对话框。

## <a name="create-a-site-page"></a>"创建网站" 页
 此基本网站页面使用自定义母版页，并显示你在上一步中添加的映像。

#### <a name="to-create-a-site-page"></a>创建网站页面

1. 在导航窗格中，选择 "**网站页面**" 对象。

2. 在 "**页面**" 功能区上，选择 "**页面**" 按钮，选择 " **ASPX** " 页类型，然后将新文件命名为**mycontentpage1**。

     （可选）可以创建子文件夹来帮助组织站点页面。

3. 在 "网站页" 列表中，选择 " **MyContentPage1** " 以打开其 "属性" 页，然后在页面底部选择 "**编辑文件**" 链接。

     如果出现一条消息，指出此页不包含任何在安全模式下可编辑的区域，并询问您是否要在 "高级" 模式下打开此页，请选择 "**是"** 按钮。

4. 在页面底部，选择 "**代码**" 按钮。

5. 将现有标记替换为以下标记。

    ```aspx-csharp
    <%@ Import Namespace="Microsoft.SharePoint.ApplicationPages" %>
    <%@ Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="Utilities" Namespace="Microsoft.SharePoint.Utilities" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="asp" Namespace="System.Web.UI" Assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" %>
    <%@ Import Namespace="Microsoft.SharePoint" %>
    <%@ Assembly Name="Microsoft.Web.CommandUI, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Page Language="C#" Inherits="Microsoft.SharePoint.WebControls.LayoutsPageBase" MasterPageFile="../_catalogs/masterpage/mybasic1.master" meta:progid="SharePoint.WebPartPage.Document" %>

    <asp:Content ID="Main" ContentPlaceHolderID="ContentPlaceHolderMain" runat="server">
    <img alt="My Image" longdesc="My image from images folder" src="../images/myimg1.png" />
    </asp:Content>
    ```

6. 保存已更新的网站页面。

## <a name="export-the-items-from-sharepoint"></a>从 SharePoint 导出项
 将 SharePoint 中的项导出到 SharePoint 解决方案（*.wsp*）文件。

#### <a name="to-export-items-from-sharepoint-designer"></a>从 SharePoint 设计器导出项

1. 在 SharePoint 设计器的导航窗格中，选择 "**团队网站**" 对象，然后在 "**网站**" 功能区上选择 "**另存为模板**"。

2. 在 "**另存为模板**" 对话框中，输入文件名和模板名称，选中 "**包括内容**" 复选框，然后选择 **"确定"** 按钮。

     这会将站点的内容保存在 *.wsp*文件中。

3. 解决方案导出后，选择 "**解决方案库**" 链接以显示可用解决方案文件的列表。

4. 打开新 *.wsp*文件的快捷菜单，然后选择 "**将目标另存为**" 将其保存到系统中。

## <a name="import-the-items-into-visual-studio"></a>将项目导入 Visual Studio
 将 *.wsp*文件导入到中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 导入内容后，你可以对其进行自定义、添加更多项，然后部署它。

#### <a name="to-import-items-from-the-wsp-file-into-visual-studio"></a>将项从 .wsp 文件导入到 Visual Studio

1. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，创建一个**导入 SharePoint 2010 解决方案包**项目。

2. 在 "**选择要导入的项**" 页上的 "**类型**" 列中的 "**模块**" 下，选中要导入的下表中的文件的复选框。

   | 文件名 | 说明 |
   |------------------------|-----------------------------------------------|
   | \_catalogsmasterpage\_ | 自定义母版页。 |
   | images_ | SharePoint 文件系统中的映像文件。 |
   | SitePages_ | 网站页面。 |

3. 选择 "**完成**" 按钮以导入所选项目。

4. 在**解决方案资源管理器**中，选择 " \_ catalogsmasterpage" \_ 节点，并将其 "**部署冲突解决方法**" 属性的值设置为 "**自动**"。

    这有助于确保自动解决任何部署冲突。

5. 如果新母版页的名称与现有页面的名称相同，请确保现有页面不会标记为默认母版页或 SharePoint Designer 中的自定义母版页。

    如果现有母版页标记为默认母版页或自定义母版页，则会出现部署错误，指出无法删除母版页。 若要避免此问题，请执行以下操作：

   - 如果将现有母版页设置为 "默认母版页"，请暂时将另一个母版页设置为默认母版页。 将文件部署到 SharePoint 后，将新母版页设置为 "默认母版页"。

   - 如果将现有母版页设置为自定义母版页，请暂时将另一个母版页设置为自定义母版页。 将文件部署到 SharePoint 后，将新的母版页设置为自定义母版页。

6. 在菜单栏上，选择 "**生成**" "  >  **部署解决方案**"。

7. 打开 SharePoint 站点以查看已部署的项目。

   导入文件并将其部署到 SharePoint 的另一种方法 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 是将文件添加到中的模块 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][如何：导入母版页或主题](../sharepoint/how-to-import-a-master-page-or-theme.md)，并[使用模块在解决方案中包含文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)。

## <a name="see-also"></a>另请参阅
- [从现有 SharePoint 站点导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
