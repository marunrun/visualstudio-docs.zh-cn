---
title: 创建支持查找数据绑定的 Windows 窗体用户控件 |Microsoft Docs
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
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a54558c2aa760ea9bb318b527a49d01efcfbef04
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694076"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>创建支持查找数据绑定的 Windows 窗体用户控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Windows 窗体上显示数据时，你可以从“工具箱”中选择现有的控件，或者，如果应用程序需要标准控件中无法实现的功能时，你还可以创作自定义控件。 本演练显示了如何创建实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> 的控件。 实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> 的控件可以包含三个属性，这些属性可以绑定到数据。 此类控件类似于 <xref:System.Windows.Forms.ComboBox>。  
  
 控件创作的详细信息，请参阅[在设计时开发 Windows 窗体控件](https://msdn.microsoft.com/library/e5a8e088-7ec8-4fd9-bcb3-9078fd134829)。  
  
 创作用于数据绑定方案中的控件时，需要实现以下数据绑定属性之一：  
  
|数据绑定特性用法|  
|-----------------------------------|  
|在简单控件上实现 <xref:System.ComponentModel.DefaultBindingPropertyAttribute>（如 <xref:System.Windows.Forms.TextBox>），此类控件用于显示数据的单个列（或属性）。 有关详细信息，请参阅[创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。|  
|在控件上实现 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.DataGridView>），此类控件用于显示数据列表（或表）。 有关详细信息，请参阅[创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。|  
|在控件上实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>（如 <xref:System.Windows.Forms.ComboBox>），该控件用于显示数据列表（或表），也需要显示数据的单个列或属性。 （本演练页面描述了此过程）。|  
  
 本演练创建绑定到源自两个表的数据的查找控件。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。 该查找控件将会绑定到源自 `CustomerID` 表的 `Orders` 字段。 它将使用此值从 `CompanyName` 表中查找 `Customers`。  
  
 在本演练中，你将学会如何执行以下任务：  
  
- 创建一个新**Windows 应用程序**。  
  
- 将新的“用户控件”添加到项目中。  
  
- 以可视方式设计用户控件。  
  
- 实现 `LookupBindingProperty` 特性。  
  
- 创建具有的数据集**数据源配置**向导。  
  
- 在“数据源”窗口中，设置“Orders”表上的“CustomerID”列，以使用新的控件。  
  
- 创建一个用于在新控件中显示数据的窗体。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你将需要：  
  
- 能够访问 Northwind 示例数据库。  
  
## <a name="create-a-windows-application"></a>创建 Windows 应用程序  
 第一步是创建**Windows 应用程序**。  
  
#### <a name="to-create-the-new-windows-project"></a>创建新的 Windows 项目  
  
1. 在 Visual Studio 中，从**文件**菜单中，创建一个新**项目**。  
  
2. 将项目命名**LookupControlWalkthrough**。  
  
3. 选择**Windows 窗体应用程序**，然后单击**确定**。  
  
     创建“LookupControlWalkthrough”项目并添加到“解决方案资源管理器”中。  
  
## <a name="add-a-user-control-to-the-project"></a>将用户控件添加到项目中  
 由于本演练从“用户控件”创建查找控件，所以必须将“用户控件”项添加到“LookupControlWalkthrough”项目中。  
  
#### <a name="to-add-a-user-control-to-the-project"></a>将用户控件添加到项目中  
  
1. 从“项目”菜单中，选择“添加用户控件”。  
  
2. 类型`LookupBox`中**名称**区域中，，然后单击**添加**。  
  
     将“LookupBox”控件添加到“解决方案资源管理器”中，并在设计器中打开该控件。  
  
## <a name="design-the-lookupbox-control"></a>设计 LookupBox 控件  
  
#### <a name="to-design-the-lookupbox-control"></a>设计 LookupBox 控件  
  
- 将 <xref:System.Windows.Forms.ComboBox> 从“工具箱”拖到该用户控件的设计图面上。  
  
## <a name="add-the-required-data-binding-attribute"></a>添加所需的数据绑定属性  
 对于支持数据绑定的查找控件，你可以实现 <xref:System.ComponentModel.LookupBindingPropertiesAttribute>。  
  
#### <a name="to-implement-the-lookupbindingproperties-attribute"></a>实现 LookupBindingProperties 特性  
  
1. 将“LookupBox”控件切换到代码视图。 （在“视图”菜单上，选择“代码”。）  
  
2. 将 `LookupBox` 中的代码替换为以下内容：  
  
     [!code-csharp[VbRaddataDisplaying#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/LookupBox.cs#5)]
     [!code-vb[VbRaddataDisplaying#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/LookupBox.vb#5)]  
  
3. 从 **“生成”** 菜单中选择 **“生成解决方案”**。  
  
## <a name="create-a-data-source-from-your-database"></a>从您的数据库创建数据源  
 此步骤根据 Northwind 示例数据库中的 `Customers` 和 `Orders` 表，使用“数据源配置”向导创建数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[安装 SQL Server 示例数据库](../data-tools/install-sql-server-sample-databases.md)。  
  
#### <a name="to-create-the-data-source"></a>创建数据源  
  
1. 在 **“数据”** 菜单上，单击 **“显示数据源”**。  
  
2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。  
  
3. 在 **“选择数据源类型”** 页上选择 **“数据库”** ，然后单击 **“下一步”**。  
  
4. 在“选择数据连接”页面上，执行以下操作之一：  
  
    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。  
  
    - 选择“新建连接”以启动“添加/修改连接”对话框。  
  
5. 如果数据库需要密码，请选择该选项以包括敏感数据，再单击“下一步”。  
  
6. 上**将连接字符串保存到应用程序配置文件**页上，单击**下一步**。  
  
7. 在“选择数据库对象”页上，展开“表”节点。  
  
8. 选择 `Customers` 和 `Orders` 表，然后单击“完成”。  
  
     将“NorthwindDataSet”添加到项目后，“数据源”窗口中即会显示 `Customers` 和 `Orders` 表。  
  
## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>将订单表以使用 LookupBox 控件的客户 id 列设置  
 在“数据源”窗口中，可以先设置要创建的控件，然后再将项拖动到窗体上。  
  
#### <a name="to-set-the-customerid-column-to-bind-to-the-lookupbox-control"></a>将“CustomerID”列设置为绑定到 LookupBox 控件  
  
1. 在设计器中打开“Form1”。  
  
2. 在“数据源”窗口中展开“Customers”节点。  
  
3. 展开“Orders”节点（“Customers”节点中“Fax”列下面的节点）。  
  
4. 单击“Orders”节点上的下拉箭头，然后从控件列表中选择“详细信息”。  
  
5. 单击“CustomerID”列（在“Orders”节点中）上的下拉箭头，然后选择“自定义”。  
  
6. 在“数据 UI 自定义选项”对话框中，从“关联的控件”列表中选择“LookupBox”。  
  
7. 单击 **“确定”**。  
  
8. 单击“CustomerID”列上的下拉箭头，然后选择“LookupBox”。  
  
## <a name="addcontrols-to-the-form"></a>向窗体 Addcontrols  
 通过将某些项从“数据源”窗口中拖到“Form1”上，可创建数据绑定控件。  
  
#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>在 Windows 窗体上创建数据绑定控件  
  
- 拖动**订单**从节点**数据源**窗口中的拖到 Windows 窗体，并验证**LookupBox**控件用于显示中的数据`CustomerID`列。  
  
## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>绑定控件从客户表中查找 CompanyName  
  
#### <a name="to-setup-the-lookup-bindings"></a>设置查找绑定  
  
- 选择主**客户**中的节点**数据源**窗口中，并将其放在组合框中框**CustomerIDLookupBox**上**Form1**.  
  
     此操作对数据绑定进行设置，使其显示 `Customers` 表中的 `CompanyName`同时保留 `Orders` 表中的 `CustomerID` 值。  
  
## <a name="running-the-application"></a>运行应用程序  
  
#### <a name="to-run-the-application"></a>要运行应用程序  
  
- 按 F5 运行该应用程序。  
  
- 通过某些记录进行定位，并验证 `LookupBox` 控件中是否显示 `CompanyName`。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
