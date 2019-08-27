---
title: 在 Visual Studio 内使用 Office 功能
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], document protection
- Office applications [Office development in Visual Studio]
- Office functionality inside Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c47ed9639a33ecdea3451c63b729d959f6855e5d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982332"
---
# <a name="use-office-functionality-inside-of-visual-studio"></a>在 Visual Studio 内使用 Office 功能
  当创建文档级项目时，文档和关联的应用程序托管在 Visual Studio 中以便您可以设计和直接使用该文档。 Microsoft Office 应用程序在 Visual Studio 中打开后，它通常按预期方式工作。 但是，某些应用程序是功能的不同的或不可访问。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="document-protection"></a>文档保护
 Microsoft Office Word 和 Microsoft Office Excel 提供文档可以在项目中使用的保护功能。 但是，如果在 Visual Studio 中打开文档时启用文档保护，则它可以阻止你进行某些设计更改。 有关详细信息，请参阅[文档在文档级解决方案中的保护](../vsto/document-protection-in-document-level-solutions.md)。

## <a name="information-rights-management"></a>信息权限管理
 信息权限管理 (IRM) 现已推出 Microsoft Office Word 和 Microsoft Office Excel。 IRM 可帮助您防止未经授权的人员查看或更改的敏感信息。 但是，IRM 还可以使您的代码，从正在运行。 有关详细信息，请参阅[信息权限管理和托管的代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)。

## <a name="password-protection"></a>密码保护
 可以设置 Microsoft Office Word 文档和 Microsoft Office Excel 工作簿，以便它们不能打开的人不知道密码。 密码保护在 Word 和 Excel 中的处理方式不同，可能会影响您的开发过程。 有关详细信息，请参阅[Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)。

## <a name="see-also"></a>请参阅
- [在文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [信息权限管理和托管的代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)
- [如何：打开 Office 解决方案但不运行代码](../vsto/how-to-open-office-solutions-without-running-code.md)
