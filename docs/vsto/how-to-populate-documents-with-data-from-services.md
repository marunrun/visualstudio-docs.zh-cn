---
title: 如何：用服务中的数据填充文档
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], populating with data
- Web services [Office development in Visual Studio], populating documents
- data [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 01e2a83f464576d1ca780daa17c0d9478f0caa14
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547142"
---
# <a name="how-to-populate-documents-with-data-from-services"></a>如何：用服务中的数据填充文档

访问 Microsoft Office 文档级项目中的数据与访问 Windows 窗体项目中的数据的方式相同。 使用相同的工具和代码将数据引入解决方案，然后即可使用 Windows 窗体控件来显示该数据。 此外，可以利用称为“宿主控件”的控件，该控件是指 Microsoft Office Excel 和 Microsoft Office Word 中借助事件和数据绑定容量进行增强的本地对象。 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

[!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

下列示例演示了如何在设计时向文档中添加数据绑定控件。 有关如何在运行时在 VSTO 外接程序中添加数据绑定控件的示例，请参阅[演练：在 Vsto 外接程序项目中绑定到服务中的数据](../vsto/walkthrough-binding-to-data-from-a-service-in-a-vsto-add-in-project.md)。

## <a name="to-populate-a-document-level-project-with-data-from-a-web-service"></a>使用 web 服务中的数据填充文档级项目

1. 打开“数据源” **** 窗口并为项目创建服务数据源。 有关详细信息，请参阅[添加新数据源](../data-tools/add-new-data-sources.md)。

2. 将所需的表或字段从“数据源” **** 窗口拖动到你的文档。

     在文档中创建控件，创建绑定到项目中的对象类的 <xref:System.Windows.Forms.BindingSource> ，并为该服务生成类。

3. 在代码中，创建一个在步骤1中连接的 web 服务类的实例。

4. 如果存在与 web 服务进行通信所需的属性，则创建这些属性的实例。

5. 使用 Web 服务公开的方法和第 4 步中创建的任何属性实例创建并发送数据请求。

     使用的方法取决于 web 服务提供的功能。

6. 将 web 服务的数据响应分配给 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 的属性 <xref:System.Windows.Forms.BindingSource> 。

运行项目时，控件显示数据源中的第一条记录。 可以通过使用 <xref:System.Windows.Forms.BindingSource>中的对象处理货币事件，从而滚动记录。

## <a name="see-also"></a>另请参阅

- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [添加新数据源](../data-tools/add-new-data-sources.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [如何：用数据库中的数据填充工作表](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [如何：用对象中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)