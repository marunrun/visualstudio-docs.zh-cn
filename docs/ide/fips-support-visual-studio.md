---
title: Visual Studio 支持 FIPS 140-2 批准的操作模式
ms.date: 04/14/2020
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 06d147397a168bb78a31a8fbe6929d6c2184d080
ms.sourcegitcommit: cc58ca7ceae783b972ca25af69f17c9f92a29fc2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81386686"
---
# <a name="visual-studio-support-for-the-fips-140-2-approved-mode-of-operation"></a>Visual Studio 支持 FIPS 140-2 批准的操作模式

从[版本 16.4](/visualstudio/releases/2019/release-notes-v16.4/) 开始，Visual Studio 2019 支持联邦信息处理标准 (FIPS) 出版物 140-2 批准的 Windows、Azure 和 .NET 操作模式。 而且，使用[版本 16.5](/visualstudio/releases/2019/release-notes-v16.5/)，在开发[面向远程 Linux 系统的 C++ 应用程序](/cpp/linux/set-up-fips-compliant-secure-remote-linux-development/)时，Visual Studio 现在支持 FIPS 140-2 批准的操作模式。

要配置 FIPS 140-2 批准的 Visual Studio 操作模式，请[安装 .NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48)，然后启用组策略设置“系统加密:  对加密、哈希和签名使用符合 FIPS 的算法”。

有关 FIPS 140-2 批准的操作模式以及如何启用它的详细信息，请参阅 [FIPS 140-2 验证](/windows/security/threat-protection/fips-140-validation/)。

> [!NOTE]
> 用于开发非 Microsoft 平台（如 iOS 或 Android）应用的工具可能不会使用符合 FIPS 的算法。 Visual Studio 附带的第三方软件或者由你安装的扩展也无法使用符合 FIPS 140-2 的算法。 而且，[SharePoint](/sharepoint/security-for-sharepoint-server/federal-information-processing-standard-security-standards/) 解决方案的开发不支持 FIPS 140-2 批准的操作模式。

## <a name="next-steps"></a>后续步骤

要详细了解 FIPS 140-2 批准的 Visual Studio 及其他 Microsoft 产品和服务的操作模式，请参阅以下链接：

- [Visual Studio：使用 C++ 设置符合 FIPS 的安全远程 Linux 开发](/cpp/linux/set-up-fips-compliant-secure-remote-linux-development/)
- [Windows：系统加密以及使用符合 FIPS 的算法进行加密、哈希和签名](/windows/security/threat-protection/security-policy-settings/system-cryptography-use-fips-compliant-algorithms-for-encryption-hashing-and-signing)
- [.NET Core：符合 FIPS](/dotnet/standard/security/fips-compliance/)

## <a name="see-also"></a>请参阅

[保护应用程序](securing-applications.md)