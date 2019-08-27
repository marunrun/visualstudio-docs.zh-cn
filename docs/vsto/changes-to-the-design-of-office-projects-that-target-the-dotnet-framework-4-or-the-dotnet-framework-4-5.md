---
title: 面向.NET Framework 的 Office 项目的设计更改
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio 2010, what's new
- what's new [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7f2c4176c0aab4340648feee0b709f9dfd472ca0
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177585"
---
# <a name="changes-to-the-design-of-office-projects-that-target-the-net-framework-4-or-the-net-framework-45"></a>面向.NET Framework 4 或.NET Framework 4.5 的 Office 项目设计更改
  从 [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]开始，Visual Studio 引入了对面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 项目设计的一些更改。 如果你熟悉以前的 Visual Studio 版本中的 Office 项目，那么在开发面向 .NET Framework 4.0 或更高版本的 Office 项目之前，应了解这些更改。 默认情况下，使用 Visual Studio 2013 或更高版本创建的所有项目都面向 .NET Framework 4.0 或更高版本。

 以下各节描述这些 Office 项目设计更改。

## <a name="understand-the-interface-based-design-of-the-visual-studio-2010-tools-for-office-runtime"></a>了解 Visual Studio 2010 Tools for Office 运行时基于接口的设计
 开发面向的 Office 项目时[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本，会用到 Visual Studio 2010 Tools for Office 运行时类型的大多数都是接口。 这是对以前版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]的一个重要更改，在以前的版本中这些类型是类。 例如，如果面向的是 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则 <xref:Microsoft.Office.Tools.Excel.Worksheet> 和 <xref:Microsoft.Office.Tools.Word.Document> 类型是接口而不是类。 有关详细信息，请参阅[Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

 对于可以在以前版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 中直接实例化的任何类型，现在可使用 `Globals.Factory` 对象的方法来获取这些类型的实例。 例如，若要获取实现 <xref:Microsoft.Office.Tools.Excel.SmartTag> 接口的对象，请使用 `Globals.Factory.CreateSmartTag` 方法。 有关详细信息，请参阅下列主题：

- [更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

- [更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Office 项目中的功能区自定义](/visualstudio/vsto/update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5)

- [更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Outlook 项目中的窗体区域](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

### <a name="new-base-classes-in-office-projects"></a>Office 项目中的新基类
 新的 Visual Studio 2010 Tools for Office 运行时基于接口的设计会影响 Office 项目中生成的类，如`ThisDocument`， `ThisWorkbook`，和`ThisAddIn`。 在面向.NET Framework 3.5 和以前版本的 Framework 的 Office 项目中，这些生成的类派生自 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 中的类，如 `Microsoft.Office.Tools.Word.Document`、`Microsoft.Office.Tools.Excel.Worksheet` 和 `Microsoft.Office.Tools.AddIn`。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 类现在为接口。 因此，Office 项目中生成的类不再从这些类派生其实现。 相反，生成的类派生自诸如 <xref:Microsoft.Office.Tools.Word.DocumentBase>、 <xref:Microsoft.Office.Tools.Excel.WorksheetBase>和 <xref:Microsoft.Office.Tools.AddInBase>等新基类。 有关详细信息，请参阅[程序 VSTO 外接](../vsto/programming-vsto-add-ins.md)并[程序文档级自定义项](../vsto/programming-document-level-customizations.md)。

 基类不属于 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 可再发行组件。 相反，基类在 Visual Studio 附带的实用工具程序集中进行定义。 这些程序集在生成 Office 项目时复制到输出文件夹，并且必须随解决方案一起部署。 有关实用工具程序集的详细信息，请参阅[Visual Studio Tools for Office runtime 中的程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)。

## <a name="breaking-changes-in-office-projects-that-are-retargeted-to-the-net-framework-4"></a>重定向到.NET Framework 4 的 Office 项目中的重大更改
 下表列出了在重定向到 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 项目中可能会遇到的主要重大更改。 有关更多详细信息，请参阅[迁移 Office 解决方案为.NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)。

|重大更改|结果|
|---------------------|-----------------|
|Office 项目中不再使用或支持 <xref:System.Security.SecurityTransparentAttribute> 。|必须从更新自 Visual Studio 2008 的 Office 项目的 AssemblyInfo 代码文件中删除此属性。 有关详细信息，请参阅[所需更改即可运行迁移到.NET Framework 4 或.NET Framework 4.5 的 Office 项目](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。|
|**ExcelLocale1033Attribute**不再使用或在 Excel 项目中受支持。|您必须删除此属性从*AssemblyInfo* Excel 项目中的代码文件。 有关详细信息，请参阅[迁移到.NET Framework 4 或.NET Framework 4.5 的更新 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。|
|**“功能区（可视化设计器）”** 项目项的编程模型已更改。|必须修改项目中任何功能区项的代码隐藏文件。 此外必须修改的实例化在运行时的功能区控件、 处理功能区事件或以编程方式设置功能区组件位置的任何代码。 有关详细信息，请参阅[迁移到.NET Framework 4 或.NET Framework 4.5 的 Office 项目中的更新功能区自定义](/visualstudio/vsto/update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5)。|
|Outlook 窗体区域的编程模型已更改。|在你的项目和任何代码都实例化某些窗体区域类在运行时，必须修改任何窗体区域的代码隐藏文件。 有关详细信息，请参阅[更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Outlook 项目中的窗体区域](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。|
|Excel 和 Word 项目中的智能标记的编程模型已更改。 在 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] 和 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]中弃用了智能标记。|如果你的解决方案使用智能标记，则生成项目时将发生错误。 由于 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] 和 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]中已弃用智能标记，因此，在 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 或更高版本中，必须先删除这些标记才能测试和调试解决方案。|
|`GetVstoObject` 和 `HasVstoObject` 方法的语法已更改|从主互操作程序集 (PIA) 在本机对象上访问这些方法时，必须将 `Globals.Factory` 传递给这些方法，或者可以在由项目中的 `Globals.Factory` 属性返回的对象上访问这些方法。 有关详细信息，请参阅[迁移到.NET Framework 4 或.NET Framework 4.5 的更新 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。|
|Word 内容控件的事件与新委托相关联。|必须将处理 Word 内容控件的事件的任何代码修改为指定新委托。 有关详细信息，请参阅[迁移到.NET Framework 4 或.NET Framework 4.5 的更新 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。|
|`OLEObject` 和 `OLEControl` 类已重命名。|必须将使用这些类的实例的任何代码改为使用 <xref:Microsoft.Office.Tools.Excel.ControlSite> 或 <xref:Microsoft.Office.Tools.Word.ControlSite> 对象。 有关详细信息，请参阅[迁移到.NET Framework 4 或.NET Framework 4.5 的更新 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。|
|主机项类，如`ThisWorkbook`， `Sheet` *n*， `ThisDocument`，并且`ThisAddIn`，不再提供`Dispose`可以重写的方法。|必须将 `Dispose` 方法替代中的任何代码移动到主机项（如 `ThisAddIn_Shutdown`）中的 `Shutdown` 事件处理程序，并从主机项类中删除 `Dispose` 方法替代。|

## <a name="see-also"></a>请参阅
- [迁移到.NET Framework 4 或更高版本的 Office 解决方案](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [什么是中的 Office 开发的新增功能](https://msdn.microsoft.com/library/bf054af2-c896-4723-aa15-6381145b14bb)
- [Visual Studio Tools for Office runtime 概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
