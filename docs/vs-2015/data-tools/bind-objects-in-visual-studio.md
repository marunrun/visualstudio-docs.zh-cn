---
title: 绑定对象
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c487df5623a233146655593265e15c34a884de3c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672999"
---
# <a name="bind-objects-in-visual-studio"></a>Visual Studio 中的绑定对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 提供设计时工具，用于在应用程序中使用自定义对象作为数据源。 如果要在绑定到 UI 控件的对象中存储数据库中的数据，建议使用实体框架来生成类。 实体 Frameworkautogenerates 所有样本更改跟踪代码，这意味着在 DbSet 对象上调用 AcceptChanges 时，对本地对象所做的任何更改都将自动保存到数据库中。    有关详细信息，请参阅[实体框架文档](https://ef.readthedocs.org/en/latest/)。

> [!TIP]
> 仅当应用程序已基于数据集时，才应考虑本文中的对象绑定方法。如果您已经熟悉数据集，则还可以使用这些方法，并且您要处理的数据是表格形式，并且不太复杂或太大。 有关更简单的示例（涉及使用 DataReader 直接将数据加载到对象和手动更新 UI 而不进行数据绑定），请参阅[使用 ADO.NET 创建简单的数据应用程序](../data-tools/create-a-simple-data-application-by-using-adonet.md)。

## <a name="object-requirements"></a>对象要求
 在 Visual Studio 中使用数据设计工具的自定义对象的唯一要求是，对象至少需要一个公共属性。

 通常，自定义对象不需要任何特定接口、构造函数或属性作为应用程序的数据源。 但是，如果要将对象从 "**数据源**" 窗口拖到设计图面以创建数据绑定控件，并且如果对象实现 <xref:System.ComponentModel.ITypedList> 或 <xref:System.ComponentModel.IListSource> 接口，则该对象必须具有默认构造函数。 否则，Visual Studio 无法实例化数据源对象，并在将项拖动到设计图面时显示错误。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>使用自定义对象作为数据源的示例
 虽然在将对象作为数据源时实现应用程序逻辑有无数种方法，但对于 SQL 数据库，有几种标准操作可以通过使用 Visual Studio 生成的 TableAdapter 对象来简化。 本页说明如何使用 TableAdapters.It 实现这些标准进程，而不是将其用作创建自定义对象的指南。 例如，你通常会执行以下标准操作，而不考虑对象的特定实现或应用程序的逻辑：

- 将数据加载到对象（通常从数据库中）。

- 创建对象的类型化集合。

- 向集合中添加对象和从集合中删除对象。

- 在窗体上向用户显示对象数据。

- 更改/编辑对象中的数据。

- 将对象中的数据保存回数据库。

> [!NOTE]
> 为了更好地理解和提供此页上的示例上下文，我们建议您完成以下操作：[演练：连接到对象中的数据（Windows 窗体）](https://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)。 本演练将创建此处讨论的对象。

### <a name="loaddata-into-objects"></a>Loaddata 到对象中
 在此示例中，使用 Tableadapter 将数据加载到对象。 默认情况下，将使用两种方法创建 Tableadapter，这些方法从数据库中提取数据并填充数据表。

- @No__t_0 方法使用返回的数据填充现有数据表。

- @No__t_0 方法返回用数据填充的新数据表。

  使用数据加载自定义对象的最简单方法是调用 `TableAdapter.GetData` 方法，遍历返回的数据表中的行集合，并使用每行中的值填充每个对象。 您可以创建一个 `GetData` 方法，该方法为添加到 TableAdapter 的任何查询返回填充的数据表。

> [!NOTE]
> 默认情况下，Visual Studio `Fill` 和 `GetData` 命名 TableAdapter 查询，但这些名称可更改为任何有效的方法名称。

 下面的示例演示如何遍历数据表中的行，并使用数据填充对象：

 [!code-csharp[VbRaddataConnecting#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Form1.cs#4)]
 [!code-vb[VbRaddataConnecting#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Form1.vb#4)]

### <a name="create-a-typed-collection-of-objects"></a>创建对象的类型化集合
 可以为对象创建集合类，或使用[BindingSource 组件](https://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9)自动提供的类型化集合。

 为对象创建自定义集合类时，建议从 <xref:System.ComponentModel.BindingList%601> 继承。 此泛型类提供管理集合的功能，以及在 Windows 窗体中引发将通知发送到数据绑定基础结构的事件的功能。

 @No__t_0 中自动生成的集合对其类型化集合使用 <xref:System.ComponentModel.BindingList%601>。 如果你的应用程序不需要其他功能，你可以在 <xref:System.Windows.Forms.BindingSource> 中维护你的集合。 有关详细信息，请参阅 <xref:System.Windows.Forms.BindingSource> 类的 <xref:System.Windows.Forms.BindingSource.List%2A> 属性。

> [!NOTE]
> 如果集合需要 <xref:System.ComponentModel.BindingList%601> 的基实现未提供的功能，则应创建自定义集合，以便可以根据需要将其添加到类中。

 下面的代码演示如何为 `Order` 对象的强类型集合创建类：

 [!code-csharp[VbRaddataConnecting#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#8)]
 [!code-vb[VbRaddataConnecting#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#8)]

### <a name="addobjects-to-a-collection"></a>Addobjects 到集合
 您可以通过调用自定义集合类或 <xref:System.Windows.Forms.BindingSource> 的 `Add` 方法，将对象添加到集合中。

 有关使用 <xref:System.Windows.Forms.BindingSource> 添加到集合的示例，请参阅[演练：连接到对象中的数据（Windows 窗体）](https://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)中的 `LoadCustomers` 方法。

 有关将对象添加到自定义集合的示例，请参阅[演练：连接到对象中的数据（Windows 窗体）](https://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)中的 `LoadOrders` 方法。

> [!NOTE]
> 从 <xref:System.ComponentModel.BindingList%601> 继承时，会自动为自定义集合提供 `Add` 方法。

 下面的代码演示如何将对象添加到 <xref:System.Windows.Forms.BindingSource> 中的类型化集合：

 [!code-csharp[VbRaddataConnecting#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#5)]
 [!code-vb[VbRaddataConnecting#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#5)]

 下面的代码演示如何将对象添加到从 <xref:System.ComponentModel.BindingList%601> 继承的类型化集合：

> [!NOTE]
> 在此示例中，`Orders` 集合是 `Customer` 对象的一个属性。

 [!code-csharp[VbRaddataConnecting#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#6)]
 [!code-vb[VbRaddataConnecting#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#6)]

### <a name="removeobjects-from-a-collection"></a>从集合中 Removeobjects
 您可以通过调用自定义集合类或 <xref:System.Windows.Forms.BindingSource> 的 `Remove` 或 `RemoveAt` 方法从集合中删除对象。

> [!NOTE]
> 当你从 <xref:System.ComponentModel.BindingList%601> 继承时，将自动为你的自定义集合提供 `Remove` 和 `RemoveAt` 方法。

 下面的代码演示如何使用 <xref:System.Windows.Forms.BindingSource.RemoveAt%2A> 方法在 <xref:System.Windows.Forms.BindingSource> 中查找和删除类型化集合中的对象：

 [!code-csharp[VbRaddataConnecting#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs#7)]
 [!code-vb[VbRaddataConnecting#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb#7)]

### <a name="displayobject-data-to-users"></a>向用户 Displayobject 数据
 若要向用户显示对象中的数据，请使用 "**数据源配置**向导" 创建一个对象数据源，然后将整个对象或各个属性从 "**数据源**" 窗口拖到窗体上。

### <a name="modify-the-data-in-objects"></a>修改对象中的数据
 若要编辑数据绑定到 Windows 窗体控件的自定义对象中的数据，只需编辑绑定控件中的数据（或直接在对象的属性中编辑）。 数据绑定体系结构更新对象中的数据。

 如果你的应用程序需要跟踪更改，并向其原始值回滚建议的更改，则必须在对象模型中实现此功能。 有关数据表如何跟踪建议的更改的示例，请参阅 <xref:System.Data.DataRowState>、<xref:System.Data.DataSet.HasChanges%2A> 和 <xref:System.Data.DataTable.GetChanges%2A>。

### <a name="savedata-in-objects-back-to-the-database"></a>将对象中的 Savedata 回数据库
 通过将对象中的值传递给 TableAdapter 的 DBDirect 方法，将数据保存回数据库。

 Visual Studio 会创建可直接针对数据库执行的 DBDirect 方法。 这些方法不需要数据集或 DataTable 对象。

|TableAdapter DBDirect 方法|描述|
|----------------------------------|-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库，以便作为方法参数传入单独的列值。|
|`TableAdapter.Update`|更新数据库中的现有记录。 Update 方法将原始值和新列值作为方法参数使用。 原始值用于查找原始记录，新值用于更新该记录。<br /><br /> @No__t_0 方法还用于通过将 <xref:System.Data.DataRow>s 的 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> 或数组作为方法参数来协调数据集中的更改。|
|`TableAdapter.Delete`|基于作为方法参数传入的原始列值删除数据库中的现有记录。|

 若要保存对象集合中的数据，请遍历对象的集合（例如，使用 for next 循环）。使用 TableAdapter 的 DBDirect 方法将每个对象的值发送到数据库。

 下面的示例演示如何使用 `TableAdapter.Insert` DBDirect 方法将新客户直接添加到数据库中：

 [!code-csharp[VbRaddataSaving#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#23)]
 [!code-vb[VbRaddataSaving#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#23)]

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
