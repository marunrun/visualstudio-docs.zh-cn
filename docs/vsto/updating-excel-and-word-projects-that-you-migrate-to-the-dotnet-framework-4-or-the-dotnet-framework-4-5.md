---
title: 更新 Excel 或 Word 项目已迁移到 .NET Framework 4/4。5
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4bc211f4d30359c885b22a45910363bbadca236f
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253723"
---
# <a name="update-excel-and-word-projects-that-you-migrate-to-the-net-framework-4-or-the-net-framework-45"></a>更新迁移到 .NET Framework 4 或 .NET Framework 4.5 的 Excel 和 Word 项目
  如果你的一个 Excel 或 Word 项目使用以下任何功能，且如果目标框架更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须修改你的代码：

- [GetVstoObject 和 HasVstoObject 方法](#GetVstoObject)

- [文档级项目中生成的类](#generatedclasses)

- [文档上的 Windows 窗体控件](#winforms)

- [Word 内容控件事件](#ccevents)

- [OLEObject 和 OLEControl 类](#ole)

- [Controls.Item(Object) 属性](#itemproperty)

- [从 CollectionBase 派生的集合](#collections)

  您还必须从重`Microsoft.Office.Tools.Excel.ExcelLocale1033Attribute`定向到[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更`Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy`高版本的 Excel 项目中删除和对类的引用。 Visual Studio 不会为你删除此属性或类引用。

## <a name="remove-the-excellocale1033-attribute-from-excel-projects"></a>从 Excel 项目中删除 ExcelLocale1033 属性
 已从用于[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]面向或更高版本的解决方案的 Visual Studio 2010 Tools for Office 运行时中删除。 `Microsoft.Office.Tools.Excel.ExcelLocale1033Attribute` [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 和更高版本中的公共语言运行时 (CLR) 始终将区域设置 ID 1033 传递给 Excel 对象模型，且你无法再使用此属性来禁用此行为。 有关详细信息，请参阅[Excel 解决方案的全球化和本地化](../vsto/globalization-and-localization-of-excel-solutions.md)。

### <a name="to-remove-the-excellocale1033attribute"></a>若要删除 ExcelLocale1033Attribute

1. 在 Visual Studio 中打开项目后，打开 **“解决方案资源管理器”** 。

2. 在 C# 的 **“属性”** 节点或在 Visual Basic 的 **“我的项目”** 节点下，双击 AssemblyInfo 代码文件以在代码编辑器中打开它。

    > [!NOTE]
    > 在 Visual Basic 项目中，必须单击 **“解决方案资源管理器”** 中的 **“显示所有文件”** 按钮，才能查看 AssemblyInfo 代码文件。

3. 找到 `Microsoft.Office.Tools.Excel.ExcelLocale1033Attribute` 并且将其从文件中删除或注释掉。

    ```vb
    <Assembly: ExcelLocale1033Proxy(True)>
    ```

    ```csharp
    [assembly: ExcelLocale1033Proxy(true)]
    ```

## <a name="remove-a-reference-to-the-excellocal1033proxy-class"></a>删除对对 excellocal1033proxy 类的引用
 使用 Microsoft Visual Studio 2005 Tools for the Microsoft Office System 创建的项目通过使用 `Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy` 类实例化 Excel <xref:Microsoft.Office.Interop.Excel.Application> 对象。 此类已从用于面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本的解决方案的 Visual Studio 2010 Tools for Office 运行时中删除。 因此，你必须删除或注释禁用引用此类的代码行。

### <a name="to-remove-the-reference-to-the-excellocal1033proxy-class"></a>若要删除对 ExcelLocal1033Proxy 类的引用

1. 在 Visual Studio 中打开该项目，然后打开 **“解决方案资源管理器”** 。

2. 在**解决方案资源管理器**中，打开*ThisAddin.cs* （适用C#于）或*ThisAddin* （对于 Visual Basic）的快捷菜单，然后选择 "**查看代码**"。

3. 在代码编辑器的 `VSTO generated code` 区域中，删除或注释禁用以下代码行。

    ```vb
    Me.Application = CType(Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy.Wrap(GetType(Excel.Application), Me.Application), Excel.Application)

    ```

    ```csharp
    this.Application = (Excel.Application)Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy.Wrap(typeof(Excel.Application), this.Application);

    ```

## <a name="GetVstoObject"></a>更新使用 GetVstoObject 和 HasVstoObject 方法的代码
 在面向 .NET Framework 3.5 的项目中，`GetVstoObject` 或 `HasVstoObject` 方法在你项目中的以下本机对象之一上都可用作扩展方法：<xref:Microsoft.Office.Interop.Word.Document>、<xref:Microsoft.Office.Interop.Excel.Workbook>、<xref:Microsoft.Office.Interop.Excel.Worksheet> 或 <xref:Microsoft.Office.Interop.Excel.ListObject>。 当调用这些方法时，你不需要传递参数。 下面的代码示例演示如何在面向 .NET Framework 3.5 的 Word VSTO 外接程序中使用 GetVstoObject 方法。

```vb
Dim vstoDocument as Microsoft.Office.Tools.Word.Document = _
    Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject()
```

```csharp
Microsoft.Office.Tools.Word.Document vstoDocument =
    Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject();
```

 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，必须修改代码才能按照以下方式之一访问这些方法：

- 你仍可以在 <xref:Microsoft.Office.Interop.Word.Document>、 <xref:Microsoft.Office.Interop.Excel.Workbook>、 <xref:Microsoft.Office.Interop.Excel.Worksheet>或 <xref:Microsoft.Office.Interop.Excel.ListObject> 对象上将这些方法作为扩展方法访问。 但是，现在你必须将 `Globals.Factory` 属性返回的对象传递给这些方法。

  ```vb
  Dim vstoDocument as Microsoft.Office.Tools.Word.Document = _
      Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject(Globals.Factory)
  ```

  ```csharp
  Microsoft.Office.Tools.Word.Document vstoDocument =
      Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject(Globals.Factory);
  ```

- 或者，你可以在 `Globals.Factory` 属性返回的对象上访问这些方法。 当你以这种方式访问这些方法时，则必须将想要扩展的本机对象传递给该方法。

  ```vb
  Dim vstoDocument as Microsoft.Office.Tools.Word.Document = _
      Globals.Factory.GetVstoObject(Globals.ThisAddIn.Application.ActiveDocument)
  ```

  ```csharp
  Microsoft.Office.Tools.Word.Document vstoDocument =
      Globals.Factory.GetVstoObject(Globals.ThisAddIn.Application.ActiveDocument);
  ```

  有关详细信息，请参阅[在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="generatedclasses"></a>更新使用文档级项目中生成的类的实例的代码
 在面向 .NET Framework 3.5 的文档级项目中，项目中生成的类派生自 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]中的以下类：

- `ThisDocument`: <xref:Microsoft.Office.Tools.Word.Document>

- `ThisWorkbook`: <xref:Microsoft.Office.Tools.Excel.Workbook>

- `Sheet`*n*：<xref:Microsoft.Office.Tools.Excel.Worksheet>

- `Chart`*n*：<xref:Microsoft.Office.Tools.Excel.ChartSheet>

  在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，上面所列的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 中的类型是接口，而不是类。 面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中生成的类派生自 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]中的以下新类：

- `ThisDocument`: <xref:Microsoft.Office.Tools.Word.DocumentBase>

- `ThisWorkbook`: <xref:Microsoft.Office.Tools.Excel.WorkbookBase>

- `Sheet`*n*：<xref:Microsoft.Office.Tools.Excel.WorksheetBase>

- `Chart`*n*：<xref:Microsoft.Office.Tools.Excel.ChartSheetBase>

  如果项目中的代码将某个生成的类的实例引用为它派生自的基类，则必须修改该代码。

  例如，在面向 .NET Framework 3.5 的 Excel 工作簿项目中，可能存在一个帮助程序方法，该方法在项目中生成的 `Sheet`*n* 类的实例上执行某些工作。

```vb
Private Sub DoSomethingToSheet(ByVal worksheet As Microsoft.Office.Tools.Excel.Worksheet)
    ' Do something to the worksheet object.
End Sub
```

```csharp
private void DoSomethingToSheet(Microsoft.Office.Tools.Excel.Worksheet worksheet)
{
    // Do something to the worksheet object.
}
```

 如果你将项目重定向到 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须对代码进行以下更改之一：

- 修改调用 `DoSomethingToSheet` 方法的任何代码来传递你的项目中的 <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Base%2A> 对象的 <xref:Microsoft.Office.Tools.Excel.WorksheetBase> 属性。 该属性返回一个 <xref:Microsoft.Office.Tools.Excel.Worksheet> 对象。

    ```vb
    DoSomethingToSheet(Globals.Sheet1.Base)
    ```

    ```csharp
    DoSomethingToSheet(Globals.Sheet1.Base);
    ```

- 修改 `DoSomethingToSheet` 方法参数以预期返回 <xref:Microsoft.Office.Tools.Excel.WorksheetBase> 对象。

    ```vb
    Private Sub DoSomethingToSheet(ByVal worksheet As Microsoft.Office.Tools.Excel.WorksheetBase)
        ' Do something to the worksheet object.
    End Sub
    ```

    ```csharp
    private void DoSomethingToSheet (Microsoft.Office.Tools.Excel.WorksheetBase worksheet)
    {
        // Do something to the worksheet object.
    }
    ```

## <a name="winforms"></a>更新使用文档上 Windows 窗体控件的代码
 您必须将<xref:Microsoft.Office.Tools.Excel>或 C# 命名<xref:Microsoft.Office.Tools.Word>空间的 using （）或 Imports （Visual Basic）语句添加到使用 Controls 属性的任何代码文件的顶部，以将 Windows 窗体控件添加到文档或工作表中。通过.

 在面向 .NET Framework 3.5 的项目中，添加 Windows 窗体控件的方法（如 `AddButton` 方法）在 <xref:Microsoft.Office.Tools.Excel.ControlCollection> 和 <xref:Microsoft.Office.Tools.Word.ControlCollection> 类中定义。

 在面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本的项目中，这些方法是控件属性上提供的扩展方法。 若要使用这些扩展方法，你在其中使用这些方法的代码文件必须具有 **N:Microsoft.Office.Tools.Excel** 或 **N:Microsoft.Office.Tools.Word** 命名空间的 <xref:Microsoft.Office.Tools.Excel> 或 <xref:Microsoft.Office.Tools.Word> 语句。 此语句在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的新项目中自动生成。 但是，此语句不自动添加到面向 .NET Framework 3.5 的项目中，因此当你重定向项目时必须添加它。

 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="ccevents"></a>更新处理 Word 内容控件事件的代码
 在面向 .NET Framework 3.5 的项目中，Word 内容控件的事件由泛型 <xref:System.EventHandler%601> 委托处理。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些事件由其他委托处理。

 下表列出了 Word 内容控件事件以及在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中与它们关联的委托。

|事件|委托在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 和更高版本的项目中使用|
|-----------| - |
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Added>|<xref:Microsoft.Office.Tools.Word.ContentControlAddedEventHandler>|
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.ContentUpdating>|<xref:Microsoft.Office.Tools.Word.ContentControlContentUpdatingEventHandler>|
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Deleting>|<xref:Microsoft.Office.Tools.Word.ContentControlDeletingEventHandler>|
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering>|<xref:Microsoft.Office.Tools.Word.ContentControlEnteringEventHandler>|
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Exiting>|<xref:Microsoft.Office.Tools.Word.ContentControlExitingEventHandler>|
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating>|<xref:Microsoft.Office.Tools.Word.ContentControlStoreUpdatingEventHandler>|

## <a name="ole"></a>更新使用 OLEObject 和 OLEControl 类的代码
 在面向 .NET Framework 3.5 的项目中，你可以使用 `Microsoft.Office.Tools.Excel.OLEObject` 和 `Microsoft.Office.Tools.Word.OLEControl` 类向文档或工作表添加自定义控件（如 Windows 窗体用户控件）。

 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些类已替换为 <xref:Microsoft.Office.Tools.Excel.ControlSite> 和 <xref:Microsoft.Office.Tools.Word.ControlSite> 接口。 你必须修改代码，使其引用 <xref:Microsoft.Office.Tools.Excel.ControlSite> 和 <xref:Microsoft.Office.Tools.Word.ControlSite> 而不再引用 `Microsoft.Office.Tools.Excel.OLEObject` 和 `Microsoft.Office.Tools.Word.OLEControl`。 不同于新名称，这些控件的行为方式与它们在面向 .NET Framework 3.5 的项目中的行为方式相同。

 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="itemproperty"></a>更新使用 Controls （Object）属性的代码
 在面向 .NET Framework 3.5 的项目中，您可以使用 Microsoft 的 Item （Object）属性或`Microsoft.Office.Tools.Excel.Worksheet.Controls`集合来确定文档或工作表是否具有指定的控件。

 在面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本的项目中，已从这些集合中删除 Item （Object）属性。 若要确定文档或工作表是否包含指定的控件，请改为使用<xref:Microsoft.Office.Tools.Word.Document.Controls%2A>或<xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A>集合的 contains （system.object）方法。

 有关文档和工作表的控件集合的详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="collections"></a>更新使用派生自 CollectionBase 的集合的代码
 在面向 .NET Framework 3.5 的项目[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]中，中的几个集合类型派生<xref:System.Collections.CollectionBase>自类，例如`Microsoft.Office.Tools.SmartTagCollection`、 `Microsoft.Office.Tools.Excel.ControlCollection`和`Microsoft.Office.Tools.Word.ControlCollection`。

 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些集合类型现在是非派生自 <xref:System.Collections.CollectionBase>的接口。 一些成员在这些集合类型上不再可用，如 <xref:System.Collections.CollectionBase.Capacity%2A>、 <xref:System.Collections.CollectionBase.List%2A>和 <xref:System.Collections.CollectionBase.InnerList%2A>。

## <a name="see-also"></a>请参阅
- [将 Office 解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [内容控件](../vsto/content-controls.md)
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
