---
title: 演练：从现有的 SharePoint 网站导入项目 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: a2727f0f3a5f2b46c5110a33e63b102f9d26bdaf
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446606"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>演练：从现有的 SharePoint 网站导入项目
  本演练演示如何从现有的 SharePoint 网站到导入项[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 项目。

 本演练演示了下列任务：

- 通过添加自定义站点列自定义 SharePoint 站点 (也称为*字段*。

- 导出到.wsp 文件的 SharePoint 站点。

- 导入.wsp 文件到[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 通过使用.wsp 导入项目。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的版本[!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)]和 SharePoint。

- Visual Studio。

## <a name="customize-a-sharepoint-site"></a>自定义 SharePoint 站点
 对于此示例中，将创建并自定义 SharePoint 子站点，通过向其添加一个新的站点列和通过创建另一个子网站供以后使用。 更高版本，将导出到.wsp 文件的第一个子网站，并通过使用.wsp 导入项目，然后导入第二个子站点的自定义站点列。

### <a name="to-create-and-customize-a-sharepoint-site"></a>若要创建和自定义 SharePoint 站点

1. 打开 SharePoint 站点使用 Web 浏览器，如 http://<em>系统名称</em>/SitePages/Home.aspx。

2. 通过打开创建从主要的 SharePoint 网站的子网站**站点操作**菜单，然后选择**新站点**。

3. 在站点的**创建**对话框框中，选择**Blank Site**类型。

4. 在中**标题**框中，输入**站点列测试 1**; 在**URL 名称**框中，输入**columntest1**; 将其他设置保留其默认值值;然后选择**创建**按钮。

5. 创建网站后，导航回主站点上，在浏览器中 http://<em>系统名称</em>/SitePages/Home.aspx。

6. 同样，通过打开创建空的子站点从主要的 SharePoint 网站**站点操作**菜单中，选择**新的站点**，然后选择**Blank Site**类型。

7. 在中**标题**框中，输入**站点列测试 2**; 在**URL 名称**框中，输入**columntest2**; 将其他设置保留其默认值值;然后选择**创建**按钮。

8. 第一个子网站，浏览到 http://<em>SystemName</em>/columntest1/default.aspx。

9. 上**站点操作**菜单中，选择**站点设置**以显示站点设置页。

10. 在中**库**部分中，选择**站点列**链接。

11. 在顶部**网站栏库**页上，选择**创建**按钮。

12. 在中**列名**框中，输入**测试列**，保留其他默认值，，然后选择**确定**按钮。

13. **测试列**列下显示自定义列标题网站库中的列。

## <a name="exporting-the-sharepoint-site"></a>导出 SharePoint 站点
 接下来，获取一个包含 SharePoint 项和你想要导入到的元素的 SharePoint 安装程序 (.wsp) 文件您[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 项目。 如果你还没有.wsp 文件，则必须创建一个从现有的 SharePoint 网站。 对于此示例中，将默认的 SharePoint 站点导出到.wsp 文件。

> [!IMPORTANT]
> 如果收到运行时错误，执行以下过程，您必须能够访问 SharePoint 站点的系统上执行该过程。

### <a name="to-export-an-existing-sharepoint-site"></a>若要导出的现有 SharePoint 站点

1. 在 SharePoint 站点中，选择**站点设置**上**站点操作**选项卡以显示站点设置页。

2. 在中**站点操作**部分的站点设置页中，选择**另存为模板站点**链接。

3. 在中**文件名**框中，输入**ExampleSite**，然后在**模板名称**框中，输入**示例站点**。

4. 此示例中，将保留**内容包括**复选框为空。

     如果选中此框，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将所有列表和文档库和其内容保存到.wsp 文件。 虽然这是在某些情况下很有用，但它不是此示例所必需的。

5. 该操作成功完成后，选择**解决方案库**链接可查看.wsp 文件。

     若要查看更高版本中打开的解决方案库页**站点操作**菜单中，选择**站点设置**，选择**转到顶级站点设置**中的链接**站点集合管理**部分，然后再选择**解决方案**中的链接**库**部分。

6. 在解决方案库中，选择**ExampleSite**链接。

7. 在中**文件下载**对话框框中，选择**保存**按钮以保存您的本地系统上的文件默认情况下，在 Downloads 文件夹中。

## <a name="import-the-wsp-file"></a>导入.wsp 文件
 现在，你已有 *.wsp*文件，其中包含你想要重复使用 （自定义站点列测试列），导入的项 *.wsp*文件来访问它。

### <a name="to-import-a-wsp-file"></a>若要导入.wsp 文件

1. 在中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，在菜单栏上依次选择**文件** > **新建** > **项目**显示**新项目**对话框。 如果您的 IDE 设置为使用 Visual Basic 开发设置，请在菜单栏上，选择**文件** > **新项目**。

2. 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

3. 选择**导入 SharePoint 2010 解决方案包**中的模板**模板**窗格中，保留 WspImportProject1，作为项目的名称，然后选择**确定**按钮。

    **SharePoint 自定义向导**出现。

4. 上**指定用于调试的网站和安全级别**页上，输入[!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]为前面创建第二个 SharePoint 子站点。 您将添加新的自定义字段项、 http://<em>系统名称</em>/columntest2，对该子网站。

5. 在中**此 SharePoint 解决方案的信任级别是什么？** 部分中，将为此选项保留**部署为沙盒解决方案**。

6. 在中**指定新项目源**页上，浏览到您保存在系统上的位置 *.wsp*以前文件，然后选择**下一步**按钮。

   > [!NOTE]
   > 如果愿意**完成**按钮在此页上，在所有可用项 *.wsp*将导入文件。

7. 在中**选择要导入的项**框中，清除所有除列表中的复选框**测试列**，然后选择**完成**按钮。

    由于此列表包含多个项，可以选择**Ctrl**+**A**键以选择所有项在列表中，都选择空格键以清除所有复选框，然后选择仅检查框旁边**测试列**项。

    导入操作完成后，一个名为的新项目后**WspImportProject1**创建，其中包含名为的文件夹**字段**。 在此文件夹是自定义网站栏**测试列**及其定义文件*Elements.xml*。

## <a name="deploy-the-project"></a>将项目部署
 最后，部署**WspImportProject1**到第二个 SharePoint 子站点之前，若要查看自定义站点列创建。

### <a name="to-deploy-the-project"></a>若要将项目部署

1. 在中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，选择**F5**键部署并运行 *.wsp*导入项目。

2. 在 SharePoint 站点上打开**站点操作**菜单，然后选择**站点设置**以显示站点设置页。

3. 在中**库**部分中，选择**站点列**链接。

4. 向下滚动到**自定义列**部分。

     请注意，从第一个 SharePoint 站点导入的自定义站点列将出现在列表中。

## <a name="see-also"></a>请参阅
- [从现有的 SharePoint 网站导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [创建 web 部件或应用程序页的可重用的控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
