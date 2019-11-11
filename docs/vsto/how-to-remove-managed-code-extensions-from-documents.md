---
title: 如何：从文档中删除托管代码扩展
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0832f0e404331e68fe88dfc990c51ed699eca263
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985795"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>如何：从文档中删除托管代码扩展
  您可以以编程方式从文档或工作簿中移除自定义项程序集，该文档或工作簿是 Microsoft Office Word 或 Microsoft Office Excel 的文档级自定义项的一部分。 然后，用户可以打开文档并查看内容，但添加到文档中的任何自定义用户界面（UI）都不会显示，并且你的代码将不会运行。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 您可以通过使用 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]提供的 `RemoveCustomization` 方法之一删除自定义程序集。 使用哪种方法取决于您是否希望在运行时删除自定义项（即，在 Word 文档或 Excel 工作簿处于打开状态时运行自定义项中的代码）; 或者，如果要从已关闭的文档或我的文档中删除自定义项，s 在未安装 Microsoft Office 的服务器上。

## <a name="to-remove-the-customization-assembly-at-run-time"></a>在运行时删除自定义项程序集

1. 在自定义代码中，调用 <xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> 方法（适用于 Word）或 <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> 方法（对于 Excel）。 只有不再需要自定义项后，才应调用此方法。

     在代码中调用此方法的位置取决于自定义的使用方式。 例如，如果客户在准备好将文档发送给只需文档本身（而不是自定义）的其他客户端之前使用您的自定义功能，则可以提供一些在客户单击时调用 `RemoveCustomization` 的 UI。 或者，如果自定义在第一次打开时用数据填充文档，但自定义不提供客户直接访问的任何其他功能，则可在自定义项后立即调用 RemoveCustomization完成文档的初始化。

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>从关闭的文档或服务器上的文档中删除自定义程序集

1. 在不需要 Microsoft Office 的项目（例如，控制台应用程序或 Windows 窗体项目）中，添加对*VisualStudio*程序集的引用。

2. 将以下**Imports**或**using**语句添加到代码文件的顶部。

     [!code-csharp[Trin_VstcoreDeployment#1](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#1)]
     [!code-vb[Trin_VstcoreDeployment#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#1)]

3. 调用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类的静态 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> 方法，并指定参数的解决方案文档路径。

     下面的代码示例假设你要从桌面上的名为*worddocument1.docx*的文档中删除自定义项。

     [!code-csharp[Trin_VstcoreDeployment#2](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#2)]
     [!code-vb[Trin_VstcoreDeployment#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#2)]

4. 生成项目，并在要删除自定义项的计算机上运行该应用程序。 计算机必须安装 Visual Studio 2010 Tools for Office runtime。

## <a name="see-also"></a>请参阅
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
