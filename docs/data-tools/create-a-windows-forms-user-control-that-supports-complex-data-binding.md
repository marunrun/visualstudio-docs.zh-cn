---
title: 使用数据绑定创建 Windows 窗体用户控件
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 97d9e64a0fcabb207d4606d4819f6afcb61b1043
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586843"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>创建支持复杂数据绑定的 Windows 窗体用户控件

在 Windows 应用程序中的窗体上显示数据时，您可以从 "**工具箱**" 中选择现有控件。 或者，如果您的应用程序需要的功能在标准控件中不可用，则可以创作自定义控件。 本演练显示了如何创建实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> 的控件。 实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> 的控件包含可以绑定到数据的 `DataSource` 和 `DataMember` 属性。 此类控件类似于 <xref:System.Windows.Forms.DataGridView> 或 <xref:System.Windows.Forms.ListBox>。

有关控件创作的详细信息，请参阅[在设计时开发 Windows 窗体控件](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)。

创作用于数据绑定方案中的控件时，需要实现以下数据绑定属性之一：

|数据绑定属性用法|
| - |
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 有关详细信息，请参阅[创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 （本演练页面描述了此过程）。|
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），此类控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 有关详细信息，请参阅[创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。|

本演练创建显示表中多行数据的复杂控件。 本示例使用源自 Northwind 示例数据库的 `Customers` 表。 复杂用户控件将会在自定义控件中的 <xref:System.Windows.Forms.DataGridView> 中显示 Customers 表。

在本演练中，您将学习如何：

- 将新的“用户控件”添加到项目中。

- 以可视方式设计用户控件。

- 实现 `ComplexBindingProperty` 特性。

- 使用 "[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)" 创建数据集。

- 在 "[数据源" 窗口](add-new-data-sources.md#data-sources-window)中设置**Customers**表以使用新的复杂控件。

- 通过将新控件从“数据源”窗口拖到“Form1”上来添加新控件。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在**Visual Studio 安装程序**中，可以将 SQL Server Express LocalDB 作为**数据存储和处理**工作负荷的一部分进行安装，也可以作为单个组件安装。

1. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （SQL Server 对象资源管理器作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    1. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    1. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

## <a name="create-a-windows-forms-app-project"></a>创建 Windows 窗体应用项目

第一步是为C#或 Visual Basic 创建**Windows 窗体应用**项目。 将项目命名为 **ComplexControlWalkthrough**。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中

由于此演练从**用户控件**创建复杂的数据可绑定控件，因此将**用户控件**项添加到项目中：

1. 从“项目”菜单，选择“添加用户控件”。

1. 在“名称”区域中键入“ComplexDataGridView”，然后单击“添加”。

    “ComplexDataGridView”控件将会添加到“解决方案资源管理器”中，并在设计器中打开该控件。

## <a name="design-the-complexdatagridview-control"></a>设计 ComplexDataGridView 控件

若要向用户控件添加 <xref:System.Windows.Forms.DataGridView>，请将 **"工具箱**" 中的 <xref:System.Windows.Forms.DataGridView> 拖到用户控件的设计图面上。

## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定特性

对于支持数据绑定的复杂控件，可以实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>：

1. 将“ComplexDataGridView”控件切换到代码视图。 （在“视图”菜单上，选择“代码”。）

1. 将 `ComplexDataGridView` 中的代码替换为以下内容：

    [!code-csharp[VbRaddataDisplaying#4](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-complex-data-binding_1.cs)]
    [!code-vb[VbRaddataDisplaying#4](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-complex-data-binding_1.vb)]

1. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

## <a name="create-a-data-source-from-your-database"></a>从数据库创建数据源

使用 "**数据源配置**向导" 创建基于 Northwind 示例数据库中的 `Customers` 表的数据源：

1. 若要打开 "**数据源**" 窗口，请在 "**数据**" 菜单上单击 "**显示数据源**"。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在 **“选择数据源类型”** 页上选择 **“数据库”** ，然后单击 **“下一步”** 。

4. 在“选择数据连接”页面上，执行以下操作之一：

   - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

   - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，再单击“下一步”。

6. 在 "将**连接字符串保存到应用程序配置文件**" 页上，单击 "**下一步**"。

7. 在“选择数据库对象”页上，展开“表”节点。

8. 选择 `Customers` 表，然后单击“完成”。

   将“NorthwindDataSet”添加到项目中，并且“数据源”窗口中将显示 `Customers` 表。

## <a name="set-the-customers-table-to-use-the-complexdatagridview-control"></a>设置 Customers 表以使用 ComplexDataGridView 控件

在“数据源”窗口中，可以先设置要创建的控件，然后再将项拖动到窗体上：

1. 在设计器中打开“Form1”。

1. 在“数据源”窗口中展开“Customers”节点。

1. 单击“Customers”节点上的下拉箭头，然后选择“自定义”。

1. 在“数据 UI 自定义选项”对话框中，从“关联的控件”列表中选择“ComplexDataGridView”。

1. 单击 `Customers` 表上的下拉箭头，然后从控件列表中选择“ComplexDataGridView”。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。 将主“Customers”节点从“数据源”窗口拖动到窗体上。 验证 " **ComplexDataGridView** " 控件是否用于显示该表的数据。

## <a name="run-the-application"></a>运行此应用程序

按 **F5** 运行该应用程序。

## <a name="next-steps"></a>后续步骤

根据应用程序的需求，在创建了支持数据绑定的控件后，还可能需要执行一些步骤。 接下来的一些常见步骤包括：

- 将你的自定义控件置于控件库中，以便在其他应用程序中重用它们。

- 创建支持查找方案的控件。 有关详细信息，请参阅[创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
- [Windows 窗体控件](/dotnet/framework/winforms/controls/index)
