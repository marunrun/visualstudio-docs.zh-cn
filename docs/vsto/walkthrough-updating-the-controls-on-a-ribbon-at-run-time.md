---
title: 演练：更新在运行时功能区上的控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- updating Ribbon controls
- Ribbon [Office development in Visual Studio], dynamic menu
- dynamic menus [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e293a0136e6ae2d8b6a6747201e484fdea43f91e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62981109"
---
# <a name="walkthrough-update-the-controls-on-a-ribbon-at-runtime"></a>演练：更新在运行时功能区上的控件

本演练演示如何使用功能区对象模型在功能区加载到 Office 应用程序之后，更新功能区上的控件。

[!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

此示例提取来自 Northwind 示例数据库的数据，以填充 Microsoft Office Outlook 中的组合框和菜单。 这些控件中自动选择的项填充字段，如**到**并**主题**的电子邮件中。

本演练阐释了以下任务：

- 创建新的 Outlook VSTO 外接程序项目。

- 设计自定义功能区组。

- 将自定义组添加到内置选项卡。

- 更新在运行时在功能区上的控件。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

首先，创建 Outlook VSTO 外接程序项目。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

1. 在中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，创建一个 Outlook VSTO 外接程序项目名称**为 Ribbon_Update_At_Runtime**。

2. 在 **“新建项目”** 对话框中，选择 **“创建解决方案的目录”**。

3. 将项目保存到默认项目目录中。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

## <a name="design-a-custom-ribbon-group"></a>设计自定义功能区组

当用户撰写一封新邮件时，将显示此示例中的功能区。 若要创建功能区自定义组，请首先将功能区项添加到你的项目，然后设计功能区设计器中的组。 此自定义组将帮助您通过拉取名称生成跟进电子邮件消息给客户和订单历史记录数据库中。

### <a name="to-design-a-custom-group"></a>设计自定义组

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”**。

3. 更改到新的功能区的名称**CustomerRibbon**，然后单击**添加**。

     *CustomerRibbon.cs*或*CustomerRibbon.vb*文件将在功能区设计器中打开并显示一个默认选项卡和组。

4. 单击功能区设计器以将其选定。

5. 在中**属性**窗口中，单击下拉箭头旁边**RibbonType**属性，，然后单击**Microsoft.Outlook.Mail.Compose**。

     这样，当用户撰写一封新邮件在 Outlook 中的时，显示功能区。

6. 在功能区设计器中，单击**Group1**以将其选中。

7. 在中**属性**窗口中，将**标签**到**客户采购**。

8. 从**Office 功能区控件**选项卡**工具箱**，将**组合框**拖到**客户采购**组。

9. 单击**ComboBox1**以将其选中。

10. 在中**属性**窗口中，将**标签**到**客户**。

11. 从**Office 功能区控件**选项卡**工具箱**，将**菜单**拖到**客户采购**组。

12. 在中**属性**窗口中，将**标签**到**产品购买**。

13. 设置**动态**到**true**。

     这使您可以添加和删除功能区加载到 Office 应用程序后，会在运行时的菜单上的控件。

## <a name="add-the-custom-group-to-a-built-in-tab"></a>将自定义组添加到内置选项卡

内置选项卡是已在 Outlook 资源管理器或检查器的功能区选项卡。 在此过程中，将自定义组添加到内置选项卡，然后指定自定义组在选项卡上的位置。

### <a name="to-add-the-custom-group-to-a-built-in-tab"></a>将自定义组添加到内置选项卡

1. 单击**TabAddins （内置）** 选项卡以选择它。

2. 在中**属性**窗口中，展开**ControlId**属性，且然后将设置**OfficeId**到**TabNewMailMessage**。

     这将添加**客户采购**组，以便**消息**新邮件消息中出现的功能区选项卡。

3. 单击**客户采购**组以将其选中。

4. 在**属性**窗口中，展开**位置**属性中，单击下拉箭头旁边**PositionType**属性，，然后单击**BeforeOfficeId**。

5. 设置**OfficeId**属性设置为**groupclipboard**。

     这将定位**客户采购**组之前**剪贴板**组**消息**选项卡。

## <a name="create-the-data-source"></a>创建数据源

使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-create-the-data-source"></a>创建数据源

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

     这将启动**数据源配置向导**。

2. 选择**数据库**，然后单击**下一步**。

3. 选择**数据集**，然后单击**下一步**。

4. 选择与 Northwind 示例 Microsoft SQL Server Compact 4.0 数据库的数据连接或通过添加新的连接**新的连接**按钮。

5. 选择或创建连接后，单击**下一步**。

6. 单击**下一步**保存连接字符串。

7. 上**选择数据库对象**页上，展开**表**。

8. 选中以下每个表格旁的复选框：

    1. **客户**

    2. **订单详细信息**

    3. **订单**

    4. **产品**

9. 单击 **“完成”**。

## <a name="update-controls-in-the-custom-group-at-runtime"></a>更新在运行时自定义组中的控件

使用功能区对象模型执行以下任务：

- 添加到的客户名称**客户**组合框。

- 添加到菜单和按钮控件**产品购买**菜单表示销售订单和产品的销售。

- 填充收件人、 主题和正文的新邮件消息的使用中的数据字段**客户**组合框和**产品购买**菜单。

### <a name="to-update-controls-in-the-custom-group-by-using-the-ribbon-object-model"></a>使用功能区对象模型更新自定义组中的控件

1. 在“项目”菜单上，单击“添加引用”。

2. 在中**添加引用**对话框中，单击 **.NET**选项卡上，选择**System.Data.Linq**程序集，然后单击**确定**。

    此程序集包含有关使用语言集成查询 (LINQ) 的类。 你将通过 LINQ 使用 Northwind 数据库中的数据填充自定义组中的控件。

3. 在中**解决方案资源管理器**，单击**CustomerRibbon.cs**或**CustomerRibbon.vb**以将其选中。

4. 上**视图**菜单上，单击**代码**。

    功能区代码文件将在代码编辑器中打开。

5. 将下面的语句添加到功能区代码文件的顶部。 通过执行这些语句，可轻松访问 LINQ 命名空间和 Outlook 主互操作程序集 (PIA) 的命名空间。

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#1](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#1)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#1](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#1)]

6. 将以下代码添加`CustomerRibbon`类。 此代码声明了将用于存储 Northwind 数据库的“客户”、“订单”、“订单明细”和“产品”表中信息的数据表和表适配器。

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#2](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#2)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#2](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#2)]

7. 将以下代码块添加到 `CustomerRibbon` 类中。 此代码将添加在运行时创建的功能区控件的三个帮助器方法。

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#3](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#3)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#3](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#3)]

8. 将 `CustomerRibbon_Load` 事件处理程序方法替换为以下代码。 此代码使用 LINQ 查询执行以下任务：

   - 填充**客户**组合框使用 Northwind 数据库中的 ID 和 20 位客户的名称。

   - 调用 `PopulateSalesOrderInfo` 帮助程序方法。 此方法会更新**ProductsPurchased**菜单，其中包含与当前所选客户相关的销售订单号。

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#4](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#4)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#4](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#4)]

9. 向 `CustomerRibbon` 类添加下面的代码。 此代码使用 LINQ 查询执行以下任务：

   - 将添加到子菜单**ProductsPurchased**与所选客户相关的每个销售订单的菜单。

   - 将按钮添加到与销售订单相关的产品的每个子菜单中。

   - 将事件处理程序添加到每个按钮。

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#6](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#6)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#6](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#6)]

10. 在中**解决方案资源管理器**，双击功能区代码文件。

     功能区设计器随即打开。

11. 在功能区设计器中，双击**客户**组合框。

     功能区代码文件将在代码编辑器中打开，并且将显示 `ComboBox1_TextChanged` 事件处理程序。

12. 将 `ComboBox1_TextChanged` 事件处理程序替换为以下代码。 这段代码执行下列任务：

    - 调用 `PopulateSalesOrderInfo` 帮助程序方法。 此方法会更新**产品购买**菜单，其中包含与所选客户相关的销售订单。

    - 调用 `PopulateMailItem` 帮助程序方法并传入当前文本，该文本是所选客户名称。 此方法填充收件人、 主题和正文的新邮件消息的字段。

      [!code-csharp[Trin_Ribbon_Update_At_Runtime#5](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#5)]
      [!code-vb[Trin_Ribbon_Update_At_Runtime#5](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#5)]

13. 向 `Click` 类添加以下 `CustomerRibbon` 事件处理程序。 此代码添加到新邮件消息的正文字段所选产品的名称。

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#8](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#8)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#8](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#8)]

14. 向 `CustomerRibbon` 类添加下面的代码。 这段代码执行下列任务：

    - 通过使用当前所选客户的电子邮件地址，从而填充新邮件消息收件人行。

    - 将文本添加到新邮件消息的主题和正文字段。

      [!code-csharp[Trin_Ribbon_Update_At_Runtime#7](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#7)]
      [!code-vb[Trin_Ribbon_Update_At_Runtime#7](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#7)]

## <a name="test-the-controls-in-the-custom-group"></a>测试自定义组中的控件

自定义组时在 Outlook 中打开一个新的邮件窗体，名为**客户采购**上将显示**消息**功能区选项卡。

若要创建客户跟进电子邮件消息，请选择一个客户，然后选择客户所购买的产品。 中的控件**客户采购**组更新在运行时使用 Northwind 数据库中的数据。

### <a name="to-test-the-controls-in-the-custom-group"></a>测试自定义组中的控件

1. 按**F5**运行你的项目。

     Outlook 启动。

2. 在 Outlook 中，在**文件**菜单，依次指向**新建**，然后单击**邮件**。

     执行下列操作：

    - 出现新的邮件消息检查器窗口。

    - 上**消息**功能区选项卡**客户采购**组显示之前**剪贴板**组。

    - **客户**组中的组合框使用 Northwind 数据库中的客户名称进行更新。

3. 上**消息**功能区选项卡，在**客户采购**组中，选择的一位客户**客户**组合框。

     执行下列操作：

    - **产品购买**菜单进行更新，以显示所选客户的每个销售订单。

    - 每笔销售订单子菜单进行更新，以显示该笔订单中购买的产品。

    - 所选的客户的电子邮件地址添加到**到**行的邮件消息中的主题和电子邮件的正文使用文本进行填充。

4. 单击**Products Purchases**菜单上，指向任一销售订单，然后单击销售订单中的产品。

     该产品名称将添加到邮件消息的正文中。

## <a name="next-steps"></a>后续步骤

可从以下主题了解有关如何自定义 Office 用户界面的更多信息：

- 将基于上下文的 UI 添加到任何文档级自定义项。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

- 扩展标准的或自定义的 Microsoft Office Outlook 窗体。 有关详细信息，请参见[演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)。

- 将自定义任务窗格添加到 Outlook。 有关详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

## <a name="see-also"></a>请参阅

- [在运行时在功能区的访问](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [语言集成查询 (LINQ)](/dotnet/csharp/linq/index)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)
- [为 Outlook 中自定义功能区](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：将控件添加到 Backstage 视图](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)