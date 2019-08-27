---
title: 演练：为 SharePoint 创建 Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 622dfafbe16efee1e953fbc42bfa3b94cfa3cc58
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62965266"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>演练：为 SharePoint 创建 web 部件

Web 部件使用户能够使用浏览器直接修改内容、 外观和行为的 SharePoint 站点页面。 本演练演示如何使用创建 Web 部件**Web 部件**Visual Studio 2010 中的项模板。

Web 部件显示数据网格中的员工。 用户指定包含员工数据的文件的位置。 用户还可以筛选数据网格，以便在列表中只显示经理的员工。

本演练阐释了以下任务：

- 使用 Visual Studio 创建 Web 部件**Web 部件**项模板。

- 可以通过 Web 部件的用户设置创建的属性。 此属性指定员工数据文件的位置。

- 通过将控件添加到 Web 部件中呈现 Web 部件中的内容控件集合。

- 创建一个新的菜单项，称为*动词，* 呈现的 Web 部件的谓词菜单中显示。 谓词使用户能够修改 Web 部件中显示的数据。

- 在 SharePoint 中测试 Web 部件。

    > [!NOTE]
    > 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio 2017 或 Azure DevOps 服务。

## <a name="create-an-empty-sharepoint-project"></a>创建一个空 SharePoint 项目

首先，创建一个空 SharePoint 项目。 更高版本，您会将 Web 部件添加到项目通过使用**Web 部件**项模板。

1. 启动[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]通过使用**以管理员身份运行**选项。

2. 在菜单栏上依次选择**文件** > **新建** > **项目**。

3. 在中**新的项目**对话框框中，展开**SharePoint**节点下你想要使用，然后选择的语言**2010年**节点。

4. 在中**模板**窗格中，选择**SharePoint 2010 项目**，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。 此向导，可选择将用于调试该项目和解决方案的信任级别的站点。

5. 选择**部署为场解决方案**选项按钮，然后选择**完成**按钮以接受默认的本地 SharePoint 站点。

## <a name="add-a-web-part-to-the-project"></a>将 web 部件添加到项目

添加**Web 部件**到项目的项。 **Web 部件**项将添加 Web 部件代码文件。 更高版本，你会将代码添加到要呈现的 Web 部件内容的 Web 部件代码文件。

1. 在菜单栏上，依次选择“项目” > “添加新项”。

2. 在中**添加新项**对话框中**已安装的模板**窗格中，展开**SharePoint**节点，然后选择**2010年**节点。

3. 在 SharePoint 模板列表中，选择**Web 部件**模板，然后选择**添加**按钮。

     **Web 部件**项以显示**解决方案资源管理器**。

## <a name="rendering-content-in-the-web-part"></a>呈现在 web 部件中的内容

您可以指定你想要显示在 Web 部件中的将它们添加到 Web 部件类的控件集合的控件。

1. 在中**解决方案资源管理器**，打开*WebPart1.vb* （在 Visual Basic) 或*WebPart1.cs* （在 C# 中)。

     Web 部件代码文件将在代码编辑器中打开。

2. 将以下语句添加到 Web 部件代码文件的顶部。

     [!code-csharp[SP_WebPart#1](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#1)]
     [!code-vb[SP_WebPart#1](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#1)]

3. 向 `WebPart1` 类添加下面的代码。 此代码声明了以下字段：

   - 若要在 Web 部件中显示员工数据网格。

   - 用于筛选数据网格控件显示的文本。

   - 显示错误，如果数据网格是无法显示数据标签。

   - 一个字符串，包含员工数据文件的路径。

     [!code-csharp[SP_WebPart#2](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#2)]
     [!code-vb[SP_WebPart#2](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#2)]

4. 向 `WebPart1` 类添加下面的代码。 此代码将添加一个名为的自定义属性`DataFilePath`到 Web 部件。 自定义属性是可以由用户在 SharePoint 中设置的属性。 此属性获取和设置用于填充数据网格的 XML 数据文件的位置。

     [!code-csharp[SP_WebPart#3](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#3)]
     [!code-vb[SP_WebPart#3](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#3)]

5. 将 `CreateChildControls` 方法替换为以下代码。 这段代码执行下列任务：

   - 上一步中添加数据网格和声明的标签。

   - 将数据网格绑定到 XML 文件，其中包含员工数据。

     [!code-csharp[SP_WebPart#4](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#4)]
     [!code-vb[SP_WebPart#4](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#4)]

6. 将以下方法添加到 `WebPart1` 类。 这段代码执行下列任务：

   - 创建呈现的 Web 部件的 Web 部件谓词菜单中显示的谓词。

   - 处理在用户选择谓词菜单中的谓词时所引发的事件。 此代码筛选数据网格中显示的员工的列表。

     [!code-csharp[SP_WebPart#5](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#5)]
     [!code-vb[SP_WebPart#5](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#5)]

## <a name="test-the-web-part"></a>测试 web 部件

运行项目时，将打开 SharePoint 站点。 Web 部件会自动添加到在 SharePoint Web 部件库中。 您可以将 Web 部件添加到任何 Web 部件页。

1. 将以下 XML 粘贴到记事本文件。 此 XML 文件包含会在 Web 部件中显示的示例数据。

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

2. 在记事本中，在菜单栏上，选择**文件** > **另存为**。

3. 在中**另存为**对话框中**另存为类型**列表中，选择**的所有文件**。

4. 在中**文件名**框中，输入**data.xml**。

5. 通过选择任意文件夹**浏览文件夹**按钮，，然后选择**保存**按钮。

6. 在 Visual Studio 中，选择**F5**密钥。

     SharePoint 网站将打开。

7. 上**站点操作**菜单中，选择**更多选项**。

8. 在中**创建**页上，选择**Web 部件页**类型，然后选择**创建**按钮。

9. 在中**新的 Web 部件页**页上，将该页命名为**SampleWebPartPage.aspx**，然后选择**创建**按钮。

     将显示 Web 部件页。

10. 选择 Web 部件页面上的任何区域。

11. 在页面顶部，选择**插入**选项卡，然后选择**Web 部件**按钮。

12. 在中**类别**窗格中，选择**自定义**文件夹中，选择**WebPart1** Web 部件，然后选择**添加**按钮。

     Web 部件显示在此页。

## <a name="test-the-custom-property"></a>测试自定义属性

若要填充的数据网格中显示在 Web 部件中，指定包含有关每个雇员的数据的 XML 文件的路径。

1. 选择显示 Web 部件，右侧的箭头，然后选择**编辑 Web 部件**从显示的菜单。

     包含 Web 部件的属性窗格显示在页面的右侧。

2. 在窗格中，展开**杂项**节点，输入前面创建的 XML 文件的路径，选择**应用**按钮，，然后选择**确定**按钮。

     验证在 Web 部件中显示的员工列表。

## <a name="test-the-web-part-verb"></a>测试 web 部件谓词

显示和隐藏通过单击 Web 部件谓词菜单中显示的项不是经理的员工。

1. 选择显示 Web 部件，右侧的箭头，然后选择**仅显示经理**从显示的菜单。

     只有是经理的员工显示在 Web 部件。

2. 同样，选择箭头，然后选择**显示所有员工**从显示的菜单。

     在 Web 部件中显示所有员工。

## <a name="see-also"></a>请参阅

[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)
[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
[演练：使用设计器为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
