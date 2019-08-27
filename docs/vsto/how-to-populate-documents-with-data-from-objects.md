---
title: 如何：用对象中的数据填充文档
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], populating with data
- data [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7cb221715ef1c2a50bc60e1725db3b1d8721f165
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967717"
---
# <a name="how-to-populate-documents-with-data-from-objects"></a>如何：用对象中的数据填充文档

在 Microsoft Office Word 文档级项目中，访问数据对象中的数据与访问 Windows 窗体项目中的数据的方式相同。 使用相同的工具和代码将数据从对象引入解决方案，然后即可使用 Windows 窗体控件来显示该数据。 此外，还可以使用主机控件来显示数据。 主机控件是指 Microsoft Office Word 中借助事件和数据绑定容量进行增强的本地对象。 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

必须完成三个基本步骤才能用对象中的数据填充文档：

- 将控件添加到可以绑定到数据的文档。

- 将数据对象添加到文档中。

- 将数据对象连接到 BindingSource。

## <a name="to-add-a-data-object"></a>若要添加数据对象

若要添加的数据对象，打开**数据源**窗口并从对象创建数据源。 有关详细信息，请参阅[添加新数据源](../data-tools/add-new-data-sources.md)。

## <a name="connect-the-data-object-to-the-bindingsource"></a>将数据对象连接到 BindingSource

在文档级项目中，可以在设计时向文档中添加控件并将其绑定到数据。

在 VSTO 外接程序项目中，可以在运行时创建并绑定控件。

### <a name="document-level-projects"></a>文档级项目

若要连接到 BindingSource 的数据对象：

1. 将所需数据字段从“数据源”  窗口拖动到你的文档。 此操作会自动创建一个控件。

2. 在代码中，可以创建为数据源选择的对象类型的实例。

3. 将实例分配给 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 的 <xref:System.Windows.Forms.BindingSource>属性。

### <a name="application-level-projects"></a>应用程序级项目

若要连接到 BindingSource 的数据对象：

1. 在代码中，可以创建与数据源关联的对象类型的实例。

2. 创建 <xref:System.Windows.Forms.BindingSource>的实例。

3. 将数据源实例分配给 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 的 <xref:System.Windows.Forms.BindingSource>属性。

4. 将数据源作为数据绑定添加到控件。

## <a name="see-also"></a>请参阅

- [添加新数据源](../data-tools/add-new-data-sources.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)