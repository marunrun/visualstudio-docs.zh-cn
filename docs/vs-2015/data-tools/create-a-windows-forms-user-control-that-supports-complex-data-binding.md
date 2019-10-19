---
title: 创建支持复杂数据绑定的 Windows 窗体用户控件 |Microsoft Docs
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
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
ms.assetid: c8f29c2b-b49b-4618-88aa-33b6105880b5
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 99c4a20939ed2e3a036831930749bb59b5a42315
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670043"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>创建支持复杂数据绑定的 Windows 窗体用户控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Windows 应用程序的窗体上显示数据时，可以从“工具箱”中选择现有的控件，而当标准控件无法提供应用程序所要求的功能时，还可以创作自定义控件。 本演练显示了如何创建实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> 的控件。 实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> 的控件包含可以绑定到数据的 `DataSource` 和 `DataMember` 属性。 此类控件类似于 <xref:System.Windows.Forms.DataGridView> 或 <xref:System.Windows.Forms.ListBox>。

 有关控件创作的详细信息，请参阅[在设计时开发 Windows 窗体控件](https://msdn.microsoft.com/library/e5a8e088-7ec8-4fd9-bcb3-9078fd134829)。

 创作用于数据绑定方案中的控件时，需要实现以下数据绑定属性之一：

|数据绑定属性用法|
|-----------------------------------|
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 有关详细信息，请参阅[创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。|
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 （本演练页面描述了此过程）。|
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），此类控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 有关详细信息，请参阅[创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。|

 本演练创建显示表中多行数据的复杂控件。 本示例使用源自 Northwind 示例数据库的 `Customers` 表。 复杂用户控件将会在自定义控件中的 <xref:System.Windows.Forms.DataGridView> 中显示 Customers 表。

 在本演练中，你将学会如何执行以下任务：

- 创建新的**Windows 应用程序**。

- 将新的“用户控件”添加到项目中。

- 以可视方式设计用户控件。

- 实现 `ComplexBindingProperty` 特性。

- 使用 "[数据源配置向导](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)" 创建数据集。

- 在 "[数据源" 窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)中设置**Customers**表以使用新的复杂控件。

- 通过将新控件从 "**数据源" 窗口**拖到**Form1**上来添加新控件。

## <a name="prerequisites"></a>Prerequisites
 若要完成本演练，你将需要：

- 能够访问 Northwind 示例数据库。

## <a name="create-a-windows-application"></a>创建 Windows 应用程序
 第一步是创建**Windows 应用程序**。

#### <a name="to-create-the-new-windows-project"></a>创建新的 Windows 项目

1. 在 Visual Studio 中的 "**文件**" 菜单上，创建一个新**项目**。

2. 将项目命名为 **ComplexControlWalkthrough**。

3. 选择 " **Windows 应用程序**"，然后单击 **"确定"** 。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。

     “ComplexControlWalkthrough”项目即被创建并添加到“解决方案资源管理器”中。

## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中
 由于本演练从**用户控件**创建复杂的数据可绑定控件，因此必须将**用户控件**项添加到项目。

#### <a name="to-add-a-user-control-to-the-project"></a>将用户控件添加到项目中

1. 从“项目”菜单，选择“添加用户控件”。

2. 在“名称”区域中键入“ComplexDataGridView”，然后单击“添加”。

     “ComplexDataGridView”控件将会添加到“解决方案资源管理器”中，并在设计器中打开该控件。

## <a name="design-the-complexdatagridview-control"></a>设计 ComplexDataGridView 控件
 此步骤将 <xref:System.Windows.Forms.DataGridView> 添加到该用户控件。

#### <a name="to-design-the-complexdatagridview-control"></a>设计 ComplexDataGridView 控件

- 将 <xref:System.Windows.Forms.DataGridView> 从“工具箱”拖到该用户控件的设计图面上。

## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定特性
 对于支持数据绑定的复杂控件，你可以实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>。

#### <a name="to-implement-the-complexbindingproperties-attribute"></a>实现 ComplexBindingProperties 特性

1. 将“ComplexDataGridView”控件切换到代码视图。 （在“视图”菜单上，选择“代码”。）

2. 将 `ComplexDataGridView` 中的代码替换为以下内容：

     [!code-csharp[VbRaddataDisplaying#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/ComplexDataGridView.cs#4)]
     [!code-vb[VbRaddataDisplaying#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/ComplexDataGridView.vb#4)]

3. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

## <a name="creating-a-data-source-from-your-database"></a>从数据库创建数据源
 此步骤根据 Northwind 示例数据库中的 `Customers` 表，使用“数据源配置”向导创建数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[安装 SQL Server 示例数据库](../data-tools/install-sql-server-sample-databases.md)。

#### <a name="to-create-the-data-source"></a>创建数据源

1. 在 **“数据”** 菜单上，单击 **“显示数据源”** 。

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
 在“数据源”窗口中，可以先设置要创建的控件，然后再将项拖动到窗体上。

#### <a name="to-set-the-customers-table-to-bind-to-the-complexdatagridview-control"></a>设置 Customers 表以绑定到 ComplexDataGridView 控件

1. 在设计器中打开“Form1”。

2. 在“数据源”窗口中展开“Customers”节点。

3. 单击“Customers”节点上的下拉箭头，然后选择“自定义”。

4. 在“数据 UI 自定义选项”对话框中，从“关联的控件”列表中选择“ComplexDataGridView”。

5. 单击 `Customers` 表上的下拉箭头，然后从控件列表中选择“ComplexDataGridView”。

## <a name="addcontrols-to-the-form"></a>Addcontrols 窗体
 通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。

#### <a name="to-create-data-bound-controls-on-the-form"></a>在窗体上创建数据绑定控件

- 将主 " **Customers** " 节点从 "**数据源**" 窗口拖到窗体上。验证 " **ComplexDataGridView** " 控件是否用于显示该表的数据。

## <a name="running-the-application"></a>运行应用程序

#### <a name="to-run-the-application"></a>要运行应用程序

- 按 F5 运行该应用程序。

## <a name="next-steps"></a>后续步骤
 根据应用程序的需求，在创建了支持数据绑定的控件后，还可能需要执行一些步骤。 接下来的一些常见步骤包括：

- 将你的自定义控件置于控件库中，以便在其他应用程序中重用它们。

- 创建支持查找方案的控件。 有关详细信息，请参阅[创建支持查找数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)。

## <a name="see-also"></a>请参阅
 将[Windows 窗体控件绑定到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)[设置从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md) [Windows 窗体控件](https://msdn.microsoft.com/library/f050de8f-4ebd-4042-94b8-edf9a1dbd52a)
