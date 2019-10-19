---
title: 示例 Excel 扩展：Element 类 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 7c251098-00aa-49cf-9e37-5717c0c6b3f1
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 21c7777be710f0175708629eb9507b34f0d70be2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660454"
---
# <a name="sample-excel-extension-element-classes"></a>示例 Excel 扩展：Element 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

该扩展使用从 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> 派生的类，并表示 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 中的工作表控件和单元控件。

 此扩展的基本元素是 `ExcelElement`。 `ExcelWorksheetElement` 类和 `ExcelCellElement` 类继承自此元素

## <a name="element-and-elementinformation-classes"></a>Element 类和 ElementInformation 类
 `Element` 是 Excel 扩展的所有用户界面元素的基类，它继承自 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> 类。 `ElementInformation` 是示例中元素信息类的基类，它没有成员。

#### <a name="simple-properties-and-methods"></a>简单的属性和方法
 这些成员返回简单的值，例如 `Name` 属性的值或 `ClassName` 属性的值，并且代码清晰、易读。 一些值使用 `Utility` 类返回，该类将在后面说明。 其他成员返回 `null`，因为它们不是此示例扩展的有关成员。 有两个成员比其他成员更加有趣：<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A> 属性和 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.CacheProperties%2A> 方法。

#### <a name="queryid-property"></a>QueryId 属性
 此属性返回由名称/值对表示的条件，此名称/值对唯一标识播放期间的控件。 对于每个派生的控件类，开发者必须重写此属性以返回可供框架查找 UI 中的控件的 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement> 对象。

#### <a name="cacheproperties-method"></a>CacheProperties 方法
 在录制过程中测试框架调用此方法来告知元素保存重要属性的快照。 这样即使实际的 UI 控件已不再在屏幕上，也可以保持属性可用。

## <a name="worksheetelement-and-worksheetinformation-classes"></a>WorksheetElement 和 WorksheetInformation 类
 `WorksheetElement` 类代表测试框架中的 Excel 工作表，并继承自 `Element` 基类。 将重写三个属性，以提供有关 Excel 工作表对象的具体信息：<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.ClassName%2A><xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.ControlTypeName%2A> 和 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.Name%2A>。

 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 也适用于此类，以使其对 COM 可见。

 `WorksheetInformation` 类表示有关 Excel 工作表的信息。 它只有一个成员，`SheetName` 属性，这对于本示例已足够。

## <a name="cellelement-and-cellinformation-classes"></a>CellElement 和 CellInformation 类
 `CellElement` 类表示一个 Excel 单元格，继承自 `Element` 基类。 重写的唯一成员是 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A> 属性，该属性返回使用 `RowIndex` 和 `ColumnIndex` 属性标识单元的 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement>。

## <a name="utilities-and-excelutilities-classes"></a>Utilities 和 ExcelUtilities 类
 内部 `ExcelUtilities` 类提供了一些常量值，例如技术名称和确定提供的窗口句柄是否代表 Excel 工作表的方法。

 `Utilities` 类具有返回有关 UI 的各种信息的帮助程序方法。 某些方法直接调用外部系统 DLL，如 **USER32.DLL** 和 **OLEACC.DLL**，以从 UI 获取窗口句柄<strong>。</strong>

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement>
 [扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)
