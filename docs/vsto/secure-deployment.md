---
title: 安全部署
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying applications [Office development in Visual Studio], security
- Office development in Visual Studio, security
- Office applications [Office development in Visual Studio], security
- ClickOnce deployment [Office development in Visual Studio], security
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1000504ad83706bd028af4bd668da7483e478b7a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978363"
---
# <a name="secure-deployment"></a>安全部署
  创建 Office 解决方案时，是自动更新你的开发计算机以允许你运行的项目中的代码。 但是，在部署你的解决方案时，必须提供要签名的证书，该解决方案或使用基于信任决定的证据[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信任提示密钥。 有关详细信息，请参阅[向 Office 解决方案授予信任](../vsto/granting-trust-to-office-solutions.md)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 对于文档级自定义项，如果将文档部署到网络位置，您还必须添加该文档的位置到信任中心中的 Office 应用程序的受信任位置列表。 有关如何设置最终用户计算机上的文档权限的详细信息，请参阅[向文档授予信任](../vsto/granting-trust-to-documents.md)。

## <a name="prevent-office-solutions-from-running-code"></a>阻止 Office 解决方案运行代码
 管理员可以使用注册表来阻止所有 Office 解决方案的计算机上运行。 具有托管代码扩展的 Office 解决方案打开时，Visual Studio Tools for Office 运行时检查的条目是否具有名称`Disabled`存在的计算机上的以下注册表项之一：

- **HKEY_CURRENT_USER\Software\Microsoft\VSTO**

- **HKEY_LOCAL_MACHINE\Software\Microsoft\VSTO**

  若要防止 Office 解决方案运行代码，创建`Disabled`条目下一个或两个这些注册表项，并指定以下数据类型和值的一个`Disabled`:

- REG_SZ 或 REG_EXPAND_SZ 设置为"0"（零） 以外的其他任何字符串。

- 设置为 0 （零） 以外的其他任何值的 REG_DWORD。

  若要启用 Office 解决方案运行代码，请设置这两个`Disabled`条目为 0 （零），或删除的注册表项。

## <a name="see-also"></a>请参阅
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [准备计算机以运行或托管 Office 解决方案](https://msdn.microsoft.com/be1b173f-7261-4d74-aa4e-94ccd43db8d8)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
