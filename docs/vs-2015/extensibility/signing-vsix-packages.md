---
title: 对 VSIX 包进行签名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9fabe2931310b97f0c0864ea77ceef024f0e57cd
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63447216"
---
# <a name="signing-vsix-packages"></a>对 VSIX 包进行签名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

不需要扩展插件程序集进行签名之前它们可以运行在 Visual Studio 中，但它是执行此操作的好办法。  
  
 如果你想要保护你的扩展，并确保它尚未被篡改，您可以将数字签名添加到 VSIX 包。 当 VSIX 中进行了签名时，VSIX 安装程序将显示一条消息指出进行签名，以及有关签名本身的详细信息。 如果 VSIX 内容已被修改，并且不重新签名 VSIX，VSIX 安装程序将显示签名无效。 不停止安装，但警告用户。  
  
> [!IMPORTANT]
> 从 2015年开始，使用 SHA256 加密以外的任何签名的 VSIX 包将标识为具有无效签名。 VSIX 安装不会被阻止，但会警告用户。  
  
## <a name="signing-a-vsix-with-vsixsigntool"></a>签名与 VSIXSignTool VSIX  
 没有 SHA256 加密签名工具，可从[VisualStudioExtensibility](http://www.nuget.org/profiles/VisualStudioExtensibility)在 nuget.org 上[VsixSignTool](http://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)。  
  
#### <a name="to-use-the-vsixsigntool"></a>若要使用 VSIXSignTool  
  
1. 将在 VSIX 添加到项目。  
  
2. 右键单击解决方案资源管理器中的项目节点上选择**添加&#124;管理 NuGet 包**。  有关详细信息，NuGet 和添加 NuGet 包请参阅[NuGet 概述](http://docs.nuget.org/)并[使用对话框管理 NuGet 程序包](http://docs.nuget.org/Consume/Package-Manager-Dialog)。  
  
3. 从 VisualStudioExtensibility VSIXSignTool 搜索并安装 NuGet 包。  
  
4. 现在可以从项目的本地包位置运行 VSIXSignTool。 签名方案，请查阅该工具的命令行帮助 (VSIXSignTool.exe /？)。  
  
   对于要用密码保护的证书文件进行签名的示例：  
  
   VSIXSignTool.exe sign /f \<certfile> /p \<password> \<VSIXfile>  
  
## <a name="see-also"></a>请参阅  
 [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
