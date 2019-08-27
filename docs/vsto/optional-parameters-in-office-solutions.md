---
title: Office 解决方案中的可选参数
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], optional parameters
- Visual C# [Office development in Visual Studio], optional parameters
- Visual Basic [Office development in Visual Studio], optional parameters
- application development [Office development in Visual Studio], optional parameters
- missing field [Office development in Visual Studio]
- optional parameters [Office development in Visual Studio]
- parameters [Office development in Visual Studio], optional
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e8684ad4b9429a5499660ef4ad6fdd8133dccaa5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442419"
---
# <a name="optional-parameters-in-office-solutions"></a>Office 解决方案中的可选参数
  Microsoft Office 应用程序的对象模型中的许多方法都接受可选参数。 如果使用 Visual Basic 在 Visual Studio 中开发 Office 解决方案，你不必为可选参数传递值，因为系统会为每个缺少的参数自动使用默认值。 在大多数情况下，也可以省略 Visual C# 项目中的可选参数。 但是，您不能省略可选**ref**的参数`ThisDocument`在文档级 Word 项目中的类。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 有关使用 Visual C# 和 Visual Basic 项目中的可选参数的详细信息，请参阅[命名参数和可选参数&#40;C&#35;编程指南&#41;](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)并[&#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters)。

> [!NOTE]
> 在 Visual Studio 的早期版本中，必须为 Visual C# 项目中的每个可选参数传递一个值。 为了方便起见，这些项目包括一个名为 `missing` 的全局变量，当你想要使用某个可选参数的默认值时，可以将该变量传递给该可选参数。 Visual C# 项目在 Visual Studio 中的 office 仍然包含`missing`变量，但你通常不需要开发中的 Office 解决方案时使用它[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]，当您调用具有可选的方法除外**ref**中的参数`ThisDocument`Word 的文档级项目中的类。

## <a name="example-in-excel"></a>Excel 中的示例
 <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> 方法具有多个可选参数。 可以为某些参数指定值，并接受其他参数的默认值，如下面的代码示例所示。 此示例需要一个具有名为 `Sheet1` 的工作表类的文档级项目。

 [!code-csharp[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs#1)]
 [!code-vb[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb#1)]

## <a name="example-in-word"></a>Word 中的示例
 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 方法具有多个可选参数。 可以为某些参数指定值，并接受其他参数的默认值，如下面的代码示例所示。

 [!code-vb[Trin_VstrefGeneralWord#1](../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstrefGeneralWord#1](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#1)]

## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Word ThisDocument 类中 Visual C# 文档级项目中使用方法的可选的参数
 Word 对象模型包含许多方法具有可选**ref**接受的参数<xref:System.Object>值。 但是，您不能省略可选**ref**所生成的方法的参数`ThisDocument`Word 的 Visual C# 文档级项目中的类。 Visual C#，可省略可选**ref**参数仅对方法的接口，而不是类。 例如，下面的代码示例不会进行编译，因为不能省略可选**ref**的参数<xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A>方法的`ThisDocument`类。

 [!code-csharp[Trin_VstrefGeneralWord#3](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#3)]

 调用 `ThisDocument` 类的方法时，请遵循以下准则：

- 若要接受默认值的可选**ref**参数，传递`missing`变量到参数。 在 Visual C# Office 项目中自动定义 `missing` 变量，并分配给生成的项目代码中的值 <xref:System.Type.Missing>。

- 若要指定自己的值的可选**ref**参数，分配给你想要指定，值将对象声明，然后将该对象传递给参数。

  下面的代码示例演示如何调用<xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A>方法，并指定的值*ignoreUppercase*参数并接受其他参数的默认值。

  [!code-csharp[Trin_VstrefGeneralWord#4](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#4)]

  如果你想要编写代码的省略了可选**ref**中的方法的参数`ThisDocument`类，您可以或者调用相同的方法上<xref:Microsoft.Office.Interop.Word.Document>返回对象<xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A>属性，并省略该方法的参数。 可以这样做是因为 <xref:Microsoft.Office.Interop.Word.Document> 是接口而不是类。

  [!code-csharp[Trin_VstrefGeneralWord#5](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#5)]

  有关值和引用类型参数的详细信息，请参阅[按值和按引用传递参数&#40;Visual Basic&#41; ](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) （对于 Visual Basic) 和[将参数传递给&#40;C&#35;编程指南&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters)。

## <a name="see-also"></a>请参阅
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
