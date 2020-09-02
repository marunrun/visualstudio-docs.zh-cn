---
title: 向文档授予信任
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], trust
- inclusion lists [Office development in Visual Studio], about inclusion lists
- trust [Office development in Visual Studio], 2007 Office system
- granting trust [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9d245ddf00e4005b763bcd4437d3f8c18d05291e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72986045"
---
# <a name="grant-trust-to-documents"></a>向文档授予信任
  文档级项目与应用程序级项目具有相同的安全要求：使用证书对清单进行签名，或单击信任提示。 此外，文档或工作簿必须位于指定为受信任位置的目录中。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="trusted-locations"></a>受信任位置
 和 Office 2010 中的应用程序 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 具有信任中心，用户可以在其中配置安全和隐私设置，如受信任的位置。 对于 Office 解决方案，将本地计算机视为受信任的位置。 但是，由于具有较高风险，因此某些特定目录（如系统、用户和 Internet Explorer 的临时文件夹）也无法信任。

 有关信任中心的详细信息，请参阅 [Office 2010 中的安全性和策略和设置](/previous-versions/office/office-2010/cc178946(v=office.14))。 有关如何创建、管理、删除和配置受信任文件夹的详细信息，请参阅 [在 2007 Office 系统中配置受信任的位置和受信任的发布者设置](/previous-versions/office/office-2007-resource-kit/cc178948(v=office.12)) 和 [创建、删除或更改文件的受信任位置](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)。

## <a name="security-considerations-for-office-solutions"></a>Office 解决方案的安全注意事项
 在考虑将哪些文件夹添加到受信任的位置时，存在几个安全问题：

- 将本地文件夹视为较安全并且隐式受信任。 必须将远程位置（例如，文件共享）指定为受信任的位置。

- 当将某个目录添加到受信任的位置时，此操作将不仅向 Office 解决方案，还向 VBA 和 ActiveX 代码授予完全信任。 出于此原因，不应将根目录和 " *我的文档* " 文件夹指定为受信任。

- 尽管通过使用受信任的位置使文档本身受到信任，但仍需要其他权限来信任该自定义项。 你可以通过使用证书对清单进行签名，单击信任提示，或将 Office 解决方案安装到 *Program Files* 目录，为自定义授予完全信任。

- 可以在与程序集相同或不同的目录中存储文档级解决方案的文档或工作薄。 例如，文档可以位于 SharePoint 服务器，而程序集可以位于网络文件共享中。 有关详细信息，请参阅 [如何：使用 ClickOnce 将文档级 Office 解决方案发布到 SharePoint 服务器](https://msdn.microsoft.com/2408e809-fb78-42a1-9152-00afa1522e58)。

## <a name="see-also"></a>另请参阅
- [向 Office 解决方案授予信任](../vsto/granting-trust-to-office-solutions.md)
- [Office 解决方案安全性疑难解答](../vsto/troubleshooting-office-solution-security.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
