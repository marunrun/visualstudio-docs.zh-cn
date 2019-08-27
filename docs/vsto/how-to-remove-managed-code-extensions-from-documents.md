---
title: 如何：删除文档中的托管的代码扩展
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
ms.openlocfilehash: 438658af3f182ea732d0fefef0f5a5d6ecbefa03
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961587"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>如何：删除文档中的托管的代码扩展
  从文档或工作簿的 Microsoft Office Word 或 Microsoft Office Excel 文档级自定义的一部分，可以以编程方式删除自定义程序集。 然后，用户可以打开的文档并查看内容，但不是会向文档添加任何自定义用户界面 (UI)，而你的代码不会运行。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 可以使用其中一个来删除自定义程序集`RemoveCustomization`提供的方法[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 使用哪种方法取决于是否想要删除在运行时自定义项 （即通过 Word 时自定义项中运行代码文档或 Excel 工作簿处于打开状态），或如果你想要从已关闭的文档或文档中删除自定义项，i没有安装 Microsoft Office 安装的服务器上的 s。

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[我如何：附加或分离的 VSTO 程序集从 Word 文档？](http://go.microsoft.com/fwlink/?LinkId=136782).

## <a name="to-remove-the-customization-assembly-at-runtime"></a>若要删除在运行时自定义程序集

1. 在自定义代码中，调用<xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A>的方法 （如 Word) 或<xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A>（针对 Excel) 的方法。 只有在不再需要自定义项后，应调用此方法。

     在代码中调用此方法的位置取决于如何使用自定义项。 例如，如果客户使用你的自定义功能，直到他们就可以将文档发送给其他客户端只需对文档本身 （不自定义），则可以提供一些 UI，以调用`RemoveCustomization`客户时单击它。 或者，如果你的自定义填充具有数据的文档时首次打开，但自定义项不提供直接由客户访问的任何其他功能，则可以调用 RemoveCustomization 尽快在自定义项完成初始化该文档。

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>若要从已关闭的文档或服务器上的文档中删除自定义程序集

1. 在项目中，不需要 Microsoft Office，如控制台应用程序或 Windows 窗体项目，添加对的引用*Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll*程序集。

2. 添加以下**导入**或**使用**到你的代码文件顶部的语句。

     [!code-csharp[Trin_VstcoreDeployment#1](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#1)]
     [!code-vb[Trin_VstcoreDeployment#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#1)]

3. 调用静态<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A>方法的<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类，并指定该参数的解决方案文档路径。

     下面的代码示例假定，您要从名为的文档中删除自定义*WordDocument1.docx*这也是桌面。

     [!code-csharp[Trin_VstcoreDeployment#2](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#2)]
     [!code-vb[Trin_VstcoreDeployment#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#2)]

4. 生成项目并想要删除自定义项在计算机上运行应用程序。 计算机必须具有 Visual Studio 2010 Tools for Office 运行时安装。

## <a name="see-also"></a>请参阅
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
