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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89315234"
---
# <a name="grant-trust-to-office-solutions"></a>向 Office 解决方案授予信任
  向 Office 解决方案授予信任意味着修改每台目标计算机的安全策略，以信任解决方案程序集、应用程序清单、部署清单和文档。 你或最终用户可以向 Office 解决方案授予信任。

 可以通过对应用程序和部署清单进行签名来向 Office 解决方案授予完全信任。

 最终用户可以通过信任提示做出信任决定向 Office 解决方案授予信任 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trust-the-solution-by-signing-the-application-and-deployment-manifests"></a><a name="Signing"></a> 通过对应用程序和部署清单进行签名来信任解决方案
 Office 解决方案的所有应用程序和部署清单必须使用标识发布者的证书进行签名。 证书提供了做出信任决策的基础。

 系统会为你创建一个临时证书，并在生成时向其授予信任，以便在你对其进行调试时运行解决方案。 如果发布使用临时证书签名的解决方案，则会提示最终用户进行信任决定。

 如果使用已知的可信证书对解决方案进行签名，则会自动安装解决方案，而不会提示最终用户做出信任决定。 有关如何获取签名证书的详细信息，请参阅 [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)。 获取证书后，必须通过将证书添加到 "受信任的发布者" 列表来显式信任该证书。 有关详细信息，请参阅 [如何：为 ClickOnce 应用程序将受信任的发布者添加到客户端计算机](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)。

 如果开发人员使用临时证书对解决方案进行签名，则管理员可以通过使用清单生成和编辑工具 (*mage.exe*) （其中一个 Microsoft .NET 框架工具之一）对该自定义证书进行重新签名。 有关签名解决方案的详细信息，请参阅 [如何：对 Office 解决方案](../vsto/how-to-sign-office-solutions.md) 进行签名和 [如何：对应用程序和部署清单进行签名](../ide/how-to-sign-application-and-deployment-manifests.md)。

## <a name="trust-the-solution-by-using-the-clickonce-trust-prompt"></a><a name="TrustPrompt"></a>使用 ClickOnce 信任提示符信任解决方案
 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 如果没有组织范围内信任解决方案证书的策略，则会提示最终用户进行信任决定。 如果最终用户向解决方案授予信任，则会创建一个包含 URL 的包含列表条目，并创建一个公钥来存储此信任决定。 稍后运行受信任的自定义时，系统不会再次提示最终用户。

 管理员可以禁用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示，或要求仅对使用 Authenticode 证书签名的解决方案发出提示。 有关如何更改 MyComputer、LocalIntranet、Internet、TrustedSites 和 UntrustedSites 区域的这些设置的详细信息，请参阅 [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。

## <a name="see-also"></a>请参阅

- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [向文档授予信任](../vsto/granting-trust-to-documents.md)
- [Office 解决方案安全性疑难解答](../vsto/troubleshooting-office-solution-security.md)
- [Office 解决方案的特定安全注意事项](../vsto/specific-security-considerations-for-office-solutions.md)