---
title: 签署 VSIX 软件包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17179c35496fc19322c5bb951f4d04bc28e5d7bc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700092"
---
# <a name="signing-vsix-packages"></a>对 VSIX 包进行签名
扩展程序集无需在 Visual Studio 中运行之前进行签名，但最好这样做。

 如果要保护扩展并确保其未被篡改，则可以向 VSIX 包添加数字签名。 对 VSIX 进行签名后，VSIX 安装程序将显示一条消息，指示签名，以及有关签名本身的详细信息。 如果 VSIX 的内容已被修改，并且 VSIX 尚未再次签名，则 VSIX 安装程序将显示签名无效。 安装不会停止，但警告用户。

> [!IMPORTANT]
> 从 Visual Studio 2015 开始，使用 SHA256 加密以外的任何内容签名的 VSIX 软件包将标识为签名无效。 VSIX 安装未被阻止，但会警告用户。

## <a name="signing-a-vsix-with-vsixsigntool"></a>使用 VSIXSignTool 签署 VSIX
 在[VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)的 nuget.org 上[，VisualStudioExis 可利用](https://www.nuget.org/profiles/VisualStudioExtensibility)一个 SHA256 加密签名工具。

#### <a name="to-use-the-vsixsigntool"></a>使用 VSIXSign 工具

1. 将 VSIX 添加到项目。

2. 右键单击解决方案资源管理器中的项目节点，选择 **"添加&#124;管理 NuGet 包**。  有关 NuGet 和添加 NuGet 包的详细信息，请参阅[NuGet 文档](/NuGet)和[包管理器 UI](/NuGet/Tools/Package-Manager-UI)主题。

3. 从 VisualStudioExex 可性搜索 VSIXSignTool 并安装 NuGet 软件包。

4. 您现在可以从项目的本地包位置运行 VSIXSignTool。 有关签名方案（VSIXSignTool.exe /？）请查阅该工具的命令行帮助。

   例如，要使用受密码保护的证书文件进行签名：

   VSIXSignTool.exe 符号\</f 证书文件\<> \</p 密码> VSIX 文件>

## <a name="see-also"></a>请参阅
- [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
