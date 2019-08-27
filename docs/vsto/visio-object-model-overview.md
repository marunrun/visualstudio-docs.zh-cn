---
title: Visio 对象模型概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Visio
- objects [Office development in Visual Studio], Office object models
- Office object models
- Visio object model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1ca692e85396b11647c507b18c95ca095b3f8072
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438754"
---
# <a name="visio-object-model-overview"></a>Visio 对象模型概述
  要为 Microsoft Office Visio 开发 Office 解决方案，则可以与 Visio 对象模型进行交互。 此对象模型包含 Visio 中主互操作程序集所提供的类和接口，并在 `Microsoft.Office.Interop.Visio` 命名空间中定义。

 本主题概要介绍 Visio 对象模型。 有关使用 Visio 对象模型在 Office 项目中执行任务的信息，请参阅以下主题：

- [使用 Visio 文档](../vsto/working-with-visio-documents.md)

- [使用 Visio 形状](../vsto/working-with-visio-shapes.md)

## <a name="understand-the-visio-object-model"></a>了解 Visio 对象模型
 Visio 提供了许多可与之交互的对象。 这些对象采用严格遵循用户界面的层次结构进行组织。 层次结构的顶部是 [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application) 对象。 此对象表示 Visio 的当前实例。 `Microsoft.Office.Interop.Visio.Application`对象包含`Microsoft.Office.Interop.Visio.Document`并`Microsoft.Office.Interop.Visio.Page`对象并将`Microsoft.Office.Interop.Visio.Documents`和`Microsoft.Office.Interop.Visio.Pages`集合。 每个对象和集合都有许多方法和属性，可进行访问以便操作并与其进行交互。

 有关详细信息，请参阅适用于 [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application)、 [Microsoft.Office.Interop.Visio.Document](/office/vba/api/Visio.Document)和 [Microsoft.Office.Interop.Visio.Page](/office/vba/api/Visio.Page) 对象，以及 [Microsoft.Office.Interop.Visio.Documents](/office/vba/api/Visio.Documents) 和 [Microsoft.Office.Interop.Visio.Pages](/office/vba/api/Visio.Pages) 集合的 VBA 的参考文档。

 下列各节简要介绍了顶级对象以及它们彼此交互的方式。 这些对象包括以下对象：

- 应用程序对象

- 文档对象

- Page 对象

### <a name="application-object"></a>应用程序对象
 Microsoft.Office.Interop.Visio.Application 对象表示 Visio 应用程序，并且所有其他对象的父级。 其成员通常作为一个整体应用于 Visio。 可以使用的属性和方法 Microsoft.Office.Interop.Visio.Application 和`Microsoft.Office.Interop.Visio.ApplicationSettings`对象来控制 Visio 环境。

 在 VSTO 外接程序项目中，可以通过访问 Microsoft.Office.Interop.Visio.Application 对象`Application`字段的`ThisAddIn`类。 有关详细信息，请参阅 [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md)。

### <a name="document-object"></a>文档对象
 Microsoft.Office.Interop.Visio.Document 对象是 Visio 编程的核心。 它表示绘图、模具或模板文件。 当您打开 Visio 文档，或创建新文档时，创建到 Microsoft.Office.Interop.Visio.Documents Microsoft.Office.Interop.Visio.Application 对象的集合添加一个新 Microsoft.Office.Interop.Visio.Document 对象.

 具有焦点的文档被称为活动文档。 由表示`Microsoft.Office.Interop.Visio.Application.ActiveDocument`Microsoft.Office.Interop.Visio.Application 对象的属性。

### <a name="page-object"></a>Page 对象
 Microsoft.Office.Interop.Visio.Page 对象表示前景页或背景页的绘图区域。 可以使用 `Microsoft.Office.Interop.Visio.Page.Background` 属性来确定某页是前景页还是背景页。

 若要创建形状，则可以使用包含 `Microsoft.Office.Interop.Visio.Page.DrawSpline` 和 `Microsoft.Office.Interop.Visio.Page.DrawOval` 方法的方法。 此外，可以通过使用 `Microsoft.Office.Interop.Visio.Page.Drop` 或 `Microsoft.Office.Interop.Visio.Page.DropMany` 方法从模具检索母板，并将形状放置在页面上。

## <a name="use-the-visio-object-model-documentation"></a>使用 Visio 对象模型文档
 有关 Visio 对象模型的完整信息，可以参考 Visio VBA 对象模型引用。 VBA 对象模型引用在 Visio 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅[Visio 2010 对象模型引用](http://go.microsoft.com/fwlink/?LinkId=199775)。

 VBA 对象模型引用中的所有对象和成员都对应于 Visio 主互操作程序集 (PIA) 中的类型和成员。 例如， `Document` VBA 对象模型引用中的对象对应于 Visio PIA 中的 Microsoft.Office.Interop.Visio.Document 类型。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果想要将其用于使用 Visual Studio 创建的 Visio VSTO 外接程序项目，则必须将本引用中的 VBA 代码转换成 Visual Basic 或 Visual C#。

> [!NOTE]
> 此时，没有任何 Visio 主互操作程序集的参考文档。

 有关相关的代码示例和创建 Visio 解决方案的其他工具，请参阅[Visio 2010 软件开发工具包](http://go.microsoft.com/fwlink/?LinkId=196501)。

### <a name="additional-types-in-primary-interop-assemblies"></a>主互操作程序集中的其他类型
 可以在主互操作程序集中找到因为实现不同而对 VBA 不可见的类型。 VBA 提供 Visio 对象模型的视图，该视图仅包括可以直接使用的对象和成员。 主互操作程序集公开相同的对象模型，但它们还包括将 COM 对象模型中的对象转换为托管代码的其他接口、类和的成员。 这些附加项不应直接在代码中使用。

 有关详细信息，请参阅[概述中 Office 主互操作程序集类和接口](http://go.microsoft.com/fwlink/?LinkId=189592)并[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="see-also"></a>请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [使用 Visio 文档](../vsto/working-with-visio-documents.md)
- [使用 Visio 形状](../vsto/working-with-visio-shapes.md)
