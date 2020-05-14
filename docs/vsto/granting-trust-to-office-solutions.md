---
title: 授予 Office 解决方案的信任
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
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301655"
---
# <a name="grant-trust-to-office-solutions"></a>授予 Office 解决方案的信任
  向 Office 解决方案授予信任意味着修改每个目标计算机的安全策略，以信任解决方案程序集、应用程序清单、部署清单和文档。 您或最终用户都可以信任 Office 解决方案。

 您可以通过签署应用程序和部署清单来授予 Office 解决方案完全信任。

 最终用户可以通过在[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信任提示中做出信任决策来授予 Office 解决方案的信任。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trust-the-solution-by-signing-the-application-and-deployment-manifests"></a><a name="Signing"></a>通过签署应用程序和部署清单来信任解决方案
 Office 解决方案的所有应用程序和部署清单都必须使用标识发布者的证书进行签名。 证书为做出信任决策提供了基础。

 临时证书是为您创建的，并在生成时授予信任，因此在调试解决方案时将运行解决方案。 如果发布使用临时证书签名的解决方案，将提示最终用户做出信任决策。

 如果使用已知且受信任的证书对解决方案进行签名，则解决方案将自动安装，而不会提示最终用户做出信任决策。 有关如何获取签名证书的详细信息，请参阅[ClickOnce 和身份验证](../deployment/clickonce-and-authenticode.md)。 获取证书后，必须通过将其添加到"受信任的发布者"列表来显式信任该证书。 有关详细信息，请参阅[如何：将受信任的发布者添加到用于 ClickOnce 应用程序的客户端计算机](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)。

 如果开发人员使用临时证书对解决方案进行签名，则管理员可以使用 Microsoft .NET 框架工具之一的清单生成和编辑工具 *（mage.exe）* 使用已知且受信任的证书重新对自定义进行签名。 有关签名解决方案的详细信息，请参阅[如何：对 Office 解决方案进行签名](../vsto/how-to-sign-office-solutions.md)以及如何[：对应用程序和部署清单进行签名](../ide/how-to-sign-application-and-deployment-manifests.md)。

## <a name="trust-the-solution-by-using-the-clickonce-trust-prompt"></a><a name="TrustPrompt"></a>使用 ClickOnce 信任提示信任解决方案
 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]如果没有信任解决方案证书的组织范围策略，则提示最终用户做出信任决策。 如果最终用户向解决方案授予信任，则创建包含列表条目，其中包含一个 URL 和一个公钥来存储此信任决策。 稍后运行受信任的自定义项时，不会再次提示最终用户。

 管理员可以禁用[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]信任提示，或要求仅对使用身份验证证书签名的解决方案执行提示。 有关如何更改"我的计算机"、"本地内联网"、"互联网"、"受信任的网站"和不受信任的站点区域的这些设置的详细信息，请参阅[：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。

## <a name="see-also"></a>另请参阅

- [安全办公室解决方案](../vsto/securing-office-solutions.md)
- [授予文档信任](../vsto/granting-trust-to-documents.md)
- [排除 Office 解决方案安全性](../vsto/troubleshooting-office-solution-security.md)
- [Office 解决方案的特定安全注意事项](../vsto/specific-security-considerations-for-office-solutions.md)