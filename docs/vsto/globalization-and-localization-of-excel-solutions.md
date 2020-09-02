---
title: Excel 解决方案的全球化和本地化
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], configuring
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f37ddcbbd3145fc96cd8081d7a1df524ef7ea8ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72986046"
---
# <a name="globalization-and-localization-of-excel-solutions"></a>Excel 解决方案的全球化和本地化
  本节包含有关 Microsoft Office Excel 解决方案的特殊注意事项的信息，这些解决方案将在具有 Windows 非英语设置的计算机上运行。 全球化和本地化 Microsoft Office 解决方案过程中所遇到的大多数问题与使用 Visual Studio 创建其他各种解决方案时遇到的问题相同。 有关一般信息，请参阅 [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)。

 默认情况下，只要使用托管代码传递或操作的所有数据的格式都是使用“英语（美国）”格式设置进行设置的，Microsoft Office Excel 的宿主控件在任何 Windows 区域设置中均可正确工作。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]的项目中，此行为由公共语言运行时 (CLR) 控制。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="format-data-in-excel-with-various-regional-settings"></a>用各种区域设置在 Excel 中设置数据格式
 在将数据传递到 Microsoft Office Excel 或从 Office 项目中的代码读取数据之前，必须使用英语（美国）数据格式（区域设置 ID 1033）对具有区分区域设置格式的所有数据（例如日期和货币）进行格式设置。

 默认情况下，在 Visual Studio 中开发 Office 解决方案时，Excel 对象模型应为区域设置 ID 1033 数据格式（这也称为将对象模型锁定为区域设置 ID 1033）。 此行为与 Visual Basic for Applications 的运行方式相匹配。 但是，你可以在 Office 解决方案中修改此行为。

### <a name="understand-how-the-excel-object-model-always-expects-locale-id-1033"></a>了解 Excel 对象模型如何始终要求区域设置 ID 1033
 默认情况下，使用 Visual Studio 创建的 Office 解决方案不会受到最终用户区域设置的影响，并且其行为始终如同区域设置为英语（美国）一样。 例如，如果在 Excel 中获取或设置 <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> 属性，则必须按照区域设置 ID 1033 所要求的方式来设置数据格式。 如果使用不同的数据格式，可能会产生意外结果。

 即使你对由托管代码传递或操作的数据使用英语（美国）格式，Excel 仍然会根据最终用户的区域设置来正确解释并显示数据。 Excel 可以正确设置数据格式，因为托管代码将区域设置 ID 1033 与数据一起传递，这表示数据为英语（美国）格式，因此必须重新设置格式，使其与用户的区域设置相匹配。

 例如，如果最终用户将其区域选项设置为德语（德国）区域设置，则他们期望采用以下方式设置日期 2005 年 6 月 29 日的格式：29.06.2005。 但是，如果解决方案以字符串形式将该日期传递到 Excel，则必须依据英语（美国）格式 6/29/2005 设置该日期的格式。 如果将单元格格式化为日期单元格，则 Excel 将采用德语（德国）格式显示日期。

### <a name="pass-other-locale-ids-to-the-excel-object-model"></a>将其他区域设置 Id 传递到 Excel 对象模型
 公共语言运行时 (CLR) 会自动将区域设置 ID 1033 传递到接受区分区域设置的数据的 Excel 对象模型中的所有方法和属性。 无法为调入对象模型的所有调用自动更改此行为。 但是，通过使用 <xref:System.Type.InvokeMember%2A> 来调用方法以及将区域设置 ID 传递到方法的 *culture* 参数，可以将不同的区域设置 ID 传递到特定的方法。

## <a name="localize-document-text"></a>本地化文档文本
 项目中的文档、模板或工作簿中可能包含静态文本，静态文本必须与程序集和其他托管资源分开进行本地化。 完成此任务的一个直接的方法是，创建文档的副本，然后使用 Microsoft Office Word 或 Microsoft Office Excel 对文本进行翻译。 即使不对代码进行任何更改，此过程仍然有效，因为可将任意数量的文档链接到同一程序集。

 还必须确保与文档文本交互的任何代码部分都与文本的语言保持匹配，并确保书签、命名范围以及其他显示字段能够适应 Office 文档的重新格式化，针对不同语法和文本长度进行调整时需要该 Office 文档。 对于包含相对较少文本的文档模板，可以考虑在资源文件中存储文本，然后在运行时加载该文本。

### <a name="text-direction"></a>文本方向
 在 Excel 中，可以将工作表的属性设置为从右向左呈现文本。 放置在设计器上的宿主控件或任何具有 `RightToLeft` 属性的控件将在运行时自动匹配这些设置。 Word 没有针对双向文本的文档设置 (只更改文本) 的对齐方式，因此无法将控件映射到此设置。 相反，必须为每个控件设置文本对齐方式。 可以编写代码来遍历所有控件，并强制这些控件从右向左呈现文本。

### <a name="change-culture"></a>更改区域性
 文档级自定义项代码通常将共享 Excel 的主 UI 线程，因此，对线程区域性的任何更改都将影响在该线程上运行的所有其他内容；更改不会限制为针对自定义项。

 Windows 窗体控件在主机应用程序启动应用程序级 VSTO 外接程序之前进行初始化。 在这些情况下，应在设置 UI 控件之前更改区域性。

## <a name="install-the-language-packs"></a>安装语言包
 如果 Windows 具有非英语设置，则可安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 来以 Windows 使用的语言查看 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 消息。 如果最终用户使用 Windows 的非英语设置来运行你的解决方案，则他们必须具有相应的语言包来以 Windows 使用的语言查看运行时消息。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]可从[Microsoft 下载中心](https://www.microsoft.com/download)获得语言包。

 此外，可再发行的.NET Framework 语言包是 ClickOnce 消息所必需的。 可从 [Microsoft 下载中心](https://www.microsoft.com/download)获取 .NET Framework 语言包。

## <a name="regional-settings-and-excel-com-calls"></a>区域设置和 Excel COM 调用
 每当托管客户端对 COM 对象调用一个方法并且需要传入特定于区域性的信息时，它都使用与当前线程区域设置匹配的 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> （区域设置）来执行这些操作。 默认情况下，当前线程区域设置是从用户的区域设置继承而来的。 但是，当你从使用 Visual Studio 中的 Office 开发工具创建的 Excel 解决方案中调用 Excel 对象模型时，会自动将英语（美国）数据格式（区域设置 ID 1033）传递到 Excel 对象模型。 在将数据传递到 Microsoft Office Excel 或从项目代码中读取数据之前，必须使用英语（美国）数据格式对具有区分区域设置格式的所有数据（如日期和货币）进行格式设置。

## <a name="considerations-for-storing-data"></a>存储数据的注意事项
 若要确保正确解释和显示数据，还应考虑应用程序在字符串文本（硬编码）而不是在强类型对象中存储数据（例如 Excel 工作表公式）时可能发生的问题。 应使用采用区域性固定的样式或英语（美国）（LCID 值为 1033）样式进行格式设置的数据。

### <a name="applications-that-use-string-literals"></a>使用字符串文本的应用程序
 可硬编码的值包括用英语（美国）格式编写的日期文本，以及包含本地化函数名的 Excel 工作表公式。 还可能是包含数字（如“1,000”）的硬编码字符串；在某些区域性中，“1,000”被解释为一千，而在另一些区域性中它表示一点零。 根据错误的格式执行计算和比较会导致不正确的数据。

 Excel 根据随字符串传递的 LCID 解释所有字符串。 如果字符串的格式与传递的 LCID 不对应，则会出现问题。 使用 Visual Studio 中的 Office 开发工具创建的 Excel 解决方案在传递所有数据时都使用 LCID 1033 (en-US)。 Excel 根据区域设置和 Excel 用户界面语言显示数据。 Visual Basic for Applications (VBA) 也采用这种工作方式；字符串被设置为 en-US 格式，而 VBA 通常传递 0（非特定语言）作为 LCID。 例如，下面的 VBA 代码根据当前的用户区域设置，显示5月 12 2004 日的格式正确的值：

```vb
'VBA
Application.ActiveCell.Value2 = "05/12/04"
```

 当在通过 Visual Studio 中的 Office 开发工具创建的解决方案中使用，并通过 COM 互操作传递到 Excel 时，相同的代码在日期格式为 en-US 样式时会产生相同的结果。

 例如：

 [!code-vb[Trin_VstcoreCreatingExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#6)]
 [!code-csharp[Trin_VstcoreCreatingExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#6)]

 应尽可能使用强类型数据而不要使用字符串文本。 例如，不将日期存储为字符串格式，而是存储为 <xref:System.Double>，然后将其转换为 <xref:System.DateTime> 对象进行操作。

 下面的代码示例获取用户在单元格 A5 中输入的日期，将其存储为 <xref:System.Double>然后将其转换为 <xref:System.DateTime> 对象以在单元格 A7 中显示。 必须设置单元格 A7 的格式以显示日期。

 [!code-vb[Trin_VstcoreCreatingExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#7)]
 [!code-csharp[Trin_VstcoreCreatingExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#7)]

### <a name="excel-worksheet-functions"></a>Excel 工作表函数
 Excel 的大多数语言版本都在内部转换了工作表函数名。 但是，由于潜在的语言和 COM 互操作问题，建议你在代码中仅使用英语函数名称。

### <a name="applications-that-use-external-data"></a>使用外部数据的应用程序
 对于打开或以其他方式使用外部数据（如包含从旧系统中导出的逗号分隔值的文件（CSV 文件））的任何代码，如果这些文件是使用除 en-US 格式之外的任何格式导出的，则这些代码也会受到影响。 由于数据库中的所有值都应为二进制格式，因此只要数据库不将日期作为字符串存储且不执行不使用二进制格式的操作，数据库访问就不会受到影响。 另外，如果使用 Excel 中的数据构造 SQL 查询，则可能需要根据使用的函数来确保数据为 en-US 格式。

## <a name="see-also"></a>另请参阅

- [如何：面向 Office 多语言用户界面](../vsto/how-to-target-the-office-multilingual-user-interface.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)