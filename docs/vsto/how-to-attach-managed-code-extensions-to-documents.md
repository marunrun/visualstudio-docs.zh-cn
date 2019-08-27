---
title: 如何：将托管的代码扩展附加到文档
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], attaching
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f56d51817491726e6011e965bfd6d68630bb0dbf
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441805"
---
# <a name="how-to-attach-managed-code-extensions-to-documents"></a>如何：将托管的代码扩展附加到文档
  可以将自定义程序集附加到现有 Microsoft Office Word 文档或 Microsoft Office Excel 工作簿。 文档或工作簿可以是支持的 Microsoft Office 项目和 Visual Studio 中的开发工具的任何文件格式。 有关详细信息，请参阅[的文档级自定义体系结构](../vsto/architecture-of-document-level-customizations.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 若要将自定义项附加到 Word 或 Excel 文档，请使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A>方法的<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类。 因为<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>类专为没有安装 Microsoft Office 的计算机上运行，则可以不直接相关 （如控制台或 Windows 窗体应用程序） 的 Microsoft Office 开发的解决方案中使用此方法。

> [!NOTE]
> 自定义项将无法加载如果代码需要指定的文档中不存在的控件。

 ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：附加或分离的 VSTO 程序集从 Word 文档？](http://go.microsoft.com/fwlink/?LinkId=136782).

### <a name="to-attach-managed-code-extensions-to-a-document"></a>若要将托管的代码扩展附加到文档

1. 在项目中，不需要 Microsoft Office，如控制台应用程序或 Windows 窗体项目，添加对的引用*Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll*和*Microsoft.VisualStudio.Tools.Applications.Runtime.dll*程序集。

2. 添加以下**导入**或**使用**到你的代码文件顶部的语句。

     [!code-csharp[Trin_VstcoreDeployment#4](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#4)]
     [!code-vb[Trin_VstcoreDeployment#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#4)]

3. 调用静态<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A>方法。

     下面的代码示例使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A>重载。 此重载需要使用文档的完整路径和一个<xref:System.Uri>，它指定你想要附加到文档的自定义项的部署清单的位置。 此示例假定的 Word 文档名为**WordDocument1.docx**是在桌面上，和部署清单位于名为的文件夹中的**发布**这也是在桌面上。

     [!code-csharp[Trin_VstcoreDeployment#3](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#3)]
     [!code-vb[Trin_VstcoreDeployment#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#3)]

4. 生成项目并想要附加自定义项在计算机上运行应用程序。 计算机必须具有 Visual Studio 2010 Tools for Office 运行时安装。

## <a name="see-also"></a>请参阅
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [如何：删除文档中的托管的代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [在 Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
