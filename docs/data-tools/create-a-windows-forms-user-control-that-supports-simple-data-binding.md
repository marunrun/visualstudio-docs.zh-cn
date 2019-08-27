---
title: 创建可支持简单数据绑定的用户控件
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: d1584f0d6a772a6f24578f9693832fb6b0812444
ms.sourcegitcommit: 3cc73e74921a9ceb622542e0e263abeebc455c00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624494"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>创建支持简单数据绑定的 Windows 窗体用户控件

在 Windows 应用程序的窗体上显示数据时，可以从“工具箱”中选择现有的控件，而当标准控件无法提供应用程序所要求的功能时，还可以创作自定义控件  。 本演练显示了如何创建实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> 的控件。 用于实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> 的控件可以包含一个可以绑定到数据的属性。 此类控件类似于 <xref:System.Windows.Forms.TextBox> 或 <xref:System.Windows.Forms.CheckBox>。

控件创作的详细信息，请参阅[在设计时开发 Windows 窗体控件](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)。

在创作时用于在数据绑定方案中的控件，应实现以下数据绑定特性之一：

|数据绑定特性用法|
| - |
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 （本演练页面描述了此过程）。|
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 有关详细信息，请参阅[创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），此类控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 有关详细信息，请参阅[创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。|

本演练创建了一个简单控件，用于显示表中单个列的数据。 此示例使用 Northwind 示例数据库的 `Phone` 表中的 `Customers` 列。 简单的用户控件显示客户的电话号码采用标准的电话号码格式，使用<xref:System.Windows.Forms.MaskedTextBox>并将掩码设置为电话号码。

在本演练中，你将学会如何执行以下任务：

- 创建新的“Windows 窗体应用程序”  。

- 将新的“用户控件”添加到项目中  。

- 以可视方式设计用户控件。

- 实现 `DefaultBindingProperty` 特性。

- 创建具有的数据集**数据源配置**向导。

- 在“数据源”窗口中，设置“电话”列，以使用新的控件   。

- 创建一个用于在新控件中显示数据的窗体。

## <a name="prerequisites"></a>系统必备

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果您没有 SQL Server Express LocalDB，安装它从[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)，或通过**Visual Studio 安装程序**。 在中**Visual Studio 安装程序**，可以作为的一部分安装 SQL Server Express LocalDB**数据存储和处理**工作负荷，或作为单个组件。

2. 通过执行以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中打开**SQL Server 对象资源管理器**窗口。 (SQL Server 对象资源管理器安装的一部分**数据存储和处理**中的工作负荷**Visual Studio 安装程序**。)展开**SQL Server**节点。 LocalDB 实例上右键单击并选择**新查询**。

       查询编辑器窗口随即打开。

    2. 复制[Northwind Transact SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)到剪贴板。 此 T-SQL 脚本从零开始创建 Northwind 数据库，并使用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器，然后选择**Execute**按钮。

       后不久，查询完成运行并创建 Northwind 数据库。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建**Windows 窗体应用程序**:

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**在左侧窗格中，然后选择**Windows 桌面**。

3. 在中间窗格中，选择**Windows 窗体应用**项目类型。

4. 将项目命名**SimpleControlWalkthrough**，然后选择**确定**。

     创建“SimpleControlWalkthrough”项目并将其添加到“解决方案资源管理器”中   。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中

本演练创建一个简单的可数据绑定控件从**用户控件**。 添加**用户控件**项**SimpleControlWalkthrough**项目：

1. 从“项目”菜单，选择“添加用户控件”   。

2. 在名称区域键入“PhoneNumberBox”，然后单击“添加”   。

     将“PhoneNumberBox”控件添加到“解决方案资源管理器”中，并在设计器中打开它   。

## <a name="design-the-phonenumberbox-control"></a>设计 PhoneNumberBox 控件

本演练中阐述了现有<xref:System.Windows.Forms.MaskedTextBox>来创建**PhoneNumberBox**控件：

1. 将 <xref:System.Windows.Forms.MaskedTextBox> 从“工具箱”拖到该用户控件的设计图面上  。

2. 选择刚刚拖动的 <xref:System.Windows.Forms.MaskedTextBox> 上的智能标记，然后选择“设置掩码”  。

3. 在“输入掩码”对话框中选择“电话号码”，然后单击“确定”以设置掩码    。

## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定属性

对于支持数据绑定的简单控件，实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>：

1. 交换机**PhoneNumberBox**到代码视图的控件。 （在“视图”菜单上，选择“代码”。   ）

2. 中的代码替换**PhoneNumberBox**以下：

     [!code-csharp[VbRaddataDisplaying#3](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-simple-data-binding_1.cs)]
     [!code-vb[VbRaddataDisplaying#3](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-simple-data-binding_1.vb)]

3. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

## <a name="create-a-data-source-from-your-database"></a>从您的数据库创建数据源

此步骤根据 Northwind 示例数据库中的 `Customers` 表，使用“数据源配置”向导创建数据源  。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

1. 若要打开**数据源**窗口，然后在**数据**菜单中，单击**显示数据源**。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导    。

3. 在“选择数据源类型”页上，选择“数据库”，然后单击“下一步”    。

4. 在“选择数据连接”页面上，执行以下操作之一  ：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

    - 选择“新建连接”以启动“添加/修改连接”对话框   。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，再单击“下一步”  。

6. 上**将连接字符串保存到应用程序配置文件**页上，单击**下一步**。

7. 在“选择数据库对象”页上，展开“表”节点   。

8. 选择 `Customers` 表，然后单击“完成”  。

     将“NorthwindDataSet”添加到项目中，并且“数据源”窗口中将显示 `Customers` 表   。

## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>设置要使用 phonenumberbox 控件的 phone 列

在“数据源”窗口中，可以先设置要创建的控件，然后再将项拖动到窗体上  ：

1. 在设计器中打开“Form1”  。

2. 在“数据源”窗口中展开“Customers”节点   。

3. 在“Customers”节点上单击下拉箭头，然后从控件列表中选择“详细信息”   。

4. 单击“电话”列上的下拉箭头，然后选择“自定义”   。

5. 从“数据 UI 自定义选项”对话框中的“关联的控件”列表中，选择“PhoneNumberBox”    。

6. 单击“电话”列上的下拉箭头，然后选择“PhoneNumberBox”   。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

通过将“数据源”窗口中的项拖到窗体上，可创建数据绑定控件  。

若要创建数据绑定控件在窗体上的，将主**客户**从节点**数据源**窗口拖到窗体，并验证**PhoneNumberBox**控件用于显示中的数据**Phone**列。

带有描述性标签的数据绑定控件将显示在窗体上，同时还显示一个工具条 (<xref:System.Windows.Forms.BindingNavigator>)，用于在记录间进行导航。 组件栏中显示“[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)”、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

## <a name="run-the-application"></a>运行此应用程序

按 **F5** 运行该应用程序。

## <a name="next-steps"></a>后续步骤

根据应用程序的需求，在创建了支持数据绑定的控件后，可能还需要执行一些步骤。 接下来的一些常见步骤包括：

- 将你的自定义控件置于控件库中，以便在其他应用程序中重用它们。

- 创建支持更复杂的数据绑定方案的控件。 有关详细信息，请参阅[创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)并[创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)