---
title: 创建使用设计器的 SharePoint web 部件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9963c2f7e829e9d295ca254aa651e37e3ad08efd
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401146"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>演练：使用设计器为 SharePoint 创建 web 部件

如果您创建的 SharePoint 站点的 web 部件，用户可以直接修改内容、 外观和行为的该站点中的页通过使用浏览器。 本演练演示如何通过使用 SharePoint 直观地创建 web 部件**可视 Web 部件**Visual Studio 中的项目模板。

你将创建的 web 部件显示站点上每月的日历视图和每个日历列表的复选框。 用户可以指定的日历列表以包含在每月的日历视图中通过选中复选框。

本演练阐释了以下任务：

- 使用创建 web 部件**可视 Web 部件**项目模板。
- 在 Visual Studio 中使用 Visual Web Developer 设计器设计 web 部件。
- 添加代码以处理 web 部件上的控件事件。
- 在 SharePoint 中测试 web 部件。

    > [!NOTE]
    > 您的计算机可能会显示不同的名称或 Visual Studio 用户界面的某些元素的位置中的以下说明进行操作。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-web-part-project"></a>创建 web 部件项目

首先，使用创建 web 部件项目**可视 Web 部件**项目模板。

1. 启动[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]通过使用**以管理员身份运行**选项。

2. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

     此时将出现“新建项目”  对话框。

3. 在中**新的项目**对话框中的，在**Visual C#** 或**Visual Basic**，展开**Office/SharePoint**，然后选择**SharePoint 解决方案**类别。

4. 在模板列表中，选择**SharePoint 2013-可视 Web 部件**模板，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。 通过使用此向导，可以指定将用于调试该项目和解决方案的信任级别的站点。

5. 在中**此 SharePoint 解决方案的信任级别是什么？** 部分中，选择**部署为场解决方案**选项按钮。

6. 选择**完成**按钮以接受默认的本地 SharePoint 站点。

## <a name="designing-the-web-part"></a>设计 web 部件

通过添加控件来设计 web 部件**工具箱**到 Visual Web Developer 设计器图面。

1. 在 Visual Web Developer 设计器中，选择**设计**选项卡以切换到设计视图。

2. 在菜单栏上，依次选择“视图” > “工具箱”   。

3. 在中**标准**的节点**工具箱**，选择**CheckBoxList**控件，然后执行以下步骤之一：

    - 打开快捷菜单**CheckBoxList**控制中，选择**副本**，在设计器中，打开第一行的快捷菜单，然后选择**粘贴**。

    - 拖动**CheckBoxList**控件从**工具箱**，并将控件连接到在设计器中的第一行。

4. 重复上一步，但将按钮移到设计器的下一行。

5. 在设计器中，选择**Button1**按钮。

6. 在菜单栏上依次选择**视图** > **属性窗口**。

     **属性**窗口随即打开。

7. 在中**文本**按钮的属性中输入**更新**。

## <a name="handling-the-events-of-controls-on-the-web-part"></a>处理 web 部件上的控件事件

添加代码，使用户能够将日历添加到母版日历视图。

1. 执行下面的某一组步骤：

   - 在设计器中，双击**更新**按钮。

   - 在中**属性**窗口**更新**按钮，选择**事件**按钮。 在中**单击**属性中，输入**Button1_Click**，然后选择 Enter 键。

     用户控件代码文件将在代码编辑器中打开和`Button1_Click`事件处理程序会显示。 更高版本，会将代码添加到此事件处理程序。

2. 将以下语句添加到用户控件代码文件的顶部。

     [!code-vb[SP_VisualWebPart#1](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_VisualWebPart#1](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

3. 添加以下代码行`VisualWebPart1`类。 此代码声明的每月的日历视图控件。

     [!code-vb[SP_VisualWebPart#2](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#2)]
     [!code-csharp[SP_VisualWebPart#2](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#2)]

4. 替换`Page_Load`方法的`VisualWebPart1`用下面的代码的类。 这段代码执行下列任务：

   - 将每月的日历视图添加到用户控件。

   - 在站点上添加一个复选框，为每个日历列表。

   - 指定在月历视图中显示的项的每个类型的模板。

     [!code-vb[SP_VisualWebPart#3](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#3)]
     [!code-csharp[SP_VisualWebPart#3](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#3)]

5. 替换`Button1_Click`方法的`VisualWebPart1`用下面的代码的类。 此代码将每个所选日历中的项添加到母版日历视图中。

     [!code-vb[SP_VisualWebPart#4](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#4)]
     [!code-csharp[SP_VisualWebPart#4](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#4)]

## <a name="test-the-web-part"></a>测试 web 部件

运行项目时，将打开 SharePoint 站点。 Web 部件会自动添加到在 SharePoint Web 部件库中。 若要测试此项目，将执行以下任务：

- 向每个两个单独的日历列表添加一个事件。
- 将 web 部件添加到 web 部件页。
- 指定要包含在每月的日历视图中的列表。

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>若要将事件添加到网站上的日历列表

1. 在 Visual Studio 中，选择**F5**密钥。

     将打开 SharePoint 站点，并且[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]快速启动栏显示在此页。

2. 在快速启动栏下**列出了**，选择**日历**链接。

     **日历**页将出现。

     如果您没有日历链接显示在快速启动栏上，选择**站点内容**链接。 如果站点内容页中未显示**日历**项目，请创建一个。

3. 在日历页上，选择一天，然后选择**添加**以添加一个事件在所选一天中的链接。

4. 在中**标题**框中，输入**中的默认日历事件**，然后选择**保存**按钮。

5. 选择**站点内容**链接，，然后选择**添加应用**磁贴。

6. 上**创建**页上，选择**日历**类型，命名日历，，然后选择**创建**按钮。

7. 将事件添加到新的日历，将命名事件**中的自定义日历事件**，然后选择**保存**按钮。

### <a name="to-add-the-web-part-to-a-web-part-page"></a>若要将 web 部件添加到 web 部件页

1. 上**站点内容**页上，打开**站点页面**文件夹。

2. 在功能区中，选择**文件**选项卡上，打开**新文档**菜单中，然后选择**Web 部件页**命令。

3. 上**新的 Web 部件页**页上，将该页命名为**SampleWebPartPage.aspx**，然后选择**创建**按钮。

     将显示 web 部件页。

4. 在 web 部件页的顶部区域，选择**插入**选项卡，然后选择**Web 部件**按钮。

5. 选择**自定义**文件夹中，选择**VisualWebPart1** web 部件，，然后选择**添加**按钮。

     Web 部件显示在此页。 以下控件显示 web 部件：

    - 每月的日历视图。

    - **更新**按钮。

    - 一个**日历**复选框。

    - 一个**自定义日历**复选框。

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>若要指定列出要包含在月历视图中

在 web 部件中，指定你想要包括在每月的日历视图中，然后选择日历**更新**按钮。

从指定的所有日历事件显示在每月的日历视图中。

## <a name="see-also"></a>请参阅

[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
[演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
