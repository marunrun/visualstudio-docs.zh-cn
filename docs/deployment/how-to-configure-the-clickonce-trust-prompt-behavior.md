---
title: 如何：配置点击信任提示行为 |微软文档
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ec5f1cca49f1b799b39969849e0a73bf1e6e296d
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649156"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>如何：配置 ClickOnce 信任提示行为
您可以配置 ClickOnce 信任提示，以控制是否允许最终用户选择安装 ClickOnce 应用程序，例如 Windows 窗体应用程序、Windows 演示文稿基础应用程序、控制台应用程序、WPF 浏览器应用程序和 Office 解决方案。 通过在每个最终用户的计算机上设置注册表项来配置信任提示。

 下表显示了可应用于五个区域（Internet、不受信任的站点、MyComputer、本地 Intranet 和受信任的站点）中的每个区域的配置选项。

|选项|注册表设置值|说明|
|------------|----------------------------|-----------------|
|启用信任提示。|`Enabled`|将显示"单击一次信任"提示，以便最终用户可以信任 ClickOnce 应用程序。|
|限制信任提示。|`AuthenticodeRequired`|仅当 ClickOnce 应用程序使用标识发布者的证书进行签名时，才会显示 ClickOnce 信任提示。|
|禁用信任提示。|`Disabled`|对于未使用显式受信任的证书签名的任何 ClickOnce 应用程序，不会显示 ClickOnce 信任提示。|

 下表显示了每个区域的默认行为。 "应用程序"列是指 Windows 窗体应用程序、Windows 演示文稿基础应用程序、WPF 浏览器应用程序和控制台应用程序。

|区域|应用程序|Office 解决方案|
|----------|------------------|----------------------|
|`MyComputer`|`Enabled`|`Enabled`|
|`LocalIntranet`|`Enabled`|`Enabled`|
|`TrustedSites`|`Enabled`|`Enabled`|
|`Internet`|`Enabled`|`AuthenticodeRequired`|
|`UntrustedSites`|`Disabled`|`Disabled`|

 您可以通过启用、限制或禁用"单击"信任提示来覆盖这些设置。

## <a name="enable-the-clickonce-trust-prompt"></a>启用"单击次数"信任提示
 当您希望向最终用户显示安装和运行来自该区域的任何 ClickOnce 应用程序的选项时，启用区域的信任提示。

#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>使用注册表编辑器启用 ClickOnce 信任提示

1. 打开注册表编辑器：

    1. 单击 **“开始”**，然后单击 **“运行”**。

    2. 在 **"打开"** 框中，`regedit`键入 ，然后单击"**确定**"。

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果密钥不存在，请创建它。

3. 如果子键不存在，则将以下子键添加为**字符串值**，并显示下表中的关联值。

    |字符串值子键|“值”|
    |-------------------------|-----------|
    |`Internet`|`Enabled`|
    |`UntrustedSites`|`Disabled`|
    |`MyComputer`|`Enabled`|
    |`LocalIntranet`|`Enabled`|
    |`TrustedSites`|`Enabled`|

     对于 Office`Internet`解决方案，具有默认值`AuthenticodeRequired`，`UntrustedSites`并且具有`Disabled`值 。 对于所有其他 ，`Internet`具有默认值`Enabled`。

#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>以编程方式启用"单击次数"信任提示

1. 在可视化工作室中创建可视化基本或可视化 C++ 控制台应用程序。

2. 打开*程序.vb*或*Program.cs*文件进行编辑并添加以下代码。

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

## <a name="restrict-the-clickonce-trust-prompt"></a>限制单击信任提示
 限制信任提示，以便在提示用户做出信任决策之前，必须使用具有已知标识的身份验证证书对解决方案进行签名。

#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>使用注册表编辑器限制 ClickOnce 信任提示

1. 打开注册表编辑器：

    1. 单击 **“开始”**，然后单击 **“运行”**。

    2. 在 **"打开"** 框中，`regedit`键入 ，然后单击"**确定**"。

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果密钥不存在，请创建它。

3. 如果子键不存在，则将以下子键添加为**字符串值**，并显示下表中的关联值。

    |字符串值子键|“值”|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`AuthenticodeRequired`|
    |`MyComputer`|`AuthenticodeRequired`|
    |`LocalIntranet`|`AuthenticodeRequired`|
    |`TrustedSites`|`AuthenticodeRequired`|

#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>以编程方式限制单击信任提示

1. 在可视化工作室中创建可视化基本或可视化 C++ 控制台应用程序。

2. 打开*程序.vb*或*Program.cs*文件进行编辑并添加以下代码。

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

## <a name="disable-the-clickonce-trust-prompt"></a>禁用"单击一次信任提示"
 您可以禁用信任提示，以便最终用户不会选择安装其安全策略中尚未信任的解决方案。

#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>使用注册表编辑器禁用 ClickOnce 信任提示

1. 打开注册表编辑器：

    1. 单击 **“开始”**，然后单击 **“运行”**。

    2. 在 **"打开"** 框中，`regedit`键入 ，然后单击"**确定**"。

2. 查找以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果密钥不存在，请创建它。

3. 如果子键不存在，则将以下子键添加为**字符串值**，并显示下表中的关联值。

    |字符串值子键|“值”|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`Disabled`|
    |`MyComputer`|`Disabled`|
    |`LocalIntranet`|`Disabled`|
    |`TrustedSites`|`Disabled`|

#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>以编程方式禁用"单击次数"信任提示

1. 在可视化工作室中创建可视化基本或可视化 C++ 控制台应用程序。

2. 打开*程序.vb*或*Program.cs*文件进行编辑并添加以下代码。

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

## <a name="see-also"></a>另请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [如何：启用 ClickOnce 安全设置](../deployment/how-to-enable-clickonce-security-settings.md)
- [如何：为 ClickOnce 应用程序设置安全区域](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [如何：为 ClickOnce 应用程序设置自定义权限](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [如何：使用受限权限对 ClickOnce 应用程序进行调试](securing-clickonce-applications.md)
- [如何：将受信任的发布者添加到用于 ClickOnce 应用程序的客户端计算机](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [如何：重新签名应用程序和部署清单](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
