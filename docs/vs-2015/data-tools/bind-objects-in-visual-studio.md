---
title: 将对象绑定
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
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 09afb67f0e9431ca8cd520635f243dca70880f09
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65683155"
---
# <a name="bind-objects-in-visual-studio"></a>Visual Studio 中的绑定对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 提供用于为你的应用程序中的数据源使用自定义对象的设计时工具。 当你想要将绑定到 UI 控件的对象中存储数据库中的数据时，建议的方法是使用实体框架生成的类。 DbSet 对象上调用 AcceptChanges 时，实体 Frameworkautogenerates 所有样板更改跟踪代码，这意味着对本地对象的任何更改都会自动保存到数据库。    有关详细信息，请参阅[Entity Framework 文档](https://ef.readthedocs.org/en/latest/)。

> [!TIP]
> 如果你的应用程序已基于数据集，才应考虑到这篇文章中的对象绑定的方法。如果你已熟悉的数据集，并进行处理的数据是表格和不太复杂或过大，则还可以使用这些方法。 更简单的示例，涉及将数据加载到对象直接，通过使用 DataReader 并手动更新用户界面而无需进行数据绑定，请参阅[使用 ADO.NET 创建简单的数据应用](../data-tools/create-a-simple-data-application-by-using-adonet.md)。

## <a name="object-requirements"></a>对象要求
 若要处理的数据设计工具在 Visual Studio 中的自定义对象的唯一要求是，对象所需的至少一个公共属性。

 通常情况下，自定义对象不需要任何特定的接口，构造函数或要充当应用程序的数据源属性。 但是，如果你想要将对象从**数据源**窗口到设计图面来创建数据绑定控件，并且如果该对象实现<xref:System.ComponentModel.ITypedList>或<xref:System.ComponentModel.IListSource>接口，该对象必须具有默认值构造函数。 否则为 Visual Studio 无法实例化的数据源对象，并将项拖至设计图面上时显示错误。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>作为数据源使用自定义对象的示例
 虽然有无数的使用方法来实现应用程序逻辑，使用对象作为数据源时，SQL 的情况下存在数据库是可以通过使用 Visual Studio – 生成 TableAdapter 对象来简化的几个标准操作。 此页说明如何实现这些标准过程使用 TableAdapters.It 不旨在作为指南来创建自定义对象。 例如，你通常将执行以下的标准操作而不考虑特定实现的对象或应用程序的逻辑：

- 将数据加载到对象 （通常是从数据库）。

- 创建类型化的对象的集合。

- 将对象添加到和从集合中删除对象。

- 向窗体上的用户显示的对象数据。

- 更改并正在编辑的对象中的数据。

- 将数据从对象保存到数据库。

> [!NOTE]
> 为了更好地了解，并为此页上的示例提供的上下文，我们建议你完成以下：[演练：连接到对象 （Windows 窗体） 中的数据](https://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)。 该演练创建此处所述的对象。

### <a name="loaddata-into-objects"></a>为对象的 Loaddata
 对于此示例中，您将数据加载到您的对象使用 Tableadapter。 默认情况下，使用两种类型的方法，从数据库提取数据并填充数据的表创建 Tableadapter。

- `TableAdapter.Fill`方法返回的数据填充现有数据表。

- `TableAdapter.GetData`方法返回一个新的数据集填充数据。

  加载数据使用自定义对象的最简单方法是调用`TableAdapter.GetData`方法中，循环遍历返回的数据表中的行的集合，并填充每个行中的值与每个对象。 您可以创建`GetData`返回填充的数据表的任何添加到 TableAdapter 的查询的方法。

> [!NOTE]
> Visual Studio 名称 TableAdapter 查询`Fill`和`GetData`默认情况下，但这些名称可以更改为任何有效的方法名称。

 下面的示例演示如何循环访问在数据表中的行和填充数据的对象：

 [!code-csharp[VbRaddataConnecting#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Form1.cs#4)]
 [!code-vb[VbRaddataConnecting#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Form1.vb#4)]

### <a name="create-a-typed-collection-of-objects"></a>创建类型化的对象的集合
 可以为您的对象，创建集合类，也可以使用自动提供的类型化的集合[BindingSource 组件](https://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9)。

 当创建对象的自定义集合类时，我们建议从继承<xref:System.ComponentModel.BindingList%601>。 此泛型类提供功能来管理你的集合，以及能够引发事件通知发送到 Windows 窗体中的数据绑定基础结构。

 中的自动生成的集合<xref:System.Windows.Forms.BindingSource>使用<xref:System.ComponentModel.BindingList%601>其类型的集合。 如果你的应用程序不需要额外的功能，则可以保留在集合内的<xref:System.Windows.Forms.BindingSource>。 有关详细信息，请参阅<xref:System.Windows.Forms.BindingSource.List%2A>属性的<xref:System.Windows.Forms.BindingSource>类。

> [!NOTE]
> 如果你的集合要求没有提供的基实现的功能<xref:System.ComponentModel.BindingList%601>，应创建自定义集合，以便您可以根据需要添加到类。

 下面的代码演示如何创建强类型化的集合类`Order`对象：

 [!code-csharp[VbRaddataConnecting#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#8)]
 [!code-vb[VbRaddataConnecting#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#8)]

### <a name="addobjects-to-a-collection"></a>Addobjects 到集合
 通过调用的对象添加到集合`Add`方法的自定义集合类或的<xref:System.Windows.Forms.BindingSource>。

 有关将添加到集合使用的示例<xref:System.Windows.Forms.BindingSource>，请参阅`LoadCustomers`中的方法[演练：连接到对象 （Windows 窗体） 中的数据](https://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)。

 将对象添加到自定义集合的示例，请参阅`LoadOrders`中的方法[演练：连接到对象 （Windows 窗体） 中的数据](https://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)。

> [!NOTE]
> `Add`方法会自动提供为自定义集合时从继承<xref:System.ComponentModel.BindingList%601>。

 下面的代码演示如何将对象添加到中的类型化集合<xref:System.Windows.Forms.BindingSource>:

 [!code-csharp[VbRaddataConnecting#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#5)]
 [!code-vb[VbRaddataConnecting#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#5)]

 下面的代码演示如何将对象添加到继承的类型集合<xref:System.ComponentModel.BindingList%601>:

> [!NOTE]
> 在此示例中`Orders`集合是的一个属性`Customer`对象。

 [!code-csharp[VbRaddataConnecting#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#6)]
 [!code-vb[VbRaddataConnecting#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#6)]

### <a name="removeobjects-from-a-collection"></a>从集合 Removeobjects
 您从集合中移除对象通过调用`Remove`或`RemoveAt`方法的自定义集合类或的<xref:System.Windows.Forms.BindingSource>。

> [!NOTE]
> `Remove`并`RemoveAt`方法自动提供为自定义集合，当从继承<xref:System.ComponentModel.BindingList%601>。

 下面的代码演示如何查找并删除对象中的类型化集合<xref:System.Windows.Forms.BindingSource>与<xref:System.Windows.Forms.BindingSource.RemoveAt%2A>方法：

 [!code-csharp[VbRaddataConnecting#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#7)]
 [!code-vb[VbRaddataConnecting#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#7)]

### <a name="displayobject-data-to-users"></a>向用户 Displayobject 数据
 若要显示给用户的对象中的数据，创建对象数据源使用**数据源配置**向导，然后将整个对象或单独的属性拖动到窗体从**数据源**窗口。

### <a name="modify-the-data-in-objects"></a>修改对象中的数据
 若要编辑自定义对象绑定到 Windows 窗体控件中的数据，只需编辑数据绑定控件中 （或直接在对象的属性中）。 数据绑定体系结构更新的对象中的数据。

 如果应用程序需要的更改跟踪和回滚建议的更改到其原始值，则必须在您的对象模型中实现此功能。 有关如何保留跟踪数据的表的建议的更改示例，请参阅<xref:System.Data.DataRowState>， <xref:System.Data.DataSet.HasChanges%2A>，和<xref:System.Data.DataTable.GetChanges%2A>。

### <a name="savedata-in-objects-back-to-the-database"></a>与数据库对象中的 Savedata
 通过将值从您的对象传递到 TableAdapter 的 DBDirect 方法将数据保存回数据库。

 Visual Studio 创建可以直接对数据库执行的 DBDirect 方法。 这些方法不需要 DataSet 或 DataTable 对象。

|TableAdapter DBDirect 方法|描述|
|----------------------------------|-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库，您可以在各列的值作为方法参数中传递。|
|`TableAdapter.Update`|更新现有数据库中的记录。 Update 方法使用原始的和新列的值作为方法参数。 用于查找的原始记录的原始值和新值用于更新该记录。<br /><br /> `TableAdapter.Update`方法还可用于将数据集的更改回数据库中，通过采用<xref:System.Data.DataSet>， <xref:System.Data.DataTable>， <xref:System.Data.DataRow>，或数组<xref:System.Data.DataRow>的方法参数。|
|`TableAdapter.Delete`|删除现有的基于原始列值作为方法参数传入数据库中的记录。|

 若要保存数据的对象的集合，请依次通过 （例如，使用的下一步循环） 的对象的集合。使用 TableAdapter 的 DBDirect 方法将为每个对象的值发送到数据库。

 下面的示例演示如何使用`TableAdapter.Insert`DBDirect 方法来添加新客户直接到数据库：

 [!code-csharp[VbRaddataSaving#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#23)]
 [!code-vb[VbRaddataSaving#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#23)]

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
