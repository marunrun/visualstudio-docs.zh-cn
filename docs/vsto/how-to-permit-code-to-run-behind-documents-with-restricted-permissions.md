---
title: 允许代码在具有受限权限的文档的后台运行
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 15cfb7ebf2f4f71e892820206f0dd1d006639992
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547506"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>如何：允许代码在具有受限权限的文档的后台运行
  您可以使用 Microsoft Office 的 Rights Management (IRM) 功能的信息来限制对文档或工作簿的权限。 默认情况下，不允许运行受限 Microsoft Office Word 文档或 Microsoft Office Excel 工作簿的隐藏代码。 你可以更改默认值，以便托管代码扩展可以访问对象模型，你的解决方案将工作。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 您必须是文档或工作簿的作者，或者具有 "完全控制" 权限才能更改权限设置。

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>允许代码在具有受限权限的文档的后台运行

1. 在 Word 或 Excel 中打开文档或工作簿。

2. 单击 " **文件** " 选项卡，指向 " **准备**"，指向 " **限制权限**"，然后单击 " **受限访问**"。

   > [!NOTE]
   > 首次使用时，系统将提示您安装 Windows Rights Management 客户端。 安装客户端后，你可能需要重复这些步骤。

3. 在 " **权限** " 对话框中，选择 " **限制对此文档的权限**"，然后单击 " **更多选项**"。

4. 在 " **用户的其他权限**" 下，选择 " **以编程方式访问内容**"。

   Word 或 Excel 将允许以编程方式访问对象模型。

## <a name="see-also"></a>另请参阅
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
