---
title: 演练：从现有 SharePoint 站点导入项 |Microsoft Docs
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
ms.openlocfilehash: 46bc2ceacfde599a70b4e84bba134c4a4d5f9757
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86017122"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>演练：从现有 SharePoint 网站导入项
  本演练演示如何将项从现有 SharePoint 网站导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sharepoint 项目。

 本演练演示了下列任务：

- 通过添加自定义网站列来自定义 SharePoint 网站 (也称为 *字段*。

- 将 SharePoint 站点导出到 .wsp 文件。

- 使用 .wsp 导入项目将 .wsp 文件导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 中。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

## <a name="customize-a-sharepoint-site"></a>自定义 SharePoint 站点
 在此示例中，你将通过向 SharePoint 子站点添加新的网站栏并创建另一个子网站来创建和自定义 SharePoint 子站点，以便以后使用。 稍后，你会将第一个子站点导出到 .wsp 文件，然后使用 .wsp 导入项目将自定义网站列导入第二个子网站。

### <a name="to-create-and-customize-a-sharepoint-site"></a>创建和自定义 SharePoint 站点

1. 使用 Web 浏览器打开 SharePoint 站点，如 http://<em>system name</em>/SitePages/Home.aspx。

2. 通过打开 " **网站操作** " 菜单并选择 " **新建网站**"，从主 SharePoint 站点创建子网站。

3. 在站点的 " **创建** " 对话框中，选择 " **空白站点** " 类型。

4. 在 " **标题** " 框中，输入 " **网站列测试 1**"。在 " **URL 名称** " 框中，输入 **columntest1**;将其他设置保留为其默认值;然后选择 " **创建** " 按钮。

5. 创建站点后，在浏览器中导航回到主站点，http://<em>system name</em>/SitePages/Home.aspx。

6. 同样，可以通过打开 " **站点操作** " 菜单，选择 " **新建网站**"，然后选择 " **空白站点** " 类型，创建主 SharePoint 站点的空白子站点。

7. 在 " **标题** " 框中，输入 " **网站列测试 2**"。在 " **URL 名称** " 框中，输入 **columntest2**;将其他设置保留为其默认值;然后选择 " **创建** " 按钮。

8. 导航回第一个子站点，http://<em>SystemName</em>/columntest1/default.aspx。

9. 在 " **站点操作** " 菜单上，选择 " **站点设置** " 以显示 "站点设置" 页。

10. 在 " **库** " 部分中，选择 " **网站列** " 链接。

11. 在 " **网站列库** " 页的顶部，选择 " **创建** " 按钮。

12. 在 " **列名称** " 框中，输入 " **测试列**"，保留其他默认值，然后选择 **"确定"** 按钮。

13. " **测试列** " 列显示在 "网站" 列库中的 "自定义列" 标题下。

## <a name="exporting-the-sharepoint-site"></a>导出 SharePoint 站点
 接下来，获取 SharePoint 安装 ( .wsp) 文件，其中包含要导入到 sharepoint 项目中的 SharePoint 项和元素 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 如果还没有 .wsp 文件，则必须从现有的 SharePoint 站点创建一个。 在此示例中，将默认的 SharePoint 站点导出到 .wsp 文件中。

> [!IMPORTANT]
> 如果在执行以下过程时收到运行时错误，则必须在对 SharePoint 站点具有访问权限的系统上执行该过程。

### <a name="to-export-an-existing-sharepoint-site"></a>导出现有 SharePoint 站点

1. 在 SharePoint 站点中，选择 "**站点操作**" 选项卡上的 "**站点设置**"，以显示 "站点设置" 页。

2. 在 "站点设置" 页的 " **站点操作** " 部分，选择 " **将站点另存为模板** " 链接。

3. 在 " **文件名" 框中** ，输入 " **ExampleSite**"，然后在 " **模板名称** " 框中，输入 " **Example Site**"。

4. 对于本示例，请清除 " **包括内容** " 复选框。

     如果选择此框，则会 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将所有列表和文档库及其内容保存到 .wsp 文件。 尽管这在某些情况下很有用，但在此示例中不需要这样做。

5. 操作成功完成后，选择 " **解决方案库** " 链接以查看 .wsp 文件。

     若要在以后查看 "解决方案库" 页，请打开 "**站点操作**" 菜单，选择 "**站点设置**"，在 "**网站集管理**" 部分中选择 "**中转到顶层站点设置**" 链接，然后选择 "**库**" 部分中的 "**解决方案**" 链接。

6. 在解决方案库中，选择 " **ExampleSite** " 链接。

7. 在 " **文件下载** " 对话框中，选择 " **保存** " 按钮，在默认情况下，将文件保存在本地系统上的 "下载" 文件夹中。

## <a name="import-the-wsp-file"></a>导入 .wsp 文件
 现在，你已有一个 *.wsp* 文件，其中包含你要重复使用的项 (自定义网站列测试列) ，导入 *.wsp* 文件以进行访问。

### <a name="to-import-a-wsp-file"></a>导入 .wsp 文件

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的菜单栏上，选择 "**文件**" "  >  **新建**  >  **项目**" 以显示 "**新建项目**" 对话框。 如果 IDE 设置为使用 Visual Basic 开发设置，请在菜单栏上选择 "**文件**" "  >  **新建项目**"。

2. 展开 " **Visual c #** " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 "**模板**" 窗格中选择 "**导入 SharePoint 2010 解决方案包**" 模板，将项目名称保留为 "WspImportProject1"，然后选择 **"确定"** 按钮。

    " **SharePoint 自定义向导** " 随即出现。

4. 在 " **指定用于调试的站点和安全级别** " 页上， [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 为之前创建的第二个 SharePoint 子站点输入。 你将向该子网站添加新的自定义字段项 http://<em>system name</em>/columntest2。

5. 在 " **此 SharePoint 解决方案的信任级别是什么？** " 部分中，将选定内容保留为 " **部署为沙盒解决方案**"。

6. 在 " **指定新的项目源** " 页上，浏览到系统上以前保存 *.wsp* 文件的位置，然后选择 " **下一步** " 按钮。

   > [!NOTE]
   > 如果在此页上选择 " **完成** " 按钮，则将导入 *.wsp* 文件中的所有可用项。

7. 在 " **选择要导入的项** " 框中，清除列表中除 " **测试列**" 之外的所有复选框，然后选择 " **完成** " 按钮。

    由于列表包含多个项，因此可以选择**Ctrl** + **A**键以选择列表中的所有项，选择空格键以清除所有复选框，然后仅选中**测试列**项旁边的复选框。

    导入操作完成后，将创建一个名为 **WspImportProject1** 的新项目，其中包含一个名为 " **字段**" 的文件夹。 在此文件夹中，为自定义网站列 **测试列** 及其定义文件 *Elements.xml*。

## <a name="deploy-the-project"></a>部署项目
 最后，将 **WspImportProject1** 部署到之前创建的第二个 SharePoint 子网站，以查看自定义网站列。

### <a name="to-deploy-the-project"></a>部署项目

1. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，选择 **F5** 键以部署并运行 *.wsp* 导入项目。

2. 在 SharePoint 站点上，打开 " **站点操作** " 菜单，然后选择 " **站点设置** " 以显示 "站点设置" 页。

3. 在 " **库** " 部分中，选择 " **网站列** " 链接。

4. 向下滚动到 " **自定义列** " 部分。

     请注意，从第一个 SharePoint 站点导入的自定义网站列将出现在列表中。

## <a name="see-also"></a>另请参阅
- [从现有 SharePoint 站点导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
