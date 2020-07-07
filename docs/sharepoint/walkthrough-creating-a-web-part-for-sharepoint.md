---
title: 演练：为 SharePoint 创建 Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], developing
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7d8b5e05fb234e9997bce615f7b2de1d790c1ae0
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014578"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>演练：为 SharePoint 创建 web 部件

Web 部件允许用户使用浏览器直接修改 SharePoint 网站页的内容、外观和行为。 本演练演示如何使用 Visual Studio 2010 中的 " **Web 部件**" 项模板创建 web 部件。

Web 部件显示数据网格中的雇员。 用户指定包含员工数据的文件的位置。 用户还可以筛选数据网格，以便只在列表中显示经理的员工。

本演练阐释了以下任务：

- 使用 Visual Studio **Web 部件**项模板创建 Web 部件。

- 创建可由 Web 部件的用户设置的属性。 此属性指定雇员数据文件的位置。

- 通过向 Web 部件控件集合添加控件，在 Web 部件中呈现内容。

- 创建一个新菜单项（称为*谓词）* ，该菜单项出现在所呈现的 Web 部件的谓词菜单中。 谓词使用户能够修改 Web 部件中显示的数据。

- 在 SharePoint 中测试 Web 部件。

    > [!NOTE]
    > 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio 2017 或 Azure DevOps Services。

## <a name="create-an-empty-sharepoint-project"></a>创建一个空 SharePoint 项目

首先，创建一个空 SharePoint 项目。 稍后，你将使用 " **Web 部件**" 项模板将 web 部件添加到项目。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]使用 "以**管理员身份运行**" 选项启动。

2. 在男人栏上，选择 "**文件**" "  >  **新建**  >  **项目**"。

3. 在 "**新建项目**" 对话框中，展开要使用的语言下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在 "**模板**" 窗格中，选择 " **SharePoint 2010 项目**"，然后选择 "**确定"** 按钮。

     " **SharePoint 自定义向导**" 随即出现。 使用此向导，您可以选择将用于调试项目的站点以及解决方案的信任级别。

5. 选择 "**部署为场解决方案**" 选项按钮，然后选择 "**完成**" 按钮以接受默认的本地 SharePoint 站点。

## <a name="add-a-web-part-to-the-project"></a>向项目中添加 web 部件

向项目中添加**Web 部件**项。 **Web 部件**项添加 web 部件代码文件。 稍后，您将向 Web 部件代码文件添加代码，以呈现 Web 部件的内容。

1. 在菜单栏上，选择 "**项目**" "  >  **添加新项**"。

2. 在 "**添加新项**" 对话框的 "**已安装的模板**" 窗格中，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 SharePoint 模板列表中，选择 " **Web 部件**" 模板，然后选择 "**添加**" 按钮。

     **Web 部件**项显示在**解决方案资源管理器**中。

## <a name="rendering-content-in-the-web-part"></a>在 web 部件中呈现内容

可以通过将控件添加到 Web 部件类的 controls 集合来指定要在 Web 部件中显示的控件。

1. 在**解决方案资源管理器**中，打开*WebPart1* （在 Visual Basic 中）或*WebPart1.cs* （在 c # 中）。

     Web 部件代码文件将在代码编辑器中打开。

2. 将以下指令添加到 Web 部件代码文件的顶部。

     [!code-csharp[SP_WebPart#1](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#1)]
     [!code-vb[SP_WebPart#1](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#1)]

3. 将以下代码添加到 `WebPart1` 类。 此代码声明以下字段：

   - 用于在 Web 部件中显示员工的数据网格。

   - 在用于筛选数据网格的控件上显示的文本。

   - 在数据网格无法显示数据时显示错误的标签。

   - 一个字符串，其中包含 employee 数据文件的路径。

     [!code-csharp[SP_WebPart#2](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#2)]
     [!code-vb[SP_WebPart#2](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#2)]

4. 将以下代码添加到 `WebPart1` 类。 此代码将名为的自定义属性添加 `DataFilePath` 到 Web 部件。 自定义属性是可以在 SharePoint 中由用户设置的属性。 此属性获取和设置用于填充数据网格的 XML 数据文件的位置。

     [!code-csharp[SP_WebPart#3](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#3)]
     [!code-vb[SP_WebPart#3](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#3)]

5. 将 `CreateChildControls` 方法替换为以下代码。 此代码执行以下任务：

   - 添加在上一步中声明的数据网格和标签。

   - 将数据网格绑定到包含员工数据的 XML 文件。

     [!code-csharp[SP_WebPart#4](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#4)]
     [!code-vb[SP_WebPart#4](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#4)]

6. 将以下方法添加到 `WebPart1` 类。 此代码执行以下任务：

   - 创建在所呈现的 Web 部件的 Web 部件谓词菜单中显示的谓词。

   - 处理在用户选择谓词菜单中的谓词时所引发的事件。 此代码筛选显示在数据网格中的员工列表。

     [!code-csharp[SP_WebPart#5](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#5)]
     [!code-vb[SP_WebPart#5](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#5)]

## <a name="test-the-web-part"></a>测试 web 部件

运行该项目时，SharePoint 网站将打开。 Web 部件会自动添加到 SharePoint 中的 Web 部件库。 可以将 Web 部件添加到任何 Web 部件页。

1. 将以下 XML 粘贴到记事本文件中。 此 XML 文件包含将出现在 Web 部件中的示例数据。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
        <employees xmlns="http://schemas.microsoft.com/vsto/samples">
           <employee>
               <name>David Hamilton</name>
               <hireDate>2001-05-11</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Karina Leal</name>
               <hireDate>1999-04-01</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Nancy Davolio</name>
               <hireDate>1992-05-01</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Steven Buchanan</name>
               <hireDate>1955-03-04</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Suyama Michael</name>
               <hireDate>1963-07-02</hireDate>
               <title>Sales Associate</title>
           </employee>
        </employees>
    ```

2. 在记事本的菜单栏上，选择 "**文件**  >  **另存为**"。

3. 在 "**另存为**" 对话框的 "**保存类型**" 列表中，选择 "**所有文件**"。

4. 在 "**文件名" 框中**，输入**data.xml**。

5. 使用 "**浏览文件夹**" 按钮选择任意文件夹，然后选择 "**保存**" 按钮。

6. 在 Visual Studio 中，选择**F5**键。

     SharePoint 站点将打开。

7. 在 "**站点操作**" 菜单上，选择 "**更多选项**"。

8. 在 "**创建**" 页中，选择 " **Web 部件" 页**类型，然后选择 "**创建**" 按钮。

9. 在 "**新建 Web 部件页**" 页上，将该页命名为**SampleWebPartPage**，然后选择 "**创建**" 按钮。

     此时将显示 "Web 部件" 页。

10. 选择 Web 部件页上的任意区域。

11. 在页面顶部，选择 "**插入**" 选项卡，然后选择 " **Web 部件**" 按钮。

12. 在 "**类别**" 窗格中，选择 "**自定义**" 文件夹，选择 " **WebPart1** " Web 部件，然后选择 "**添加**" 按钮。

     Web 部件显示在该页上。

## <a name="test-the-custom-property"></a>测试自定义属性

若要填充 Web 部件中显示的数据网格，请指定包含有关每个员工的数据的 XML 文件的路径。

1. 选择显示在 "Web 部件" 右边的箭头，然后从出现的菜单中选择 "**编辑 Web 部件**"。

     页面右侧将显示一个包含 Web 部件属性的窗格。

2. 在窗格中，展开 "**杂项**" 节点，输入以前创建的 XML 文件的路径，选择 "**应用**" 按钮，然后选择 "**确定"** 按钮。

     验证员工列表是否出现在 Web 部件中。

## <a name="test-the-web-part-verb"></a>测试 web 部件谓词

通过单击显示在 Web 部件谓词菜单中的项，显示和隐藏不是经理的员工。

1. 选择显示在 "Web 部件" 右边的箭头，然后从出现的菜单中选择 "**仅显示管理器**"。

     只有作为经理的员工才会出现在 Web 部件中。

2. 再次选择该箭头，然后从出现的菜单中选择 "**显示所有员工**"。

     所有员工都显示在 Web 部件中。

## <a name="see-also"></a>另请参阅

[为 SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
 创建 web 部件[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
[如何：使用设计器](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) 
 创建 SharePoint web 部件[演练：使用设计器为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
