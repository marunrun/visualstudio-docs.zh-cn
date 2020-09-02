---
title: Office 文档上的密码保护
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- passwords [Office development in Visual Studio], document protections
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e3c9521389ce348a482f35ec95c9766edea49f5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62977895"
---
# <a name="password-protection-on-office-documents"></a>Office 文档上的密码保护
  可以设置 Microsoft Office Word 文档和 Microsoft Office Excel 工作簿的密码，使不知道密码的人无法打开这些工作簿。 此选项 **在 Open**时称为 Password。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 可以使用启用了 **打开的密码** 的现有文档和工作簿来创建文档级项目。 Visual Studio 中的行为不同于启用了 **密码打开** 的 Word 和 Excel 文档。

 有关 **打开时启用密码**的信息，请参阅 Word 或 Excel 中的帮助。

## <a name="behavior-of-excel-and-word"></a>Excel 和 Word 的行为
 每次在 Visual Studio 中打开启用了 **密码打开** 的 excel 工作簿时，excel 会提示输入密码。 当你生成解决方案时，系统将再次提示你输入密码，因为在生成过程中将打开该文档。

 首次在 Visual Studio 中打开启用了 **密码打开** 的 word 文档时，word 会提示输入密码。 成功输入密码后，将从文档中删除 **"打开密码** "，并且打开文档将不再需要密码。 如果希望解决方案中的文档在可以打开之前需要密码，则必须在最终生成之后和部署解决方案之前启用 **密码打开** 。

## <a name="see-also"></a>另请参阅
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [如何：允许代码在具有受限权限的文档的后台运行](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
