---
title: 允许代码文档的后面使用受限权限运行
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- IRM [Office development in Visual Studio]
- code [Office development in Visual Studio], running behind restricted documents
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 32e42954958fda71d54c3c0ac2685928644e7461
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402250"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>如何：允许代码以使用受限权限的文档的后台运行
  Microsoft Office 信息权限管理 (IRM) 功能可用于限制对文档或工作簿的权限。 默认情况下，受限制的 Microsoft Office Word 文档或 Microsoft Office Excel 工作簿后的代码不被允许运行。 可以更改默认值，使托管的代码扩展可以访问的对象模型，该解决方案将适用。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 您必须文档或工作簿作者或具有完全控制权限，以便能够更改权限设置。

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>若要允许代码以使用受限权限的文档的后台运行

1. 在 Word 或 Excel 中打开文档或工作簿。

2. 单击**文件**选项卡上，依次指向**准备**，指向**限制权限**，然后单击**受限访问权限**。

   > [!NOTE]
   > 首次使用时，系统会提示安装的 Windows 权限管理客户端。 安装客户端后，你可能需要重复这些步骤。

3. 在中**权限**对话框中，选择**限制此文档的权限**，然后单击**更多选项**。

4. 下**用户的其他权限**，选择**以编程方式访问内容**。

   Word 或 Excel 将允许以编程方式访问的对象模型。

## <a name="see-also"></a>请参阅
- [信息权限管理和托管的代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [在文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
