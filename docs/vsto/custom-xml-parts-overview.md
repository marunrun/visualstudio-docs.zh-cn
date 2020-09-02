---
title: 自定义 XML 部件概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom XML parts [Office development in Visual Studio], about
- Office Open XML Formats [Office development in Visual Studio]
- custom XML parts [Office development in Visual Studio]
- embedding XML data in documents [Office development in Visual Studio]
- XML parts [Office development in Visual Studio]
- XML file formats [Office development in Visual Studio]
- data [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- XML [Office development in Visual Studio], custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- documents [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b94deacad38f40d76b4c8485186bfd563808d912
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "64784427"
---
# <a name="custom-xml-parts-overview"></a>自定义 XML 部件概述
  对于某些 Microsoft Office 应用程序，可在文档中嵌入 XML 数据。 在文档中嵌入 XML 数据时，数据将被命名为 *自定义 XML 部件*。

 可使用 Visual Studio 中的 VSTO 外接程序或文档级解决方案来创建和修改自定义 XML 部件。 无需启动 Microsoft Office 应用程序来创建和修改自定义 XML 部件。

 **适用于：** 本主题中的信息适用于 Excel、PowerPoint 和 Word 的文档级别项目和 VSTO 外接程序项目。 有关详细信息，请参阅 [按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

> [!NOTE]
> Visual Studio 还使你能够在文档级自定义项中缓存数据对象。 尽管有一些相似之处，此功能并不同于自定义 XML 部件。 有关详细信息，请参阅 [文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)。

## <a name="understand-custom-xml-parts"></a>了解自定义 XML 部件
 自定义 XML 部件和 Open XML 格式一起在 2007 Microsoft Office 系统中引入。 这些格式包括新的基于 XML 的文件格式，适用于 Excel、PowerPoint 和 Word (例如 *.xlsx*、 *.pptx*和 *.docx*) 。 采用这些格式的文档包括 XML 文件 (也称为 *xml part*) ，这些部件在 ZIP 存档的文件夹中进行组织。 大多数 XML 部件为有助于定义文档的结构和状态的内置部件。 但文档还可包含自定义 XML 部件，可用于将任意 XML 数据存储在文档中。

 使用 XML 文件格式，应用程序可以使用较旧的二进制文件格式不可能的方式来处理文档， (如 *.xls*、 *.ppt*和 *.doc*) 。 可读取 ZIP 存档的所有应用程序都可检查和修改文档内容，即使未安装 Microsoft Office。

 有关 Open XML 和自定义 XML 部件的结构的详细信息，请参阅以下文章：

- [引入 Office (2007) Open XML 文件格式](/previous-versions/office/developer/office-2007/aa338205(v=office.12))

- [如何：处理开放式 XML 格式文档](/previous-versions/office/developer/office-2007/aa982683(v=office.12))

- [演练： Word 2007 XML 格式](/previous-versions/office/developer/office-2007/bb266220(v=office.12))

- [使用 Open XML 格式生成 Word 2007 文档](/previous-versions/office/developer/office-2007/bb264572(v=office.12))

> [!NOTE]
> Excel、Word 和 PowerPoint 还使你可以使用以二进制文件格式保存的文档中的自定义 XML 部件。 但如果文档以二进制格式保存，则无法添加或修改自定义 XML 部件，除非启动 Microsoft Office 应用程序。

## <a name="create-and-modify-custom-xml-parts"></a>创建和修改自定义 XML 部件
 当文档在 Office 应用程序中打开时，或当文档关闭时，可创建或修改自定义 XML 部件，即使未安装 Microsoft Office。

### <a name="modify-xml-parts-while-the-office-application-is-running"></a>Office 应用程序运行时修改 XML 部件
 可以通过使用文档级自定义项或 VSTO 外接程序来使用自定义 XML 部件。 如果使用文档级自定义项，通常将使用自定义文档中的自定义 XML 部件。 如果你使用的是 VSTO 外接程序，则可以在应用程序中打开的任何文档中创建或修改自定义 XML 部件。

 若要通过使用 Visual Studio 来创建自定义 XML 部件，请将新的 <xref:Microsoft.Office.Core.CustomXMLPart> 添加到文档中的 <xref:Microsoft.Office.Core.CustomXMLParts> 集合。 有关详细信息，请参阅下列主题：

- [如何：向文档级自定义项添加自定义 XML 部件](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)

- [如何：使用 VSTO 外接程序将自定义 XML 部件添加到文档](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)

### <a name="modify-xml-parts-without-starting-the-office-application"></a>无需启动 Office 应用程序即可修改 XML 部件
 可在不启动 Excel、PowerPoint 或 Word 的情况下添加或修改自定义 XML 部件。 需在未安装 Microsoft Office 应用程序的计算机（如服务器）上使用文档中的 XML 数据时，这将非常有用。

 若要在不启动 Microsoft Office 的情况下添加自定义 XML 部件，请使用 Open XML SDK 中的类。 这些类旨在提供对特定于 Office 文档的 Open XML 内容的访问。 例如，若要向 Excel 工作簿添加自定义 XML 部件，请使用 <xref:DocumentFormat.OpenXml.Packaging.OpenXmlPartContainer.AddNewPart%2A> 对象的方法 <xref:DocumentFormat.OpenXml.Packaging.WorkbookPart> 。 有关详细信息，请参阅 [OPEN XML SDK](/office/open-xml/open-xml-sdk)。

## <a name="bind-custom-xml-parts-to-word-content-controls"></a>将自定义 XML 部件绑定到 Word 内容控件
 可将 Word 解决方案中的内容控件绑定到自定义 XML 部件中的元素。 当内容控件绑定到自定义 XML 部件时，自定义 XML 部件中的数据将显示在内容控件的用户界面 (UI)。 如果用户编辑控件中的文本，则将自动更新相应的 XML 元素。 同样，如果自定义 XML 部件中的元素值发生更改，则绑定到 XML 元素的内容控件将显示新的数据。 有关详细信息，请参阅 [内容控件](../vsto/content-controls.md)。

## <a name="see-also"></a>另请参阅
- [文档级自定义项中的 XML 架构和数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
- [如何：向文档级自定义项添加自定义 XML 部件](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)
- [如何：使用 VSTO 外接程序将自定义 XML 部件添加到文档](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)
- [内容控件](../vsto/content-controls.md)
- [演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)
