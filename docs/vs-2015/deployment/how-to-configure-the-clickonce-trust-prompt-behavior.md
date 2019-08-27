---
title: 如何：配置 ClickOnce 信任提示行为 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- deploying applications [ClickOnce], trust prompt
- ClickOnce applications, install without prompting
- ClickOnce applications, trust prompt
- ClickOnce deployment, trust prompt
ms.assetid: cc04fa75-012b-47c9-9347-f4216be23cf2
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 58e5f0e9154137097a94637799966ee94818fca4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150833"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>如何：配置 ClickOnce 信任提示行为
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以配置 ClickOnce 信任提示来控制是否最终用户提供的安装 ClickOnce 应用程序，如 Windows 窗体应用程序、 Windows Presentation Foundation 应用程序、 控制台应用程序、 WPF 浏览器选项应用程序和 Office 解决方案。 通过在每个最终用户的计算机上设置注册表项配置信任提示。  
  
 下表显示了可以应用于每个五个区域 （Internet、 UntrustedSites、 MyComputer、 LocalIntranet 和 TrustedSites） 的配置选项。  
  
|选项|注册表设置值|描述|  
|------------|----------------------------|-----------------|  
|启用信任提示。|`Enabled`|ClickOnce 信任提示，显示，以便最终用户可以授予对 ClickOnce 应用程序的信任。|  
|限制信任提示。|`AuthenticodeRequired`|如果 ClickOnce 应用程序使用标识的发布服务器的证书进行签名，则仅显示 ClickOnce 信任提示。|  
|禁用信任提示。|`Disabled`|任何未使用明确信任的证书进行签名的 ClickOnce 应用程序的情况下不显示 ClickOnce 信任提示。|  
  
 下表显示了每个区域的默认行为。 应用程序列是指 Windows 窗体应用程序、 Windows Presentation Foundation 应用程序、 WPF 浏览器应用程序，和控制台应用程序。  
  
|区域|应用程序|Office 解决方案|  
|----------|------------------|----------------------|  
|`MyComputer`|`Enabled`|`Enabled`|  
|`LocalIntranet`|`Enabled`|`Enabled`|  
|`TrustedSites`|`Enabled`|`Enabled`|  
|`Internet`|`Enabled`|`AuthenticodeRequired`|  
|`UntrustedSites`|`Disabled`|`Disabled`|  
  
 您可以通过启用、 限制，或禁用 ClickOnce 信任提示来覆盖这些设置。  
  
## <a name="enabling-the-clickonce-trust-prompt"></a>启用 ClickOnce 信任提示  
 希望最终用户提供的安装和运行来自该区域任何 ClickOnce 应用程序的选项时，请启用信任提示区域。  
  
#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>若要使用注册表编辑器中启用 ClickOnce 信任提示  
  
1. 打开注册表编辑器：  
  
    1. 单击“开始”，然后单击“运行”   。  
  
    2. 在中**开放**框中，键入`regedit`(或`regedit32`32 位 Windows 上)，然后单击**确定**。  
  
2. 找到以下注册表项：  
  
     \HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel  
  
     如果不存在该键，则创建它。  
  
3. 添加以下作为子项**字符串值**，如果它们尚不存在，使用下表中显示的关联值。  
  
    |字符串值子项|值|  
    |-------------------------|-----------|  
    |`Internet`|`Enabled`|  
    |`UntrustedSites`|`Disabled`|  
    |`MyComputer`|`Enabled`|  
    |`LocalIntranet`|`Enabled`|  
    |`TrustedSites`|`Enabled`|  
  
     对于 Office 解决方案，`Internet`具有默认值`AuthenticodeRequired`并`UntrustedSites`具有值`Disabled`。 对于所有其他`Internet`具有默认值`Enabled`。  
  
#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>若要以编程方式启用 ClickOnce 信任提示  
  
1. 在 Visual Studio 中创建 Visual Basic 或 Visual C# 控制台应用程序。  
  
2. 打开进行编辑的 Program.vb 或 Program.cs 文件并添加下面的代码。  
  
    ```vb  
    Dim key As Microsoft.Win32.RegistryKey  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")  
    key.SetValue("MyComputer", "Enabled")  
    key.SetValue("LocalIntranet", "Enabled")  
    key.SetValue("Internet", "Enabled")  
    key.SetValue("TrustedSites", "Enabled")  
    key.SetValue("UntrustedSites", "Disabled")  
    key.Close()  
    ```  
  
    ```csharp  
    Microsoft.Win32.RegistryKey key;  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");  
    key.SetValue("MyComputer", "Enabled");  
    key.SetValue("LocalIntranet", "Enabled");  
    key.SetValue("Internet", "AuthenticodeRequired");  
    key.SetValue("TrustedSites", "Enabled");  
    key.SetValue("UntrustedSites", "Disabled");  
    key.Close();  
    ```  
  
3. 生成并运行应用程序。  
  
## <a name="restricting-the-clickonce-trust-prompt"></a>限制 ClickOnce 信任提示  
 限制信任提示，以便解决方案必须使用之前提示用户信任决策提供具有已知标识的验证码证书进行签名。  
  
#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>若要限制 ClickOnce 信任提示使用注册表编辑器  
  
1. 打开注册表编辑器：  
  
    1. 单击“开始”，然后单击“运行”   。  
  
    2. 在中**开放**框中，键入`regedit`(或`regedit32`32 位 Windows 上)，然后单击**确定**。  
  
2. 找到以下注册表项：  
  
     \HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel  
  
     如果不存在该键，则创建它。  
  
3. 添加以下作为子项**字符串值**，如果它们尚不存在，使用下表中显示的关联值。  
  
    |字符串值子项|值|  
    |-------------------------|-----------|  
    |`UntrustedSites`|`Disabled`|  
    |`Internet`|`AuthenticodeRequired`|  
    |`MyComputer`|`AuthenticodeRequired`|  
    |`LocalIntranet`|`AuthenticodeRequired`|  
    |`TrustedSites`|`AuthenticodeRequired`|  
  
#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>若要以编程方式限制 ClickOnce 信任提示  
  
1. 在 Visual Studio 中创建 Visual Basic 或 Visual C# 控制台应用程序。  
  
2. 打开进行编辑的 Program.vb 或 Program.cs 文件并添加下面的代码。  
  
    ```vb  
    Dim key As Microsoft.Win32.RegistryKey  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")  
    key.SetValue("MyComputer", "AuthenticodeRequired")  
    key.SetValue("LocalIntranet", "AuthenticodeRequired")  
    key.SetValue("Internet", "AuthenticodeRequired")  
    key.SetValue("TrustedSites", "AuthenticodeRequired")  
    key.SetValue("UntrustedSites", "Disabled")  
    key.Close()  
    ```  
  
    ```csharp  
    Microsoft.Win32.RegistryKey key;  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");  
    key.SetValue("MyComputer", "AuthenticodeRequired");  
    key.SetValue("LocalIntranet", "AuthenticodeRequired");  
    key.SetValue("Internet", "AuthenticodeRequired");  
    key.SetValue("TrustedSites", "AuthenticodeRequired");  
    key.SetValue("UntrustedSites", "Disabled");  
    key.Close();  
    ```  
  
3. 生成并运行应用程序。  
  
## <a name="disabling-the-clickonce-trust-prompt"></a>禁用 ClickOnce 信任提示  
 您可以禁用信任提示，以便最终用户不可以选择要安装不在其安全策略中已受信任的解决方案。  
  
#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>若要通过使用注册表编辑器来禁用 ClickOnce 信任提示  
  
1. 打开注册表编辑器：  
  
    1. 单击“开始”，然后单击“运行”   。  
  
    2. 在中**开放**框中，键入`regedit`(或`regedit32`32 位 Windows 上)，然后单击**确定**。  
  
2. 找到以下注册表项：  
  
     \HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel  
  
     如果不存在该键，则创建它。  
  
3. 添加以下作为子项**字符串值**，如果它们尚不存在，使用下表中显示的关联值。  
  
    |字符串值子项|值|  
    |-------------------------|-----------|  
    |`UntrustedSites`|`Disabled`|  
    |`Internet`|`Disabled`|  
    |`MyComputer`|`Disabled`|  
    |`LocalIntranet`|`Disabled`|  
    |`TrustedSites`|`Disabled`|  
  
#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>若要以编程方式禁用 ClickOnce 信任提示  
  
1. 在 Visual Studio 中创建 Visual Basic 或 Visual C# 控制台应用程序。  
  
2. 打开进行编辑的 Program.vb 或 Program.cs 文件并添加下面的代码。  
  
    ```vb  
    Dim key As Microsoft.Win32.RegistryKey  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")  
    key.SetValue("MyComputer", "Disabled")  
    key.SetValue("LocalIntranet", "Disabled")  
    key.SetValue("Internet", "Disabled")  
    key.SetValue("TrustedSites", "Disabled")  
    key.SetValue("UntrustedSites", "Disabled")  
    key.Close()  
    ```  
  
    ```csharp  
    Microsoft.Win32.RegistryKey key;  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");  
    key.SetValue("MyComputer", "Disabled");  
    key.SetValue("LocalIntranet", "Disabled");  
    key.SetValue("Internet", "Disabled");  
    key.SetValue("TrustedSites", "Disabled");  
    key.SetValue("UntrustedSites", "Disabled");  
    key.Close();  
  
    ```  
  
3. 生成并运行应用程序。  
  
## <a name="see-also"></a>请参阅  
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)   
 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce 和验证码](../deployment/clickonce-and-authenticode.md)   
 [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)   
 [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)   
 [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [如何：设置 ClickOnce 应用程序的自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [如何：调试具有受限权限的 ClickOnce 应用程序](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [如何：为 ClickOnce 应用程序添加到客户端计算机的受信任的发行者](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)   
 [如何：对应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
