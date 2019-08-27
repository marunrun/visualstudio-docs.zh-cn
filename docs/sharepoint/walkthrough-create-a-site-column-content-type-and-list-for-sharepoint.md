---
title: 创建 SharePoint 网站栏、 内容类型和列表
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
ms.openlocfilehash: 141ce92fa083a0afacdae3a279d2697e0931e3be
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401272"
---
# <a name="walkthrough-create-a-site-column-content-type-and-list-for-sharepoint"></a>演练：创建 SharePoint 网站栏、 内容类型和列表
  以下过程演示如何创建自定义 SharePoint 站点列，或*字段*— 以及使用的站点列的内容类型。 它还演示如何创建使用新的内容类型的列表。

 本演练包含以下任务：

- [创建自定义站点列](#create-custom-site-columns)。

- [创建自定义内容类型](#create-a-custom-content-type)。

- [创建列表](#create-a-list)。

- [测试应用程序](#test-the-application)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- [!INCLUDE[vsprvs-current](../sharepoint/includes/vsprvs-current-md.md)]

## <a name="create-custom-site-columns"></a>创建自定义站点列
 此示例创建用于管理在医院患者列表。 首先，必须创建 SharePoint 项目中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]并将站点列添加到它，如下所示。

#### <a name="to-create-the-project"></a>要创建项目

1. 上[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**文件**菜单中，选择**新建** > **项目**。

2. 在中**新的项目**对话框中的，在**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**。

3. 在中**模板**窗格中，选择**SharePoint 2010 项目**，更改到项目的名称**Clinic**，然后选择**确定**按钮。

     SharePoint 2010 项目模板是此示例中使用站点列和更高版本添加其他项目项包含一个空项目。

4. 上**指定用于调试的网站和安全级别**页上，输入你想要添加的新的自定义字段项的本地 SharePoint 站点的 URL 或使用默认位置 (`http://<`*SystemName*`>/)`.

5. 在中**此 SharePoint 解决方案的信任级别是什么？** 部分中，使用默认值**部署为沙盒解决方案**。

     有关沙盒的详细信息和场解决方案，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

6. 选择**完成**按钮。 项目现已列入**解决方案资源管理器**。

#### <a name="to-add-site-columns"></a>若要添加的站点列

1. 添加新的站点列。 若要执行此操作，在**解决方案资源管理器**，打开快捷菜单**Clinic**，然后选择**添加** > **新项**。

2. 在中**添加新项**对话框框中，选择**站点列**，将名称更改为**患者名称**，然后选择**添加**按钮。

3. 中的站点列*Elements.xml*文件中，将保留**类型**设置为**文本**，并将更改**组**设置为**Clinic 站点列**。 完成后，网站栏*Elements.xml*文件应如以下示例所示。

    ```xml
    <Field
         ID="{f9ba60d1-5631-41fb-b016-a38cf48eef63}"
         Name="Clinic - Patient Name"
         DisplayName="Patient Name"
         Type="Text"
         Required="FALSE"
         Group="Clinic Site Columns">
    </Field>
    ```

4. 使用相同的过程，将两个站点列添加到项目：**患者 ID** (类型 ="Integer") 和**医生名称**(类型 ="Text")。 将其组值设置为**Clinic 站点列**。

## <a name="create-a-custom-content-type"></a>创建自定义内容类型
 接下来，创建一个内容类型-基于联系人内容类型-包括前一过程中创建的站点列。 通过使基于现有内容类型的内容类型，可以节省时间，因为基内容类型提供了新的内容类型中使用多个站点列。

#### <a name="to-create-a-custom-content-type"></a>若要创建自定义内容类型

1. 向项目添加内容类型。 若要执行此操作，在**解决方案资源管理器**，选择项目节点

2. 在菜单栏上，依次选择“项目”   > “添加新项”  。

3. 下**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**节点。

4. 在中**模板**窗格中，选择**内容类型**模板中，将名称更改为**患者信息**，然后选择**添加**按钮。

     **SharePoint 自定义向导**随即打开。

5. 在中**基内容类型应此内容类型继承自**列表中，选择**联系人**作为内容类型上要基于新的内容类型，然后选择**完成**按钮。

     执行此操作使您可以访问到联系人内容类型，除了以前定义的站点列中的其他可能有用的站点列。

6. 内容类型设计器显示后，在**列**选项卡上，添加三个站点以前定义的列：**患者名称**，**患者 ID**，和**医生名称**。 若要添加这些列，请选择第一个列表框下的站点列列表中**显示名称**，然后选择每个站点列列表中一次。

    > [!TIP]
    > 若要更快地选择站点列，请通过输入的列的名称的第几个字母筛选列表。

7. 三个自定义站点列，以及添加**注释**站点列列表中的站点列。

8. 选择**必需**复选框**患者名称**并**患者 ID**站点列，以使其必填字段。

9. 上**Content-type**选项卡上，请确保内容类型名称是**患者信息**，然后将更改到说明**患者信息卡**。

10. 更改**组名称**到**讨论会内容类型**，并将其他设置保留为其默认值。

11. 在菜单栏上依次选择**文件** > **全部保存**，然后关闭内容类型设计器。

## <a name="create-a-list"></a>创建列表
 现在，创建一个列表，其中使用新的内容类型和站点列。

#### <a name="to-create-a-list"></a>若要创建的列表

1. 添加到项目的列表。 若要执行此操作，在**解决方案资源管理器**，选择项目节点。

2. 在菜单栏上，依次选择“项目”   > “添加新项”  。

3. 下**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**节点。

4. 在中**模板**窗格中，选择**列表**模板中，将名称更改为**患者**，然后选择**添加**按钮。

5. 将保留**自定义列表依据**设置为**默认 （空）** ，然后选择**完成**按钮。

6. 在列表设计器中，选择**内容类型**按钮以显示**内容类型设置**对话框。

7. 选择新行，然后选择**患者信息**内容类型列表中的内容类型，然后选择**确定**按钮。

     执行此操作将添加的所有站点列从**患者信息**内容到列表的类型。

8. 删除的所有站点列在列表中，以下除外：

    - 患者 ID

    - 患者的名称

    - 家庭电话

    - 电子邮件

    - 医生名称

    - 注释

9. 下**列显示名称**、 选择空的行，添加自定义列表列，并将其命名**医院**。 将作为其数据类型保留**单个文本行**。

     自定义列表列仅适用于此列表。 当将自定义列表列添加到列表中时，新列表的内容类型，包括添加到列表中，所有列创建，并设置为默认列表。

    > [!TIP]
    > 如果从站点列的列表中选择一列，则使用现有站点列。 但是，如果您输入的列名称值而不在列表中选择任何列，自定义列表创建列后，即使列表中已存在具有相同名称的列。

     （可选） 而不是设置的自定义列表列的数据类型**单个文本行**，可以改为将此列的数据类型为查找，并将从表或另一个列表检索其值。 有关查找列的信息，请参阅[SharePoint 2010 中的列表关系](http://go.microsoft.com/fwlink/?LinkId=224994)并[查找和列表关系](http://go.microsoft.com/fwlink/?LinkID=224995)。

10. 下一步**患者 ID**并**患者名称**框中，选择**所需**复选框。

11. 上**视图**选项卡上，选择一个空行以创建视图。 输入**患者的详细信息**。

     上**视图**选项卡上，可以指定你想要在 SharePoint 列表中显示的列。

12. 选择新**患者详细信息**行，，然后选择**设置为默认值**按钮。

     新视图现在会在列表的默认视图。

13. 添加到下列**选定列**按以下顺序的列表：

    - 患者 ID

    - 患者的名称

    - 家庭电话

    - 电子邮件

    - 医生名称

    - 医院

    - 注释

14. 在中**属性**列表中，选择**排序和分组**属性，然后选择省略号按钮![省略号图标](../sharepoint/media/ellipsisicon.gif "省略号图标")以显示**排序和分组**对话框。

15. 在**列名**列表中，选择**患者名称**，请确保**排序**列设置为**升序**，然后选择**确定**按钮。

## <a name="test-the-application"></a>测试应用程序
 现在，自定义站点列、 内容类型和列表准备就绪后，将其部署到 SharePoint，并运行应用程序对其进行测试。

#### <a name="to-test-the-application"></a>测试应用程序

1. 在菜单栏上，依次选择“文件”   > “全部保存”  。

2. 选择**F5**键以运行该应用程序。

     应用程序进行编译，并且然后部署到 SharePoint 和激活其功能。

3. 快速导航栏上选择**患者**链接以显示**患者**列表。

     在列表中的列名应匹配上输入的那些**视图**选项卡中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

4. 选择**添加新项**链接创建患者信息卡。

5. 在字段中输入的信息，然后选择**保存**按钮。

     列表中显示新记录。

## <a name="see-also"></a>请参阅
- [为 SharePoint 创建站点栏、 内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [如何：创建自定义字段类型](http://go.microsoft.com/fwlink/?LinkId=192079)
- [内容类型](http://go.microsoft.com/fwlink/?LinkId=192080)
- [列](http://go.microsoft.com/fwlink/?LinkId=192081)
