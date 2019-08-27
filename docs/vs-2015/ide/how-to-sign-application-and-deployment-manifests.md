---
title: 如何：应用程序和部署清单签名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- manifests [Visual Studio]
- code signing [Visual Studio], Authenticode
- deployment manifests [Visual Studio]
- signing manifests [Visual Studio]
- application manifests [Visual Studio]
- ClickOnce deployment [Visual Studio], signing assemblies
- key files [Visual Studio]
- assemblies [Visual Studio], signing
ms.assetid: 64173505-8bfb-41cf-a0de-b9075173f3a2
caps.latest.revision: 61
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6dbcc6f74d39353ae38b7298851cb1bab5fb0fe0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685426"
---
# <a name="how-to-sign-application-and-deployment-manifests"></a>如何：对应用程序和部署清单进行签名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果想要通过使用 ClickOnce 部署发布应用程序，则必须通过验证码技术使用公钥/私钥对应用程序和部署清单进行签名。 可以使用 Windows 证书存储或密钥文件中的证书对清单进行签名。  
  
 有关 ClickOnce 部署的详细信息，请参阅 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)。  
  
 对于基于 .exe 的应用程序，对 ClickOnce 清单进行签名是可选的。 有关详细信息，请参阅本文档的“生成未签名的清单”部分。  
  
 有关创建密钥文件的详细信息，请参阅[如何：创建公钥/私钥对](https://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)。  
  
> [!NOTE]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 仅支持具有 .pfx 扩展名的个人信息交换 (PFX) 密钥文件。 但是，可通过单击项目属性“签名”页上的“从存储中选择”，从当前用户的 Windows 证书存储中选择其他类型的证书。  
  
### <a name="to-sign-application-and-deployment-manifests-using-a-certificate"></a>使用证书对应用程序和部署清单进行签名  
  
1. 转到项目属性窗口（在“解决方案资源管理器”中，右键单击项目节点并选择“属性”，或在“快速启动”窗口中键入 **project properties**，或在“解决方案资源管理器”窗口中按 ALT + ENTER）。 在“签名”选项卡上，选中“为 ClickOnce 清单签名”复选框。  
  
2. 单击“从存储中选择”按钮。  
  
     “选择证书”对话框将会出现并显示 Windows 证书存储中的内容。  
  
    > [!TIP]
    > 如果单击“单击此处查看证书属性”，将会出现“证书详细信息”对话框。 此对话框中包括有关证书的详细信息以及其他选项。 可以单击“证书”查看其他帮助信息。  
  
3. 选择要用于对清单进行签名的证书。  
  
4. 还可以在“时间戳服务器 URL”文本框中指定时间戳服务器的地址。 此服务器提供一个时间戳，用于指定对清单进行签名的时间。  
  
### <a name="to-sign-application-and-deployment-manifests-using-an-existing-key-file"></a>使用现有密钥文件对应用程序和部署清单进行签名  
  
1. 在“签名”页上，选中“为 ClickOnce 清单签名”复选框。  
  
2. 单击“从文件选择”按钮。  
  
     “选择文件”对话框随即出现。  
  
3. 在“选择文件”对话框中，浏览到要使用的密钥文件 (.pfx) 的位置，然后单击“打开”。  
  
    > [!NOTE]
    > 此选项仅支持具有 .pfx 扩展名的文件。 如果有其他格式的密钥文件或证书，请将其存储在 Windows 证书存储区中并选择前面的过程中描述的证书。 选定证书的用途应该包括代码签名。  
  
     “输入密码以打开文件”对话框随即出现。 （如果 .pfx 文件已经存储在 Windows 证书存储中或没有密码保护，则不会提示输入密码。）  
  
4. 输入访问密钥文件的密码，然后按 ENTER。  
  
### <a name="to-sign-application-and-deployment-manifests-using-a-test-certificate"></a>使用测试证书对应用程序和部署清单进行签名  
  
1. 在“签名”页上，选中“为 ClickOnce 清单签名”复选框。  
  
2. 若要创建用于测试的新证书，请单击“创建测试证书”按钮。  
  
3. 在“创建测试证书”对话框中，输入密码以帮助保护测试证书的安全。  
  
## <a name="generating-unsigned-manifests"></a>生成未签名的清单  
 对于基于 .exe 的应用程序，对 ClickOnce 清单进行签名是可选的。 下面的过程演示如何生成未签名的 ClickOnce 清单。  
  
> [!IMPORTANT]
> 未签名的清单可以简化应用程序的开发和测试过程。 但是，未签名的清单也会在生产环境中带来重大的安全风险。 仅当 ClickOnce 应用程序在与 Internet 或其他恶意代码源完全隔离的 Intranet 内的计算机上运行时，才应考虑使用未签名的清单。  
  
 默认情况下，ClickOnce 将自动生成签名的清单，除非专门从生成的哈希中排除一个或多个文件。 换而言之，如果哈希中包含所有文件，则发布应用程序会得到经过签名的清单，即使清除了“为 ClickOnce 清单签名”复选框也是如此。  
  
#### <a name="to-generate-unsigned-manifests-and-include-all-files-in-the-generated-hash"></a>生成未签名的清单并将所有文件包含在生成的哈希中  
  
1. 若要生成包含哈希中所有文件的未签名清单，必须首先将应用程序与签名的清单一起发布。 因此，应首先按照上述过程之一为 ClickOnce 清单签名，然后再发布应用程序。  
  
2. 在“签名”页上，清除“为 ClickOnce 清单签名”复选框。  
  
3. 重置发布版本，以使应用程序仅有一个版本可用。 默认情况下，每次发布应用程序时，Visual Studio 都会自动递增发布版本的版本号。 有关详细信息，请参阅[如何：设置 ClickOnce 发布版本](../deployment/how-to-set-the-clickonce-publish-version.md)。  
  
4. 发布应用程序。  
  
#### <a name="to-generate-unsigned-manifests-and-exclude-one-or-more-files-from-the-generated-hash"></a>生成未签名的清单并从生成的哈希中排除一个或多个文件  
  
1. 在“签名”页上，清除“为 ClickOnce 清单签名”复选框。  
  
2. 打开“应用程序文件”对话框，对于要从生成的哈希中排除的文件，请将“哈希”设置为“排除”。  
  
    > [!NOTE]
    > 从哈希中排除文件会将 ClickOnce 配置为禁用对清单进行自动签名，这样便无需首先将应用程序与签名的清单一起发布（如上述过程所述）。  
  
3. 发布应用程序。  
  
## <a name="see-also"></a>请参阅  
 [具有强名称的程序集](https://msdn.microsoft.com/library/d4a80263-f3e0-4d81-9b61-f0cbeae3797b)   
 [如何：创建公钥 / 私钥对](https://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)   
 [“项目设计器”->“签名”页](../ide/reference/signing-page-project-designer.md)   
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
