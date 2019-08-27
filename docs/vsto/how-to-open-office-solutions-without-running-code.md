---
title: 如何：打开 Office 解决方案但不运行代码
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 366416e4f18435bd01391657eb2fc4f65f8a4d62
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441771"
---
# <a name="how-to-open-office-solutions-without-running-code"></a>如何：打开 Office 解决方案但不运行代码
  创建具有托管的代码扩展的 Microsoft Office 解决方案运行，即使最终用户 Office 应用程序中的安全设置设为高。 这是因为.NET 程序集代码安全性由 Microsoft.NET Framework 中，不是由 Microsoft Office。

 但是，有些的时候您可能想要打开的文档，而无需运行代码。 例如，当文档打开时运行的代码可能会更改此内容，但你想要更新文档之前，会查找代码更改它的方式。 或者你可能想要在其中的某些信息将文档发送到人，并不希望运行并可能更改此内容的代码。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有几种方法来打开文档或工作簿包含托管的代码扩展，而无需运行的程序集代码。

## <a name="to-bypass-the-assembly-by-using-the-shift-key"></a>若要使用 Shift 键的跳过程序集

- 打开的文档和工作簿**文件**时按下菜单**Shift**密钥以防止 Word 和 Excel 打开文档时引发初始化事件。

    > [!NOTE]
    > 如果您打开的文档或从工作簿**Getting Started**任务窗格中，按住**Shift**未跳过代码。 此外，按下 shift 键不会阻止事件被引发后在文档处于打开状态。

     此方法很有用，如果你想要打开的文档运行和第一次更改文档的代码无需进行更改。

## <a name="to-bypass-an-assembly-by-renaming-or-removing-it"></a>若要重命名或移除它通过绕过程序集

- 如果该程序集所在的计算机上具有所需的权限，可以重命名或删除程序集，使文档或工作簿找不到它。 这会导致每次打开 Office 文档时引发错误。

     如果该解决方案由多个人员，此方法会运行所有这些解决方案。 如果在代码或引用的服务器中发现有问题，并且你想要停止执行其所有用户，这很有用。

## <a name="see-also"></a>请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [在 Office 解决方案中的应用程序和部署清单](../vsto/application-and-deployment-manifests-in-office-solutions.md)
