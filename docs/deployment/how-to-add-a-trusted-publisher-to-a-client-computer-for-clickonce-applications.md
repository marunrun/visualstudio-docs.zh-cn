---
title: 向 ClickOnce 应用程序的客户端计算机添加受信任的发布者
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- trusted application deployment, Trusted Publishers
ms.assetid: 35fe324c-45a1-4509-b7be-5c18b4b1b4ab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a874415d35d08fe00989b034c0bd828dbb6d567
ms.sourcegitcommit: 8589d85cc10710ef87e6363a2effa5ee5610d46a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72806892"
---
# <a name="how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications"></a>如何：为 ClickOnce 应用程序向客户端计算机添加一个受信任的发行者
借助受信任的应用程序部署，可以配置客户端计算机，以便 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序在不提示用户的情况下以更高信任级别运行。 下面的过程演示如何使用命令行工具 CertMgr.exe 将发布者的证书添加到客户端计算机上的“受信任的发布者”存储。

 根据颁发证书的证书颁发机构 (CA) 是否为客户端受信任的根的一部分，可以使用的命令略有不同。 如果 Windows 客户端计算机是域的一部分，则它会在一个列表中包含被视为受信任的根的 CA。 此列表通常由系统管理员进行配置。 如果证书由这些受信任的根中的一个颁发，或是由链接到这些受信任的根之一的 CA 颁发，则可以将证书添加到客户端“受信任的根”存储。 另一方面，如果证书不是由这些受信任的根中的一个颁发，则必须将同时证书添加到客户端“受信任的根”存储和“受信任的发布者”存储。

> [!NOTE]
> 在计划将需要提升的权限的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序部署到的每个客户端计算机上，都必须采用这种方式添加证书。 可手动或通过部署到客户端的应用程序添加证书。 只需将这些计算机配置一次，在此之后，便可以部署使用相同证书签名的任何数量的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。

 还可以使用 <xref:System.Security.Cryptography.X509Certificates.X509Store> 类以编程方式将证书添加到存储。

 有关受信任的应用程序部署的概述，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

### <a name="to-add-a-certificate-to-the-trusted-publishers-store-under-the-trusted-root"></a>将证书添加到受信任的根下的“受信任的发布者”存储

1. 从 CA 获取数字证书。

2. 将证书导出为 Base64 X.509 (.cer) 格式。 有关证书格式的详细信息，请参阅[导出证书](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730988(v=ws.10))。

3. 从客户端计算机上的命令提示符处，运行以下命令：

     **certmgr.exe -add certificate.cer -c -s -r localMachine TrustedPublisher**

### <a name="to-add-a-certificate-to-the-trusted-publishers-store-under-a-different-root"></a>将证书添加到其他根下的“受信任的发布者”存储

1. 从 CA 获取数字证书。

2. 将证书导出为 Base64 X.509 (.cer) 格式。 有关证书格式的详细信息，请参阅 [导出证书](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730988(v=ws.10))。

3. 从客户端计算机上的命令提示符处，运行以下命令：

     **certmgr.exe -add good.cer -c -s -r localMachine Root**

     **certmgr.exe -add good.cer -c -s -r localMachine TrustedPublisher**

## <a name="see-also"></a>请参阅
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限对 ClickOnce 应用程序进行调试](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [如何：为 ClickOnce 应用程序向客户端计算机添加一个受信任的发行者](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [如何：为应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
- [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)