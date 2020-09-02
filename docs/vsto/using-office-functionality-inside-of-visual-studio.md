---
title: 在 Visual Studio 中使用 Office 功能
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62982332"
---
# <a name="use-office-functionality-inside-of-visual-studio"></a>在 Visual Studio 中使用 Office 功能
  当你创建文档级项目时，文档和关联的应用程序将托管在 Visual Studio 中，以便你可以直接设计和使用该文档。 在 Visual Studio 中打开 Microsoft Office 应用程序时，该应用程序通常按预期方式工作。 但是，某些应用程序的功能不同或无法访问。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="document-protection"></a>文档保护
 Microsoft Office Word 和 Microsoft Office Excel 提供了可在项目中使用的文档保护功能。 但是，如果文档在 Visual Studio 中打开时启用了文档保护，则可能会阻止你进行某些设计更改。 有关详细信息，请参阅文档 [级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)。

## <a name="information-rights-management"></a>信息权限管理
 Microsoft Office Word 和 Microsoft Office Excel 中提供了 Rights Management (IRM) 的信息。 IRM 可帮助防止未经授权的人员查看或更改敏感信息。 但是，IRM 还会阻止您的代码运行。 有关详细信息，请参阅 [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)。

## <a name="password-protection"></a>密码保护
 可以设置 Microsoft Office Word 文档和 Microsoft Office Excel 工作簿，以便不知道密码的人可以打开它们。 密码保护在 Word 和 Excel 中的处理方式不同，并且可能会影响你的开发过程。 有关详细信息，请参阅 [Office 文档中的密码保护](../vsto/password-protection-on-office-documents.md)。

## <a name="see-also"></a>另请参阅
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [信息权限管理和托管代码扩展概述](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)
- [如何：打开 Office 解决方案但不运行代码](../vsto/how-to-open-office-solutions-without-running-code.md)
