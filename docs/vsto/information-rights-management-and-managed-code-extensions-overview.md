---
title: '& 托管代码扩展的信息权限管理'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- IRM [Office development in Visual Studio]
- documents [Office development in Visual Studio], restricted permissions
- rights management [Office development in Visual Studio]
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 753f3d2da201c67cd86c697eccf7580596a40d6e
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68872066"
---
# <a name="information-rights-management-and-managed-code-extensions-overview"></a>信息权限管理和托管代码扩展概述
  Microsoft Office Word 和 Microsoft Office Excel 提供信息 Rights Management (IRM), 这是一项功能, 可帮助防止未经授权的人员查看或更改敏感信息。 有关信息 Rights Management 工作原理的详细信息, 请参阅特定 Office 应用程序中的帮助。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="run-code-behind-documents-with-restricted-permissions"></a>用受限权限运行代码隐藏文档
 如果你的解决方案包含使用 IRM 的文档或工作簿, 则默认情况下, Word 和 Excel 不允许运行任何代码。 如果你是文档的作者或具有 "完全控制" 权限, 则可以更改默认设置, 以便解决方案正常工作。 有关详细信息，请参阅[如何：允许代码在具有受限权限](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)的文档的后台运行。

 IRM 禁止使用<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>来检索或操作在文档中缓存的数据。

## <a name="end-users-to-restrict-permissions-to-documents-that-use-managed-code-extensions"></a>最终用户限制使用托管代码扩展的文档的权限
 对解决方案中的文档或工作簿具有完全控制访问权限的任何人都可以使用 IRM 来限制权限。 例如, 如果会计部门的最终用户使用的解决方案自动使用数据库中的数据填充工作表, 则该用户可能想要只允许对其部门的人员进行更改, 并对他人进行读访问。 当用户添加受限权限时, 默认情况下, 工作表后面的代码将无法运行, 并且不会用数据填充工作表。

 若要解决此问题, 对文档或工作簿具有完全控制访问权限的用户必须更改默认权限设置, 以允许以编程方式访问对象模型。 有关详细信息，请参阅[如何：允许代码在具有受限权限](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)的文档的后台运行。

## <a name="see-also"></a>请参阅
- [文档级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)
- [Office 文档上的密码保护](../vsto/password-protection-on-office-documents.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
