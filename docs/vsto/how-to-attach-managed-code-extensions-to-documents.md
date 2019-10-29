---
title: 如何：将托管代码扩展附加到文档
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
ms.openlocfilehash: 8fb212f9c5441d697cfa92feee7dc18fab9270d2
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985977"
---
# <a name="how-to-attach-managed-code-extensions-to-documents"></a>如何：将托管代码扩展附加到文档
  您可以将自定义程序集附加到现有 Microsoft Office Word 文档或 Microsoft Office Excel 工作簿。 文档或工作簿的格式可以为 Microsoft Office 项目和 Visual Studio 中的开发工具所支持的任何文件格式。 有关详细信息，请参阅[文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 若要将自定义附加到 Word 或 Excel 文档中，请使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> 方法。 由于 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类设计为在未安装 Microsoft Office 的计算机上运行，因此你可以在与 Microsoft Office 开发（如控制台或 Windows 窗体应用程序）不直接相关的解决方案中使用此方法。

> [!NOTE]
> 如果代码需要指定文档没有的控件，则自定义项将无法加载。

### <a name="to-attach-managed-code-extensions-to-a-document"></a>将托管代码扩展附加到文档

1. 在不需要 Microsoft Office 的项目（例如，控制台应用程序或 Windows 窗体项目）中，添加对*VisualStudio*的引用并*VisualStudio*程序集的集合。

2. 将以下**导入**或**using**语句添加到代码文件的顶部。

     [!code-csharp[Trin_VstcoreDeployment#4](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#4)]
     [!code-vb[Trin_VstcoreDeployment#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#4)]

3. 调用静态 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> 方法。

     下面的代码示例使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> 重载。 此重载采用文档的完整路径和 <xref:System.Uri> 来指定要附加到文档的自定义项的部署清单的位置。 此示例假定在桌面上有名为**worddocument1.docx**的 Word 文档，且部署清单位于名为**Publish**的文件夹中，该文件夹也在桌面上。

     [!code-csharp[Trin_VstcoreDeployment#3](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#3)]
     [!code-vb[Trin_VstcoreDeployment#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#3)]

4. 生成项目，并在要附加自定义项的计算机上运行应用程序。 计算机必须安装 Visual Studio 2010 Tools for Office Runtime。

## <a name="see-also"></a>请参阅
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [如何：从文档中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
