---
title: 使用设计器创建 SharePoint web 部件
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 732bd9fe3d34a768e0c6f71315f212c49bdf02af
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016395"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>演练：使用设计器为 SharePoint 创建 web 部件

如果为 SharePoint 站点创建 web 部件，用户可以使用浏览器直接修改该网站中页面的内容、外观和行为。 本演练演示如何使用 Visual Studio 中的 "SharePoint**可视 Web 部件**" 项目模板以可视化方式创建 web 部件。

您将创建的 web 部件将显示每月的日历视图，以及站点上每个日历列表的复选框。 用户可以通过选中相应的复选框来指定要包含在月历视图中的日历列表。

本演练阐释了以下任务：

- 使用 "**可视 Web 部件**" 项目模板创建 web 部件。
- 使用 Visual Studio 中的 Visual Web Developer 设计器设计 web 部件。
- 添加代码以处理 web 部件上的控件的事件。
- 在 SharePoint 中测试 web 部件。

    > [!NOTE]
    > 在以下说明中，计算机可能会为 Visual Studio 的用户界面的某些元素显示不同的名称或位置。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

## <a name="create-a-web-part-project"></a>创建 web 部件项目

首先，使用 "**可视 Web 部件**" 项目模板创建 web 部件项目。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]使用 "以**管理员身份运行**" 选项启动。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

     将显示“新建项目”对话框。

3. 在 "**新建项目**" 对话框中的 " **Visual c #** " 或 " **Visual Basic**" 下，展开 " **Office/SharePoint**"，然后选择 " **SharePoint 解决方案**" 类别。

4. 在模板列表中，选择 " **SharePoint 2013-可视 Web 部件**" 模板，然后选择 **"确定"** 按钮。

     " **SharePoint 自定义向导**" 随即出现。 通过使用此向导，您可以指定用于调试项目的站点以及解决方案的信任级别。

5. 在 "**此 SharePoint 解决方案的信任级别是什么？** " 部分中，选择 "**部署为场解决方案**" 选项按钮。

6. 选择 "**完成**" 按钮以接受默认的本地 SharePoint 站点。

## <a name="designing-the-web-part"></a>设计 web 部件

设计 web 部件，方法是将 "**工具箱**" 中的控件添加到 Visual web Developer 设计器的图面。

1. 在 Visual Web Developer 设计器中，选择 "**设计**" 选项卡以切换到设计视图。

2. 在菜单栏上，选择 "**视图**  >  **" "工具箱**"。

3. 在 "**工具箱**" 的 "**标准**" 节点中，选择 " **CheckBoxList** " 控件，然后执行以下步骤之一：

    - 打开**CheckBoxList**控件的快捷菜单，选择 "**复制**"，打开设计器中第一行的快捷菜单，然后选择 "**粘贴**"。

    - 从**工具箱**中拖动 " **CheckBoxList** " 控件，并将该控件连接到设计器中的第一行。

4. 重复前面的步骤，但将按钮移动到设计器的下一行。

5. 在设计器中，选择 " **Button1** " 按钮。

6. 在菜单栏上，选择 "**查看**  >  **属性窗口**"。

     此时将打开“属性”窗口****。

7. 在按钮的 "**文本**" 属性中，输入**更新**。

## <a name="handling-the-events-of-controls-on-the-web-part"></a>处理 web 部件上的控件的事件

添加使用户能够将日历添加到母版日历视图中的代码。

1. 执行下面的某一组步骤：

   - 在设计器中，双击 "**更新**" 按钮。

   - 在 "**更新**" 按钮的 "**属性**" 窗口中，选择 "**事件**" 按钮。 在 "**单击**" 属性中，输入**Button1_Click**，然后选择 enter 键。

     用户控件代码文件将在代码编辑器中打开，并 `Button1_Click` 显示事件处理程序。 稍后，您将向此事件处理程序中添加代码。

2. 将以下语句添加到用户控件代码文件的顶部。

     [!code-vb[SP_VisualWebPart#1](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_VisualWebPart#1](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

3. 向类中添加以下代码行 `VisualWebPart1` 。 此代码声明月度日历视图控件。

     [!code-vb[SP_VisualWebPart#2](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#2)]
     [!code-csharp[SP_VisualWebPart#2](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#2)]

4. 将 `Page_Load` 类的方法替换 `VisualWebPart1` 为以下代码。 此代码执行以下任务：

   - 向用户控件添加月历视图。

   - 为站点上的每个日历列表添加一个复选框。

   - 为日历视图中显示的每种类型的项指定模板。

     [!code-vb[SP_VisualWebPart#3](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#3)]
     [!code-csharp[SP_VisualWebPart#3](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#3)]

5. 将 `Button1_Click` 类的方法替换 `VisualWebPart1` 为以下代码。 此代码将每个选定日历中的项添加到母版日历视图中。

     [!code-vb[SP_VisualWebPart#4](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#4)]
     [!code-csharp[SP_VisualWebPart#4](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#4)]

## <a name="test-the-web-part"></a>测试 web 部件

运行该项目时，SharePoint 网站将打开。 Web 部件会自动添加到 SharePoint 中的 Web 部件库。 若要测试此项目，你将执行以下任务：

- 向两个单独日历列表中的每个列表添加一个事件。
- 将 web 部件添加到 web 部件页。
- 指定要包含在月历视图中的列表。

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>向网站上的日历列表添加事件

1. 在 Visual Studio 中，选择**F5**键。

     SharePoint 站点将打开，" [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 快速启动" 栏将显示在该页上。

2. 在 "快速启动" 栏上的 "**列表**" 下，选择 "**日历**" 链接。

     此时将显示 "**日历**" 页。

     如果 "快速启动" 栏上未显示 "日历" 链接，请选择 "**网站内容**" 链接。 如果 "网站内容" 页不显示**日历**项，请创建一个。

3. 在 "日历" 页上，选择一天，然后选择所选日期中的 "**添加**" 链接以添加一个事件。

4. 在 "**标题**" 框中，在**默认日历**中输入事件，然后选择 "**保存**" 按钮。

5. 选择 "**网站内容**" 链接，然后选择 "**添加应用**" 磁贴。

6. 在 "**创建**" 页上，选择**日历**类型，为日历命名，然后选择 "**创建**" 按钮。

7. 向新日历添加事件，**在自定义日历中**命名事件事件，然后选择 "**保存**" 按钮。

### <a name="to-add-the-web-part-to-a-web-part-page"></a>将 web 部件添加到 web 部件页

1. 在 "**网站内容**" 页上，打开 "**站点页面**" 文件夹。

2. 在功能区上，选择 "**文件**" 选项卡，打开 "**新建文档**" 菜单，然后选择 " **Web 部件页**" 命令。

3. 在 "**新建 Web 部件页**" 页上，将该页命名为**SampleWebPartPage**，然后选择 "**创建**" 按钮。

     此时将显示 "web 部件" 页。

4. 在 web 部件页的顶级区域中，选择 "**插入**" 选项卡，然后选择 " **web 部件**" 按钮。

5. 选择 "**自定义**" 文件夹，选择 " **VisualWebPart1** " web 部件，然后选择 "**添加**" 按钮。

     Web 部件显示在该页上。 以下控件显示在 web 部件上：

    - 月历视图。

    - "**更新**" 按钮。

    - "**日历**" 复选框。

    - "**自定义日历**" 复选框。

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>指定要包含在月历视图中的列表

在 web 部件中，指定要包含在月历视图中的日历，然后选择 "**更新**" 按钮。

您指定的所有日历中的事件均显示在每月日历视图中。

## <a name="see-also"></a>另请参阅

[为 SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
 创建 web 部件[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
[演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
