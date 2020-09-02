---
title: 如何：配置包含列表安全性
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 459cf3f33197939a916a5f11a94bbaf09e8142e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85541630"
---
# <a name="how-to-configure-inclusion-list-security"></a>如何：配置包含列表安全性
  如果你具有管理员权限，则可以配置 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示，以控制最终用户是否可以选择通过将信任决策保存到包含列表来安装 Office 解决方案。 有关包含列表的信息，请参阅 [使用包含列表信任 Office 解决方案](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 对于每个区域中每个区域的解决方案，可以设置以下选项：

- 启用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示密钥和包含列表。 可以允许最终用户向通过任何证书签名的 Office 解决方案授予信任。

- 限制 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示密钥和包含列表。 你可以允许最终用户安装使用标识发布者的证书进行签名的 Office 解决方案，但该证书尚未被信任。

- 禁用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信任提示密钥和包含列表。 你可以阻止最终用户安装未使用显式信任证书签名的任何 Office 解决方案。

## <a name="enable-the-inclusion-list"></a>启用包含列表
 如果希望向最终用户提供安装和运行来自该区域的任何 Office 解决方案的选项，请为该区域启用 "包含列表"。

### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>使用注册表编辑器启用包含列表

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在 " **打开** " 框中，键入 **regedt32.exe**，然后单击 **"确定"**。

2. 找到以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果该键不存在，请创建它。

3. 将以下子项添加为 **字符串值**（如果它们尚不存在）以及关联的值。

    |字符串值子项|值|
    |-------------------------|-----------|
    |**Internet**|**AuthenticodeRequired**|
    |**UntrustedSites**|**已禁用**|
    |**MyComputer**|**已启用**|
    |**LocalIntranet**|**已启用**|
    |**TrustedSites**|**已启用**|

     默认情况下， **Internet** 的值为 **AuthenticodeRequired** ， **UntrustedSites** 的值为 **Disabled**。

### <a name="to-enable-the-inclusion-list-programmatically"></a>以编程方式启用包含列表

1. 创建 Visual Basic 或 Visual c # 控制台应用程序。

2. 打开 Program.cs *Program.vb*文件进行编辑并*Program.cs*添加以下代码。

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "AuthenticodeRequired")
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

## <a name="restrict-the-inclusion-list"></a>限制包含列表
 限制包含列表，以便在提示用户提供信任决定之前，必须使用具有已知标识的 Authenticode 证书对解决方案进行签名。

### <a name="to-restrict-the-inclusion-list"></a>限制包含列表

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在 " **打开** " 框中，键入 **regedt32.exe**，然后单击 **"确定"**。

2. 找到以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     如果该键不存在，请创建它。

3. 将以下子项添加为 **字符串值**（如果它们尚不存在）以及关联的值。

    |字符串值子项|值|
    |-------------------------|-----------|
    |**UntrustedSites**|**已禁用**|
    |**Internet**|**AuthenticodeRequired**|
    |**MyComputer**|**AuthenticodeRequired**|
    |**LocalIntranet**|**AuthenticodeRequired**|
    |**TrustedSites**|**AuthenticodeRequired**|

     默认情况下， **Internet** 的值为 **AuthenticodeRequired** ， **UntrustedSites** 的值为 **Disabled**。

### <a name="to-restrict-the-inclusion-list-programmatically"></a>以编程方式限制包含列表

1. 创建 Visual Basic 或 Visual c # 控制台应用程序。

2. 打开 Program.cs *Program.vb*文件进行编辑并*Program.cs*添加以下代码。

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

## <a name="disable-the-inclusion-list"></a>禁用包含列表
 您可以禁用包含列表，以便最终用户仅能安装使用受信任的已知证书签名的解决方案。

### <a name="to-disable-the-inclusion-list"></a>禁用包含列表

1. 打开注册表编辑器：

    1. 单击 **“启动”** ，再单击 **“运行”** 。

    2. 在 " **打开** " 框中，键入 **regedt32.exe**，然后单击 **"确定"**。

2. 如果此注册表项尚不存在，请创建以下注册表项：

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

3. 将以下子项添加为 **字符串值**（如果它们尚不存在）以及关联的值。

    |字符串值子项|值|
    |-------------------------|-----------|
    |**UntrustedSites**|**已禁用**|
    |**Internet**|**已禁用**|
    |**MyComputer**|**已禁用**|
    |**LocalIntranet**|**已禁用**|
    |**TrustedSites**|**已禁用**|

### <a name="to-disable-the-inclusion-list-programmatically"></a>以编程方式禁用包含列表

1. 创建 Visual Basic 或 Visual c # 控制台应用程序。

2. 打开 Program.cs *Program.vb*文件进行编辑并*Program.cs*添加以下代码。

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
- [使用包含列表信任 Office 解决方案](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
