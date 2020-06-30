---
title: 如何：打开 Office 解决方案但不运行代码
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], opening
- opening Office solutions
- bypassing assemblies
- solutions [Office development in Visual Studio], opening
- assemblies [Office development in Visual Studio], bypassing
- Office documents [Office development in Visual Studio, opening without running code
- documents [Office development in Visual Studio], opening without running code
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d84515c2c3159b61b96f77555b23eef0df0ae961
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543476"
---
# <a name="how-to-open-office-solutions-without-running-code"></a>如何：打开 Office 解决方案但不运行代码
  即使最终用户的 Office 应用程序中的安全设置设置为 "高"，使用托管代码扩展创建的 Microsoft Office 解决方案也会运行。 这是因为，.NET 程序集代码安全由 Microsoft .NET 框架管理，而不是 Microsoft Office。

 但是，有时您可能希望在不运行代码的情况下打开文档。 例如，在打开文档时运行的代码可能会改变内容，但你想要在代码更改文档前更新文档的外观。 或者，您可能想要将文档中的某些信息发送给他人，并且您不希望代码运行，可能会改变内容。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有多种方法可以打开包含托管代码扩展的文档或工作簿，无需运行程序集代码。

## <a name="to-bypass-the-assembly-by-using-the-shift-key"></a>使用 Shift 键跳过程序集

- 在按住**Shift**键的同时打开 "**文件**" 菜单中的文档和工作簿，以防止 Word 和 Excel 在文档打开时引发初始化事件。

    > [!NOTE]
    > 如果从 "**入门**任务窗格打开文档或工作簿，则按住**Shift**不会绕过代码。 而且，按住 SHIFT 不会阻止在打开文档后引发事件。

     如果要在不运行代码的情况下打开文档并更改文档，则此方法非常有用。

## <a name="to-bypass-an-assembly-by-renaming-or-removing-it"></a>通过重命名或删除程序集来跳过程序集

- 如果对程序集所在的计算机具有必要的权限，则可以重命名或删除程序集，使文档或工作簿无法找到该程序集。 这会导致每次打开 Office 文档时都会引发错误。

     如果该解决方案由多个用户使用，则此方法会阻止解决方案运行。 如果在代码或引用的服务器中发现问题并且你想要阻止所有用户执行该问题，则这会很有用。

## <a name="see-also"></a>另请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
