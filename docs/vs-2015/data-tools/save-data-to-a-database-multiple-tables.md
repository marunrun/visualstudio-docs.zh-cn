---
title: 将数据保存到数据库 （多个表） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 132aa0f37cc63e6afe2eff61a6d0f6dec5b200b5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692451"
---
# <a name="save-data-to-a-database-multiple-tables"></a>将数据保存到数据库（多个表）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

应用程序开发中最常用方案之一是在 Windows 应用程序窗体上显示数据、编辑数据并将更新后的数据发回数据库。 本演练创建可显示两个相关表的数据的窗体，并显示如何编辑记录和将更改保存回数据库。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。  
  
 通过调用 TableAdapter 的 `Update` 方法，可以将应用程序中的数据保存回数据库。 当您将从表**数据源**自动添加到窗体，将数据保存所需的代码窗口。添加到窗体的任何其他表需要手动添加此代码。 本演练显示了如何添加从多个表保存更新的代码。  
  
> [!NOTE]
> 对话框和菜单命令可能不同于所述的帮助，具体取决于您现用的设置或正在使用的版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 本演练涉及以下任务：  
  
- 创建一个新**Windows 应用程序**项目。  
  
- 创建和使用应用程序中配置数据源[数据源配置向导](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)。  
  
- 设置控件中的项[数据源窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。  
  
- 通过将某些项从“数据源”窗口拖动到窗体上来创建数据绑定控件。  
  
- 修改数据集中每个表中的几个记录。  
  
- 修改用于将数据集中的更新后的数据发回数据库的代码。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你将需要：  
  
- 能够访问 Northwind 示例数据库。
  
## <a name="create-the-windows-application"></a>创建 Windows 应用程序  
 第一步是创建**Windows 应用程序**。 在此步骤中，向项目分配名称是可选的但我们将在您因为我们计划稍后保存为它提供一个名称。  
  
#### <a name="to-create-the-new-windows-application-project"></a>若要创建新的 Windows 应用程序项目  
  
1. 上**文件**菜单中，创建一个新项目。  
  
2. 将项目命名为 `UpdateMultipleTablesWalkthrough`。  
  
3. 选择**Windows 应用程序**，然后选择**确定**。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。  
  
     创建“UpdateMultipleTablesWalkthrough”项目并将其添加到“解决方案资源管理器”中。  
  
## <a name="create-the-data-source"></a>创建数据源  
 此步骤使用“数据源配置向导”从 Northwind 数据库创建一个数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。
  
#### <a name="to-create-the-data-source"></a>创建数据源  
  
1. 上**数据**菜单中，选择**显示数据源**。  
  
2. 在中**数据源**窗口中，选择**添加新数据源**以启动**数据源配置向导**。  
  
3. 上**选择数据源类型**屏幕上，选择**数据库**，然后选择**下一步**。  
  
4. 上**选择您的数据连接**屏幕执行下列任一操作：  
  
    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。  
  
         或  
  
    - 选择“新建连接”，打开“添加/修改连接”对话框。  
  
5. 如果你的数据库需要密码，选择选项以包括敏感数据，然后选择**下一步**。  
  
6. 上**将连接字符串保存到应用程序配置文件**，选择**下一步**。  
  
7. 上**选择数据库对象**屏幕上，展开**表**节点。  
  
8. 选择**客户**并**订单**表，并选择**完成**。  
  
     “NorthwindDataSet”将添加到项目，这些表将显示在“数据源”窗口中。  
  
## <a name="set-the-controls-to-be-created"></a>设置要创建的控件  
 对于本演练中的数据`Customers`表位于**详细信息**，数据显示在单独控件中的布局。 将数据从`Orders`表位于**网格**中显示的布局<xref:System.Windows.Forms.DataGridView>控件。  
  
#### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>设置“数据源”窗口中项的拖放类型  
  
1. 在中**数据源**窗口中，展开**客户**节点。  
  
2. 上**客户**节点中，选择**详细信息**从要更改的控件的控件列表**客户**为单个控件的表。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。  
  
## <a name="create-the-data-bound-form"></a>创建数据绑定窗体  
 通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>在窗体上创建数据绑定控件  
  
1. 将主“Customers”节点从“数据源”窗口拖到“Form1”上。  
  
     带有描述性标签的数据绑定控件将显示在窗体上，同时还显示一个工具条 (<xref:System.Windows.Forms.BindingNavigator>)，用于在记录间进行导航。 组件栏中显示“[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)”、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。  
  
2. 将相关的“Orders”节点从“数据源”窗口拖到“Form1”上。  
  
    > [!NOTE]
    > 相关的“Orders”节点位于“Fax”列下，该节点是“Customers”节点的子节点。  
  
     用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 OrdersTableAdapter 和<xref:System.Windows.Forms.BindingSource>组件栏中出现。  
  
## <a name="addcode-to-update-the-database"></a>Addcode 来更新数据库  
 通过调用“Customers”和“Orders”TableAdapter 的 `Update` 方法，可更新数据库。 默认情况下，事件处理程序**保存**按钮的<xref:System.Windows.Forms.BindingNavigator>添加到窗体的代码以将更新发送到数据库。 此过程修改代码以将更新发送正确的顺序。这将消除产生引用完整性错误的可能性。 该代码还将通过在 try-catch 块中包装更新调用来实现错误处理。 可以根据应用程序的需要修改代码。  
  
> [!NOTE]
> 为清楚起见，本演练不使用事务。但是，如果要更新两个或多个相关表，包含在一个事务内的所有更新逻辑。 事务是一个过程，可确保提交任何更改之前，对数据库的所有相关的更改成功。 有关详细信息，请参阅[事务和并发性](https://msdn.microsoft.com/library/f46570de-9e50-4fe6-8710-a8c31fa8569b)。  
  
#### <a name="to-add-update-logic-to-the-application"></a>将更新逻辑添加到应用程序  
  
1. 选择**保存**按钮<xref:System.Windows.Forms.BindingNavigator>。这将打开到代码编辑器`bindingNavigatorSaveItem_Click`事件处理程序。  
  
2. 替换事件处理程序中的代码以调用相关 TableAdapter 的 `Update` 方法。 下面的代码首先创建三个临时数据表以保存每个 <xref:System.Data.DataRowState> 的更新信息（<xref:System.Data.DataRowState>、<xref:System.Data.DataRowState> 和 <xref:System.Data.DataRowState>）。 然后在正确的顺序运行更新。 代码应类似于：  
  
     [!code-csharp[VbRaddataSaving#10](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form4.cs#10)]
     [!code-vb[VbRaddataSaving#10](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form4.vb#10)]  
  
## <a name="test-the-application"></a>测试应用程序  
  
#### <a name="to-test-the-application"></a>测试应用程序  
  
1. 选择**F5**。  
  
2. 对每个表中的一条或多条记录的数据执行一些更改。  
  
3. 选择“保存”按钮。  
  
4. 检查数据库中的值以验证更改是否已保存。  
  
## <a name="next-steps"></a>后续步骤  
 具体取决于应用程序的要求，有可能想要在 Windows 应用程序中创建了数据绑定窗体后执行的几个步骤。 你可以通过以下操作来增强此演练的效果：  
  
- 将搜索功能添加到该窗体。 有关详细信息，请参阅[如何：参数化的查询到 Windows 窗体应用程序添加](https://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416)。  
  
- 编辑数据源以添加或移除数据库对象。 有关详细信息，请参阅[如何：编辑数据集](https://msdn.microsoft.com/library/f2dade5f-9c7a-4ddb-96a8-e0a39e50bfd3)。  
  
## <a name="see-also"></a>请参阅  
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
