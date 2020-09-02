---
title: 保护部署
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62978363"
---
# <a name="secure-deployment"></a>保护部署
  当你创建 Office 解决方案时，你的开发计算机会自动更新，以允许你的项目中的代码运行。 但是，在部署解决方案时，必须通过使用证书或使用信任提示密钥对解决方案进行签名，来提供信任决策所依据的证据 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 有关详细信息，请参阅 [向 Office 解决方案授予信任](../vsto/granting-trust-to-office-solutions.md)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 对于文档级自定义项，如果将文档部署到网络位置，还必须将文档的位置添加到 Office 应用程序的 "信任中心" 中的受信任位置列表中。 有关如何在最终用户计算机上设置文档权限的详细信息，请参阅 [向文档授予信任](../vsto/granting-trust-to-documents.md)。

## <a name="prevent-office-solutions-from-running-code"></a>阻止 Office 解决方案运行代码
 管理员可以使用注册表来阻止所有 Office 解决方案在计算机上运行。 当打开具有托管代码扩展的 Office 解决方案时，Visual Studio Tools for Office 运行时将检查 `Disabled` 计算机上是否存在以下注册表项之一的具有该名称的条目：

- **HKEY_CURRENT_USER \Software\Microsoft\VSTO**

- **HKEY_LOCAL_MACHINE \Software\Microsoft\VSTO**

  若要阻止 Office 解决方案运行代码，请 `Disabled` 在其中一个或两个注册表项下创建一个条目，并为以下数据类型和值指定以下数据类型之一 `Disabled` ：

- 设置为除 "0" (零) 以外的任何字符串的 REG_SZ 或 REG_EXPAND_SZ。

- 设置为 0 (零) 的任何值的 REG_DWORD。

  若要使 Office 解决方案能够运行代码，请将两个项都设置 `Disabled` 为 0 (零) ，或删除注册表项。

## <a name="see-also"></a>另请参阅
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [准备计算机以运行或托管 Office 解决方案](https://msdn.microsoft.com/be1b173f-7261-4d74-aa4e-94ccd43db8d8)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
