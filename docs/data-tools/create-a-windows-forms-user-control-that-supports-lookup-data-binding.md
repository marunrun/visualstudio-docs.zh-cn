---
title: 在数据绑定中使用查找表-Windows 窗体控件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a5d6309818c251b9101b1345450ef66f3fc8f1f8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586791"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>创建支持查找数据绑定的 Windows 窗体用户控件

在 Windows 窗体上显示数据时，你可以从“工具箱”中选择现有的控件，或者，如果应用程序需要标准控件中无法实现的功能时，你还可以创作自定义控件。 本演练显示了如何创建实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> 的控件。 实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> 的控件可以包含三个属性，这些属性可以绑定到数据。 此类控件类似于 <xref:System.Windows.Forms.ComboBox>。

有关控件创作的详细信息，请参阅[在设计时开发 Windows 窗体控件](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)。

创作用于数据绑定方案中的控件时，你需要实现以下数据绑定特性之一：

|数据绑定属性用法|
| - |
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 有关详细信息，请参阅[创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 有关详细信息，请参阅[创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），该控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 （本演练页面描述了此过程）。|

本演练创建绑定到源自两个表的数据的查找控件。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。 查找控件绑定到 `Orders` 表中的 `CustomerID` 字段。 它使用此值来查找 `Customers` 表中的 `CompanyName`。

在本演练中，您将学习如何：

- 创建新的“Windows 窗体应用程序”。

- 将新的“用户控件”添加到项目中。

- 以可视方式设计用户控件。

- 实现 `LookupBindingProperty` 特性。

- 使用 "**数据源配置**向导" 创建数据集。

- 在“数据源”窗口中，设置“Orders”表上的“CustomerID”列，以使用新的控件。

- 创建一个用于在新控件中显示数据的窗体。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在**Visual Studio 安装程序**中，可以将 SQL Server Express LocalDB 作为**数据存储和处理**工作负荷的一部分进行安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （SQL Server 对象资源管理器作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

## <a name="create-a-windows-forms-app-project"></a>创建 Windows 窗体应用项目

第一步是创建**Windows 窗体应用程序**项目。

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”。

2. 在左侧窗格中展开 "**视觉对象C#**  " 或 " **Visual Basic** "，然后选择 " **Windows 桌面**"。

3. 在中间窗格中，选择 " **Windows 窗体应用程序**" 项目类型。

4. 将项目命名为**LookupControlWalkthrough**，然后选择 **"确定"** 。

     创建“LookupControlWalkthrough”项目并添加到“解决方案资源管理器”中。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中

由于本演练从“用户控件”创建查找控件，所以必须将“用户控件”项添加到“LookupControlWalkthrough”项目中。

1. 从“项目”菜单中，选择“添加用户控件”。

2. 在 "**名称**" 区域中键入 `LookupBox`，然后单击 "**添加**"。

     将“LookupBox”控件添加到“解决方案资源管理器”中，并在设计器中打开该控件。

## <a name="design-the-lookupbox-control"></a>设计 LookupBox 控件

若要设计 LookupBox 控件，请将 **"工具箱**" 中的 <xref:System.Windows.Forms.ComboBox> 拖动到用户控件的设计图面上。

## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定特性

对于支持数据绑定的查找控件，你可以实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>。

1. 将“LookupBox”控件切换到代码视图。 （在“视图”菜单上，选择“代码”。）

2. 将 `LookupBox` 中的代码替换为以下内容：

     [!code-vb[VbRaddataDisplaying#5](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.vb)]
     [!code-csharp[VbRaddataDisplaying#5](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.cs)]

3. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

## <a name="create-a-data-source-from-your-database"></a>从数据库创建数据源

此步骤根据 Northwind 示例数据库中的 `Customers` 和 `Orders` 表，使用“数据源配置”向导创建数据源。

1. 若要打开 "**数据源**" 窗口，请在 "**数据**" 菜单上单击 "**显示数据源**"。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在 **“选择数据源类型”** 页上选择 **“数据库”** ，然后单击 **“下一步”** 。

4. 在“选择数据连接”页面上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

    - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，再单击“下一步”。

6. 在 "将**连接字符串保存到应用程序配置文件**" 页上，单击 "**下一步**"。

7. 在“选择数据库对象”页上，展开“表”节点。

8. 选择 `Customers` 和 `Orders` 表，然后单击“完成”。

     将“NorthwindDataSet”添加到项目后，“数据源”窗口中即会显示 `Customers` 和 `Orders` 表。

## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>将 Orders 表的 CustomerID 列设置为使用 LookupBox 控件

在“数据源”窗口中，可以先设置要创建的控件，然后再将项拖动到窗体上。

1. 在设计器中打开“Form1”。

2. 在“数据源”窗口中展开“Customers”节点。

3. 展开“Orders”节点（“Customers”节点中“Fax”列下面的节点）。

4. 单击“Orders”节点上的下拉箭头，然后从控件列表中选择“详细信息”。

5. 单击“CustomerID”列（在“Orders”节点中）上的下拉箭头，然后选择“自定义”。

6. 在“数据 UI 自定义选项”对话框中，从“关联的控件”列表中选择“LookupBox”。

7. 单击" **确定**"。

8. 单击“CustomerID”列上的下拉箭头，然后选择“LookupBox”。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

通过将某些项从“数据源”窗口中拖到“Form1”上，可创建数据绑定控件。

若要在 Windows 窗体上创建数据绑定控件，请将 " **Orders** " 节点从 "**数据源**" 窗口拖到 windows 窗体上，并验证 " **LookupBox** " 控件是否用于显示 `CustomerID` 列中的数据。

## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>绑定控件以从 Customers 表中查找公司名称

若要设置查找绑定，请在 "**数据源**" 窗口中选择 "主要**客户**" 节点，并将其拖到 " **CustomerIDLookupBox** on **Form1**" 中的组合框上。

此操作对数据绑定进行设置，使其显示 `Customers` 表中的 `CompanyName`同时保留 `Orders` 表中的 `CustomerID` 值。

## <a name="run-the-application"></a>运行此应用程序

- 按 **F5** 运行该应用程序。

- 通过某些记录进行定位，并验证 `LookupBox` 控件中是否显示 `CompanyName`。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
