---
title: 在事务中保存数据 |Microsoft Docs
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
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b30f51da001c62166a97c954b1416e35fd8b540f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671092"
---
# <a name="save-data-in-a-transaction"></a>在事务中保存数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何使用 <xref:System.Transactions> 命名空间在事务中保存数据。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。

## <a name="prerequisites"></a>Prerequisites
 本演练需要对 Northwind 示例数据库的访问权限。

## <a name="create-a-windows-application"></a>创建 Windows 应用程序
 第一步是创建**Windows 应用程序**。

#### <a name="to-create-the-new-windows-project"></a>创建新的 Windows 项目

1. 在 Visual Studio 中的 "**文件**" 菜单上，创建一个新**项目**。

2. 将项目命名为**SavingDataInATransactionWalkthrough**。

3. 选择 " **Windows 应用程序**"，然后选择 **"确定"** 。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。

     创建“SavingDataInATransactionWalkthrough”项目并将其添加到“解决方案资源管理器”中。

## <a name="create-a-database-data-source"></a>创建数据库数据源
 此步骤使用 "[数据源配置向导](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)" 创建基于 Northwind 示例数据库中的 `Customers` 和 `Orders` 表的数据源。

#### <a name="to-create-the-data-source"></a>创建数据源

1. 在 "**数据**" 菜单上，选择 "**显示数据源**"。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在 "**选择数据源类型**" 屏幕上，选择 "**数据库**"，然后选择 "**下一步**"。

4. 在 "**选择你的数据连接**" 屏幕上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         或

    - 选择“新建连接”以启动“添加/修改连接”对话框，并创建到 Northwind 数据库的连接。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，然后选择 "**下一步**"。

6. 在 "将**连接字符串保存到应用程序配置文件**" 屏幕上，选择 "**下一步**"。

7. 在 "**选择数据库对象**" 屏幕上，展开 "**表**" 节点。

8. 选择 `Customers` 和 `Orders` 表，然后选择 "**完成**"。

     将“NorthwindDataSet”添加到项目后，“数据源”窗口即会显示 `Customers` 和 `Orders` 表。

## <a name="addcontrols-to-the-form"></a>Addcontrols 窗体
 通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。

#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>在 Windows 窗体上创建数据绑定控件

- 在 "**数据源**" 窗口中，展开 " **Customers** " 节点。

- 将主“Customers”节点从“数据源”窗口拖到“Form1”上。

     用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 组件栏中显示“[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)”、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

- 将相关的 " **orders** " 节点（而非 "主**订单**" 节点，但 " **Fax** " 列下的相关子表节点）拖到**CustomersDataGridView**下的窗体中。

     窗体上显示一个 <xref:System.Windows.Forms.DataGridView>。 组件栏中会显示 OrdersTableAdapter 和 <xref:System.Windows.Forms.BindingSource>。

## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>添加对 System.web 程序集的引用
 事务使用 <xref:System.Transactions> 命名空间。 默认情况下，不会添加对系统. 事务程序集的项目引用，因此您需要手动添加它。

#### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>添加对 System.Transactions DLL 文件的引用

1. 在 "**项目**" 菜单上，选择 "**添加引用**"。

2. 选择 "**系统事务**" （位于 " **.net** " 选项卡上），然后选择 **"确定"** 。

     将“System.Transactions”的引用添加到项目。

## <a name="modifythe-code-in-the-bindingnavigators-saveitem-button"></a>BindingNavigator 的 SaveItem 按钮中的 Modifythe 代码
 对于拖放到窗体上的第一个表，默认情况下，会将代码添加到 <xref:System.Windows.Forms.BindingNavigator> 上的 "保存" 按钮的 `click` 事件。 你需要手动添加代码以更新所有附加的表。 对于本演练，我们将重构保存按钮的单击事件处理程序中的现有保存代码。另外，还创建了一些方法，以根据是否需要添加或删除行来提供特定的更新功能。

#### <a name="to-modify-the-auto-generated-save-code"></a>修改自动生成的保存代码

1. 选择**CustomersBindingNavigator**上的 "**保存**" 按钮（带有软盘图标的按钮）。

2. 将 `CustomersBindingNavigatorSaveItem_Click` 方法替换为以下代码：

    [!code-csharp[VbRaddataSaving#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#4)]
    [!code-vb[VbRaddataSaving#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#4)]

   对相关数据的协调更改的顺序如下：

- 删除子记录。 （在这种情况下，请从 `Orders` 表中删除记录。）

- 删除父记录。 （在这种情况下，请从 `Customers` 表中删除记录。）

- 插入父记录。（在这种情况下，请在 `Customers` 表中插入记录。）

- 插入子记录。 （在这种情况下，请在 `Orders` 表中插入记录。）

#### <a name="to-delete-existing-orders"></a>删除现有顺序

- 将以下 `DeleteOrders` 方法添加到“Form1”：

     [!code-csharp[VbRaddataSaving#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#5)]
     [!code-vb[VbRaddataSaving#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#5)]

#### <a name="to-delete-existing-customers"></a>删除现有客户

- 将以下 `DeleteCustomers` 方法添加到“Form1”：

     [!code-csharp[VbRaddataSaving#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#6)]
     [!code-vb[VbRaddataSaving#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#6)]

#### <a name="to-add-new-customers"></a>添加新客户

- 将以下 `AddNewCustomers` 方法添加到“Form1”：

     [!code-csharp[VbRaddataSaving#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#7)]
     [!code-vb[VbRaddataSaving#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#7)]

#### <a name="to-add-new-orders"></a>添加新顺序

- 将以下 `AddNewOrders` 方法添加到“Form1”：

     [!code-csharp[VbRaddataSaving#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#8)]
     [!code-vb[VbRaddataSaving#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#8)]

## <a name="run-the-application"></a>运行此应用程序

#### <a name="to-run-the-application"></a>要运行应用程序

- 选择**F5**以运行应用程序。

## <a name="see-also"></a>请参阅
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
