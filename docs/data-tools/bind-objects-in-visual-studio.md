---
title: 数据绑定自定义对象
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b9994d52c5ca39d744cf26dc019440e70e809ee8
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925665"
---
# <a name="bind-objects-as-data-sources-in-visual-studio"></a>在 Visual Studio 中将对象绑定为数据源

Visual Studio 提供设计时工具, 用于在应用程序中使用自定义对象作为数据源。 如果要在绑定到 UI 控件的对象中存储数据库中的数据, 建议使用实体框架来生成类。 实体框架自动生成所有样板更改跟踪代码, 这意味着在 DbSet 对象上调用 AcceptChanges 时, 对本地对象所做的任何更改都将自动保存到数据库中。 有关详细信息, 请参阅[实体框架文档](https://ef.readthedocs.org/en/latest/)。

> [!TIP]
> 仅当应用程序已基于数据集时, 才应考虑本文中的对象绑定方法。 如果您已经熟悉了数据集, 则还可以使用这些方法, 并且您要处理的数据是表格形式的, 并且不太复杂或太大。 有关更简单的示例 (涉及使用 DataReader 直接将数据加载到对象和手动更新 UI 而不进行数据绑定), 请参阅[使用 ADO.NET 创建简单的数据应用程序](../data-tools/create-a-simple-data-application-by-using-adonet.md)。

## <a name="object-requirements"></a>对象要求

在 Visual Studio 中使用数据设计工具的自定义对象的唯一要求是, 对象至少需要一个公共属性。

通常, 自定义对象不需要任何特定接口、构造函数或属性作为应用程序的数据源。 但是, 如果要将对象从 "**数据源**" 窗口拖到设计图面以创建数据绑定控件, 并且如果对象实现<xref:System.ComponentModel.ITypedList>或<xref:System.ComponentModel.IListSource>接口, 则该对象必须具有默认构造函数。 否则, Visual Studio 无法实例化数据源对象, 并在将项拖动到设计图面时显示错误。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>使用自定义对象作为数据源的示例

虽然在使用对象作为数据源时实现应用程序逻辑有无数种方法, 但对于 SQL 数据库, 有一些标准操作可以通过使用 Visual Studio 生成的 TableAdapter 对象来简化。 本页说明如何使用 Tableadapter 实现这些标准进程。 它不是用于创建自定义对象的指南。 例如, 你通常会执行以下标准操作, 而不考虑对象的特定实现或应用程序的逻辑:

- 将数据加载到对象 (通常从数据库中)。

- 创建对象的类型化集合。

- 向集合中添加对象和从集合中删除对象。

- 在窗体上向用户显示对象数据。

- 更改/编辑对象中的数据。

- 将对象中的数据保存回数据库。

### <a name="load-data-into-objects"></a>将数据加载到对象中

在此示例中, 使用 Tableadapter 将数据加载到对象。 默认情况下, 将使用两种方法创建 Tableadapter, 这些方法从数据库中提取数据并填充数据表。

- `TableAdapter.Fill`方法使用返回的数据填充现有数据表。

- `TableAdapter.GetData`方法返回用数据填充的新数据表。

使用数据加载自定义对象的最简单方法是调用`TableAdapter.GetData`方法, 遍历返回的数据表中的行集合, 并使用每行中的值填充每个对象。 您可以为添加`GetData`到 TableAdapter 的任何查询创建返回填充数据表的方法。

> [!NOTE]
> Visual Studio 会在默认情况`Fill`下`GetData`命名 TableAdapter 查询和, 但你可以将这些名称更改为任意有效的方法名称。

下面的示例演示如何遍历数据表中的行, 并使用数据填充对象:

[!code-csharp[VbRaddataConnecting#4](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_1.cs)]
[!code-vb[VbRaddataConnecting#4](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_1.vb)]

### <a name="create-a-typed-collection-of-objects"></a>创建对象的类型化集合

可以为对象创建集合类, 或使用[BindingSource 组件](/dotnet/framework/winforms/controls/bindingsource-component)自动提供的类型化集合。

为对象创建自定义集合类时, 建议您从<xref:System.ComponentModel.BindingList%601>继承。 此泛型类提供管理集合的功能, 以及在 Windows 窗体中引发将通知发送到数据绑定基础结构的事件的功能。

中自动生成的集合将<xref:System.Windows.Forms.BindingSource> <xref:System.ComponentModel.BindingList%601>用作其类型化集合。 如果你的应用程序不需要其他功能, 你可以在中维护你<xref:System.Windows.Forms.BindingSource>的集合。 有关详细信息, 请参阅<xref:System.Windows.Forms.BindingSource.List%2A> <xref:System.Windows.Forms.BindingSource>类的属性。

> [!NOTE]
> 如果你的集合需要的基础实现<xref:System.ComponentModel.BindingList%601>未提供的功能, 则应创建自定义集合, 以便可以根据需要将其添加到类中。

下面的代码演示如何创建`Order`对象的强类型集合的类:

[!code-csharp[VbRaddataConnecting#8](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_2.cs)]
[!code-vb[VbRaddataConnecting#8](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_2.vb)]

### <a name="add-objects-to-a-collection"></a>将对象添加到集合

通过调用`Add`自定义集合类或<xref:System.Windows.Forms.BindingSource>的方法, 将对象添加到集合。

> [!NOTE]
> 当`Add` 从<xref:System.ComponentModel.BindingList%601>继承时, 将自动为您的自定义集合提供方法。

下面的代码演示如何将对象添加到中<xref:System.Windows.Forms.BindingSource>的类型化集合:

[!code-csharp[VbRaddataConnecting#5](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_3.cs)]
[!code-vb[VbRaddataConnecting#5](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_3.vb)]

下面的代码演示如何将对象添加到从<xref:System.ComponentModel.BindingList%601>继承的类型化集合:

> [!NOTE]
> 在此示例中, `Orders`该集合是`Customer`对象的一个属性。

[!code-csharp[VbRaddataConnecting#6](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_4.cs)]
[!code-vb[VbRaddataConnecting#6](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_4.vb)]

### <a name="remove-objects-from-a-collection"></a>从集合中删除对象

您可以通过调用`Remove` `RemoveAt`自定义集合类或的<xref:System.Windows.Forms.BindingSource>方法, 从集合中移除对象。

> [!NOTE]
> 当从`RemoveAt` `Remove` 继承<xref:System.ComponentModel.BindingList%601>时, 将自动为您的自定义集合提供和方法。

下面的代码演示如何<xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingSource.RemoveAt%2A>使用方法在中查找和删除类型化集合中的对象:

[!code-csharp[VbRaddataConnecting#7](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_5.cs)]
[!code-vb[VbRaddataConnecting#7](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_5.vb)]

### <a name="display-object-data-to-users"></a>向用户显示对象数据

若要向用户显示对象中的数据, 请使用 "**数据源配置**向导" 创建一个对象数据源, 然后将整个对象或各个属性从 "**数据源**" 窗口拖到窗体上。

### <a name="modify-the-data-in-objects"></a>修改对象中的数据

若要编辑数据绑定到 Windows 窗体控件的自定义对象中的数据, 只需编辑绑定控件中的数据 (或直接在对象的属性中编辑)。 数据绑定体系结构更新对象中的数据。

如果你的应用程序需要跟踪更改, 并向其原始值回滚建议的更改, 则必须在对象模型中实现此功能。 有关数据表如何跟踪建议的更改的示例, 请参阅<xref:System.Data.DataRowState>、 <xref:System.Data.DataSet.HasChanges%2A>和<xref:System.Data.DataTable.GetChanges%2A>。

### <a name="save-data-in-objects-back-to-the-database"></a>将对象中的数据保存回数据库

通过将对象中的值传递给 TableAdapter 的 DBDirect 方法, 将数据保存回数据库。

Visual Studio 会创建可直接针对数据库执行的 DBDirect 方法。 这些方法不需要数据集或 DataTable 对象。

|TableAdapter DBDirect 方法|描述|
| - |-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库, 以便作为方法参数传入单独的列值。|
|`TableAdapter.Update`|更新数据库中的现有记录。 Update 方法将原始值和新列值作为方法参数使用。 原始值用于查找原始记录, 新值用于更新该记录。<br /><br /> <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow>方法还可通过将、、或数组<xref:System.Data.DataRow>作为方法参数, 将数据集中的更改协调回数据库。 `TableAdapter.Update`|
|`TableAdapter.Delete`|基于作为方法参数传入的原始列值删除数据库中的现有记录。|

若要保存对象集合中的数据, 请遍历对象的集合 (例如, 使用 for next 循环)。 使用 TableAdapter 的 DBDirect 方法将每个对象的值发送到数据库。

下面的示例演示如何使用`TableAdapter.Insert` DBDirect 方法将新客户直接添加到数据库中:

[!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_6.cs)]
[!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_6.vb)]

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)