---
title: 为 SharePoint 创建网站栏、内容类型和列表
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.ListDesigner.GeneralMessageHelp
- Microsoft.VisualStudio.SharePoint.Designers.ListDesigner.ViewModels.ListViewModel.SortingAndGrouping
- VS.SharePointTools.ListDesigner.SortingGrouping
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, list definitions
- SharePoint development in Visual Studio, list instances
- SharePoint development in Visual Studio, fields
- SharePoint development in Visual Studio, content types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cc6782e4a83f259eb17632addec36c7804b27858
ms.sourcegitcommit: 174c992ecdc868ecbf7d3cee654bbc2855aeb67d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74879343"
---
# <a name="walkthrough-create-a-site-column-content-type-and-list-for-sharepoint"></a>演练：为 SharePoint 创建网站栏、内容类型和列表
  下面的过程演示如何创建自定义 SharePoint 网站列（或*字段*）以及使用网站列的内容类型。 它还演示如何创建使用新内容类型的列表。

 本演练包含以下任务：

- [创建自定义网站列](#create-custom-site-columns)。

- [创建自定义内容类型](#create-a-custom-content-type)。

- [创建一个列表](#create-a-list)。

- [测试应用程序](#test-the-application)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 你需要以下组件来完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- [!INCLUDE[vsprvs-current](../sharepoint/includes/vsprvs-current-md.md)]

## <a name="create-custom-site-columns"></a>创建自定义网站列
 此示例将创建一个列表，用于管理医院中的患者。 首先，你必须在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建一个 SharePoint 项目并向其添加网站列，如下所示。

#### <a name="to-create-the-project"></a>要创建项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**文件**"菜单上，选择"**新建** > **项目**"。
::: moniker range="=vs-2017"
2. 在 "**新建项目**" 对话框中的 "**视觉C#对象**" 或 " **Visual Basic**" 下，展开 " **Office/SharePoint** " 节点，然后选择 " **SharePoint 解决方案**"。

3. 在 "**模板**" 窗格中，为已安装的特定 sharepoint 版本选择**sharepoint 空项目**。 例如，如果您有 SharePoint 2016 安装，请选择**sharepoint 2016-空项目**模板。  

4. 将项目名称更改为 "**诊所**"，然后选择 **"确定"** 按钮。

5. 在 "**指定用于调试的站点和安全级别**" 对话框中，输入要向其添加新的自定义字段项的本地 SharePoint 站点的 URL，或者使用默认位置（`http://<`*SystemName*`>/)`。

6. 在 "**此 SharePoint 解决方案的信任级别是什么？** " 部分中，使用 "**部署为沙盒解决方案**的默认值"。

     有关沙盒解决方案和场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 单击“完成”按钮。 项目现已在**解决方案资源管理器**中列出。
::: moniker-end
::: moniker range=">=vs-2019"
2.  在 "**创建新项目**" 对话框中，为已安装的特定 sharepoint 版本选择**sharepoint 空项目**。 例如，如果您有 SharePoint 2016 安装，请选择**sharepoint 2016-空项目**模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 将项目名称更改为 "**诊所**"，然后选择 "**创建**" 按钮。

4. 在 "**指定用于调试的站点和安全级别**" 对话框中，输入要向其添加新的自定义字段项的本地 SharePoint 站点的 URL，或者使用默认位置（`http://<`*SystemName*`>/)`。

5. 在 "**此 SharePoint 解决方案的信任级别是什么？** " 部分中，使用 "**部署为沙盒解决方案**的默认值"。

     有关沙盒解决方案和场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

6. 单击“完成”按钮。 项目现已在**解决方案资源管理器**中列出。
::: moniker-end

#### <a name="to-add-site-columns"></a>添加网站列

1. 添加新的网站列。 为此，请在**解决方案资源管理器**中右键单击 "**诊所**" 项目，然后选择 "**添加** > **新项**"。

2. 在 "**添加新项**" 对话框中，选择 "**网站列**"，将 "名称" 更改为**PatientName**，然后选择 "**添加**" 按钮。

3. 在站点列的 "*元素 .xml* " 文件中，将 "**类型**" 设置保留为 "**文本**"，将 "**组**" 设置更改为 "**诊所站点列**"。 完成后，站点列的*元素 .xml*文件应类似于下面的示例。

    ```xml
    <Field
         ID="{f9ba60d1-5631-41fb-b016-a38cf48eef63}"
         Name="PatientName"
         DisplayName="Patient Name"
         Type="Text"
         Required="FALSE"
         Group="Clinic Site Columns">
    </Field>
    ```

    > [!TIP]
    > 如果在网站列名称中使用 camel 大小写，则 Visual Studio 将在 DisplayName 中自动添加一个空格。
    > 建议不要在站点列名称中使用空格，因为当你尝试将解决方案部署到 SharePoint 时，它可能会导致问题。

4. 使用相同的过程，将两个以上的网站列添加到项目： **PatientID** （type = "Integer"）和**DoctorName** （type = "Text"）。 将其组值设置为**诊所网站列**。

## <a name="create-a-custom-content-type"></a>创建自定义内容类型
 接下来，根据联系人内容类型创建内容类型，其中包括你在上一过程中创建的网站列。 通过将内容类型基于现有内容类型，可以节省时间，因为基内容类型提供了多个可在新内容类型中使用的网站列。

#### <a name="to-create-a-custom-content-type"></a>创建自定义内容类型

1. 向项目中添加内容类型。 为此，请在**解决方案资源管理器**中选择 "项目" 节点

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在 "**视觉C#对象**" 或 " **Visual Basic**" 下，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在 "**模板**" 窗格中，选择 "**内容类型**" 模板，将 "名称" 更改为 "**患者信息**"，然后选择 "**添加**" 按钮。

     " **SharePoint 自定义向导**" 随即打开。

5. 在 "**此内容类型应从其继承**" 列表中，选择 "**联系人**" 作为新内容类型所基于的内容类型，然后选择 "**完成**" 按钮。

     这样，你就可以访问联系人内容类型中其他可能有用的网站列，此外还提供你之前定义的网站列。

6. 显示内容类型设计器后，在 "**列**" 选项卡中添加前面定义的三个站点列：**患者名称**、**患者 ID**和**医生名称**。 若要添加这些列，请在 "**显示名称**" 下的 "站点列" 列表中选择第一个列表框，然后在列表中一次选择一个网站列。

    > [!TIP]
    > 若要更快地选择网站列，请通过输入列名称的前几个字母来筛选该列表。

7. 除了三个自定义站点列外，还可以从 "站点列" 列表中添加 "**注释**站点" 列。

8. 对于 "**患者名称**" 和 "**患者 ID** " 网站列选中 "**必需**" 复选框，以使其成为必填字段。

9. 在 "**内容类型**" 选项卡上，确保内容类型名称为 "**患者信息**"，然后将说明更改为 "**患者信息卡**"。

10. 将**组名称**更改为**诊所内容类型**，将其他设置保留为其默认值。

11. 在菜单栏上，选择 "**文件**" > "**全部保存**"，然后关闭内容类型设计器。

## <a name="create-a-list"></a>创建列表
 现在，创建一个使用新的 "内容类型" 和 "站点" 列的列表。

#### <a name="to-create-a-list"></a>创建列表

1. 向项目添加一个列表。 为此，请在**解决方案资源管理器**中选择项目节点。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在 "**视觉C#对象**" 或 " **Visual Basic**" 下，展开 " **SharePoint** " 节点。

4. 在 "**模板**" 窗格中，选择**列表**模板，将 "名称" 更改为 "**患者**"，然后选择 "**添加**" 按钮。

5. 保留 "**基于默认设置自定义**列表" **（自定义列表）** ，然后选择 "**完成**" 按钮。

6. 在列表设计器中，选择 "**内容类型**" 按钮以显示 "**内容类型设置**" 对话框。

7. 选择新行，在内容类型列表中选择 "**患者信息**" 内容类型，然后选择 **"确定"** 按钮。

     执行此操作会将**患者信息**内容类型的所有网站列添加到列表中。

8. 删除列表中除以下内容之外的所有网站列：

    - 患者 ID

    - 患者名称

    - 住宅电话

    - 电子邮件

    - 医生名称

    - Comments

9. 在 "**列显示名称**" 下，选择一个空行，添加自定义列表列，然后将其命名为 "**医院**"。 将其数据类型保留为**单行文本**。

     自定义列表列仅适用于此列表。 将自定义列表列添加到列表中时，将创建新的列表内容类型（包括添加到列表中的所有列）并将其设置为默认列表。

    > [!TIP]
    > 如果从站点列列表中选择某一列，则将使用现有的网站列。 但是，如果在不选择列表中的任何列的情况下输入列名称值，则将创建自定义列表列，即使列表中已存在同名的列也是如此。

     您可以根据需要将此列的数据类型设置为 "查找"，而不是将自定义列表列的数据类型**设置为 "** 查找"，而是从表或其他列表中检索其值。 有关查找列的信息，请参阅[在 SharePoint 2010 中列出关系](/previous-versions/msp-n-p/ff798514(v=pandp.10))和[查找和列表关系](/previous-versions/office/developer/sharepoint-2010/ff623048(v=office.14))。

10. 在 "**患者 ID** " 和 "**患者名称**" 框旁边，选中 "**必需**" 复选框。

11. 在 "**视图**" 选项卡上，选择一个空行来创建视图。 在 "**视图名称**" 列下的空白行中输入**患者详细信息**。

     在 "**视图**" 选项卡上，可以指定要在 SharePoint 列表中显示的列。

12. 选择新的 "**患者详细信息**" 行，然后选择 "**设为默认值**" 按钮。

     新视图现在为该列表的默认视图。

13. 按照以下顺序将以下列添加到 "**所选列**" 列表中：

    - 患者 ID

    - 患者名称

    - 住宅电话

    - 电子邮件

    - 医生名称

    - 医院

    - Comments

14. 在 "**属性**" 列表中，选择 "**排序和分组**" 属性，然后选择省略号按钮![省略号图标](../sharepoint/media/ellipsisicon.gif "“省略号”图标")以显示 "**排序和分组**" 对话框。

15. 在 "**列名称**" 列表中，选择 "**患者名称**"，确保 "**排序依据**" 列设置为 "**升序**"，然后选择 **"确定"** 按钮。

## <a name="test-the-application"></a>测试应用程序
 自定义网站列、内容类型和列表就绪后，请将其部署到 SharePoint 并运行应用程序进行测试。

#### <a name="to-test-the-application"></a>测试应用程序

1. 在菜单栏上，依次选择“文件” > “全部保存”。

2. 选择**F5**键以运行应用程序。

     将编译应用程序，然后将其功能部署到 SharePoint 并激活。

3. 在快速导航栏上，选择 "**患者**" 链接以显示**患者**列表。

     列表中的列名应与您在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中的 "**视图**" 选项卡上输入的名称相匹配。

4. 选择 "**添加新项**" 链接以创建患者信息卡。

5. 在字段中输入信息，然后选择 "**保存**" 按钮。

     新记录将显示在列表中。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [如何：创建自定义字段类型](/previous-versions/office/developer/sharepoint-2010/bb862248(v=office.14))
- [内容类型](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))
- [“列”](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))
