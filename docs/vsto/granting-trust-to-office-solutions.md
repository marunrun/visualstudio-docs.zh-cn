---
title: 向 Office 解决方案授予信任
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
ms.openlocfilehash: cf7a68d5d3567305e4f70049d76a1c260ddecf25
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826929"
---
# <a name="grant-trust-to-office-solutions"></a>向 Office 解决方案授予信任
  为 Office 解决方案意味着修改每台目标计算机的安全策略信任解决方案程序集、 应用程序清单、 部署清单和文档授予信任。 由你或最终用户，可以向 Office 解决方案授予信任。

 可以通过对应用程序和部署清单进行签名来授予完全信任权限的 Office 解决方案。

 最终用户可以向授予信任 Office 解决方案中的信任决策，从而[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信任提示。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="Signing"></a> 信任该解决方案通过对应用程序和部署清单进行签名
 所有应用程序和部署清单的 Office 解决方案必须使用标识的发布服务器的证书进行签名。 证书提供基础来做出信任决定。

 为你创建并在生成时授予信任，以便在调试时，将运行该解决方案的临时证书。 如果发布使用的临时证书签名的解决方案，将提示最终用户做出信任决策。

 如果你登录使用已知和受信任的证书解决方案，该解决方案将自动安装而不会提示最终用户做出信任决定。 有关如何获取用于签名的证书的详细信息，请参阅[ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)。 获取证书后，必须将其添加到受信任的发行者列表显式信任证书。 有关详细信息，请参阅[如何：ClickOnce 应用程序的客户端计算机添加受信任的发行者](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)。

 如果开发人员对该解决方案使用的临时证书进行签名，则管理员重新签名使用清单生成和编辑工具的已知和受信任的证书与自定义项 (*mage.exe*)，这是其中的项Microsoft.NET Framework 工具。 有关对解决方案进行签名的详细信息，请参阅[如何：对 Office 解决方案进行签名](../vsto/how-to-sign-office-solutions.md)和[如何：对应用程序和部署清单签名](../ide/how-to-sign-application-and-deployment-manifests.md)。

## <a name="TrustPrompt"></a>信任该解决方案通过使用 ClickOnce 信任提示
 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 将提示最终用户做出信任决定是否信任该解决方案的证书没有组织范围的策略。 如果最终用户授予到解决方案的信任，创建包含的 URL 和一个公钥用于存储此信任决策包含列表条目。 受信任的自定义运行时更高版本，是不会再次提示最终用户。

 管理员可以禁用[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信任提示或要求仅对使用验证码证书进行签名的解决方案出现提示。 有关如何为 MyComputer、 LocalIntranet、 Internet、 TrustedSites 和 UntrustedSites 区域更改这些设置的详细信息，请参阅[如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。

## <a name="see-also"></a>请参阅

- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [向文档授予信任](../vsto/granting-trust-to-documents.md)
- [Office 解决方案安全性疑难解答](../vsto/troubleshooting-office-solution-security.md)
- [有关 Office 解决方案的特定安全注意事项](../vsto/specific-security-considerations-for-office-solutions.md)