---
title: '&lt;trustInfo &gt; 元素（ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#IPermission
- urn:schemas-microsoft-com:asm.v2#PermissionSet
- urn:schemas-microsoft-com:asm.v2#assemblyRequest
- urn:schemas-microsoft-com:asm.v2#trustInfo
- urn:schemas-microsoft-com:asm.v2#defaultAssemblyRequest
- urn:schemas-microsoft-com:asm.v2#security
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- manifests [ClickOnce], trustInfo element
- <trustInfo> element [ClickOnce application manifest]
ms.assetid: 8a813a74-e158-4308-be78-565937f6af83
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5873eb18b2f803acfd5aba9444657884b1a24581
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184427"
---
# <a name="lttrustinfogt-element-clickonce-application"></a>&lt;trustInfo&gt; 元素（ClickOnce 应用程序）
描述应用程序要在客户端计算机上运行所需的最低安全权限。

## <a name="syntax"></a>语法

```xml

      <trustInfo>
   <security>
      <applicationRequestMinimum>
         <PermissionSet
            ID
            Unrestricted>
            <IPermission
               class
               version
               Unrestricted
            />
         </PermissionSet>
         <defaultAssemblyRequest
            permissionSetReference
         />
         <assemblyRequest
            name
            permissionSetReference
         />
      </applicationRequestMinimum>
      <requestedPrivileges>
         <requestedExecutionLevel
            level
            uiAccess
         />
      </requestedPrivileges>
   </security>
</trustInfo>
```

## <a name="elements-and-attributes"></a>元素和属性
 `trustInfo` 元素是必需的，它位于 `asm.v2` 命名空间中。 它没有属性，并包含下列元素。

## <a name="security"></a>security
 必需。 此元素是 `trustInfo` 元素的子元素。 它包含 `applicationRequestMinimum` 元素，但没有属性。

## <a name="applicationrequestminimum"></a>applicationRequestMinimum
 必需。 此元素是 `security` 元素的子元素，并且包含 `PermissionSet`、 `assemblyRequest`和 `defaultAssemblyRequest`元素。 此元素没有属性。

## <a name="permissionset"></a>PermissionSet
 必需。 此元素是 `applicationRequestMinimum` 元素的子元素，并且包含 `IPermission` 元素。 此元素具有以下属性。

- `ID`

     必需。 标识权限集。 此属性可为任意值。 在 `defaultAssemblyRequest` 和 `assemblyRequest` 属性中引用此 ID。

- `version`

     必需。 标识权限的版本。 此值通常为 `1`。

## <a name="ipermission"></a>IPermission
 可选。 此元素是 `PermissionSet` 元素的子元素。 `IPermission`元素在 .NET Framework 中完全标识权限类。 `IPermission` 元素具有以下属性，但可具有与权限类上属性对应的其他属性。 若要找出特定权限的语法，请参阅 Security.config 文件中列出的示例。

- `class`

     必需。 按强名称来标识权限类。 例如，下面的代码标识 `FileDialogPermission` 类型。

     `System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`

- `version`

     必需。 标识权限的版本。 此值通常为 `1`。

- `Unrestricted`

     必需。 标识应用程序是否需要不受限制地授予此权限。 如果为 `true`，则权限授予是无条件的。 如果为 `false`或者未定义此属性，则它根据 `IPermission` 标记上定义的特定于权限的属性进行限制。 以下列权限为例：

    ```xml
    <IPermission
      class="System.Security.Permissions.EnvironmentPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
      version="1"
      Read="USERNAME" />
    <IPermission
      class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
      version="1"
      Unrestricted="true" />
    ```

     在此示例中， <xref:System.Security.Permissions.EnvironmentPermission> 的声明限制应用程序仅读取环境变量 USERNAME，而 <xref:System.Security.Permissions.FileDialogPermission> 的声明使应用程序可以不受限制地使用所有 <xref:System.Windows.Forms.FileDialog> 类。

## <a name="defaultassemblyrequest"></a>defaultAssemblyRequest
 可选。 标识授予到所有程序集的权限集。 此元素是 `applicationRequestMinimum` 元素的子元素，并且包含以下元素。

- `permissionSetReference`

     必需。 标识为默认权限的权限集的 ID。 在 `PermissionSet` 元素中声明权限集。

## <a name="assemblyrequest"></a>assemblyRequest
 可选。 标识特定程序集的权限。 此元素是 `applicationRequestMinimum` 元素的子元素，并且包含下列元素。

- `Name`

     必需。 标识程序集名称。

- `permissionSetReference`

     必需。 标识此程序集必需的权限集的 ID。 在 `PermissionSet` 元素中声明权限集。

## <a name="requestedprivileges"></a>requestedPrivileges
 可选。 此元素是 `security` 元素的子元素，并且包含 `requestedExecutionLevel` 元素。 此元素没有属性。

## <a name="requestedexecutionlevel"></a>requestedExecutionLevel
 可选。 标识要执行应用程序请求的安全级别。 此元素没有子元素但具有以下属性。

- `Level`

   必需。 标识应用程序正在请求的安全级别。 可能的值包括：

   `asInvoker`，不请求其他权限。 此级别不需要其他信任提示。

   `highestAvailable`，请求可用于父进程的最高权限。

   `requireAdministrator`，请求完全管理员权限。

   [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序只会以 `asInvoker`的值进行安装。 以任何其他值安装都将失败。

- `uiAccess`

   可选。 指示应用程序是否需要访问受保护用户界面元素的权限。 值为 `true` 或 `false`，且默认值为 false。 只有已签名的应用程序才应具有为 true 的值。

## <a name="remarks"></a>备注
 如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序要求多于客户端计算机将默认授予的权限，则公共语言运行时的信任关系管理器将询问用户是否想要授予该应用程序这一提升的信任级别。 如果她说否，则不会运行该应用程序；否则，将使用请求的权限运行它。

 将授予所有使用 `defaultAssemblyRequest` 和 `assemblyRequest` 请求的权限，而无需提示用户该部署清单是否具有有效的信任许可证。

 有关权限提升的详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。 有关策略部署的详细信息，请参阅 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。

## <a name="examples"></a>示例
 下面的三个代码示例说明了默认命令的安全区域的 `trustInfo` 元素 - Internet、LocalIntranet 和 FullTrust - 用于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的应用程序清单中。

 第一个示例说明了 Internet 安全区域内可用的默认权限的 `trustInfo` 元素。

```xml
<trustInfo>
    <security>
      <applicationRequestMinimum>
        <PermissionSet ID="Internet">
          <IPermission
            class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Access="Open" />
          <IPermission
           class="System.Security.Permissions.IsolatedStorageFilePermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Allowed="DomainIsolationByUser"
            UserQuota="10240" />
          <IPermission
            class="System.Security.Permissions.SecurityPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Flags="Execution" />
          <IPermission
            class="System.Security.Permissions.UIPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Window="SafeTopLevelWindows"
            Clipboard="OwnClipboard" />
          <IPermission
            class="System.Drawing.Printing.PrintingPermission, System.Drawing, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
            version="1"
            Level="SafePrinting" />
        </PermissionSet>
        <defaultAssemblyRequest permissionSetReference="Internet" />
      </applicationRequestMinimum>
    </security>
  </trustInfo>
```

 第二个示例说明了 LocalIntranet 安全区域内可用的默认权限的 `trustInfo` 元素。

```xml
<trustInfo>
    <security>
      <applicationRequestMinimum>
        <PermissionSet ID="LocalIntranet">
          <IPermission
            class="System.Security.Permissions.EnvironmentPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Read="USERNAME" />
          <IPermission
            class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Unrestricted="true" />
          <IPermission
            class="System.Security.Permissions.IsolatedStorageFilePermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Allowed="AssemblyIsolationByUser"
            UserQuota="9223372036854775807"
            Expiry="9223372036854775807"
            Permanent="True" />
          <IPermission
            class="System.Security.Permissions.ReflectionPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Flags="ReflectionEmit" />
          <IPermission
            class="System.Security.Permissions.SecurityPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Flags="Assertion, Execution" />
          <IPermission
            class="System.Security.Permissions.UIPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Unrestricted="true" />
          <IPermission
            class="System.Net.DnsPermission, System, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Unrestricted="true" />
          <IPermission
            class="System.Drawing.Printing.PrintingPermission, System.Drawing, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
            version="1"
            Level="DefaultPrinting" />
          <IPermission
            class="System.Diagnostics.EventLogPermission, System, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1" />
        </PermissionSet>
        <defaultAssemblyRequest permissionSetReference="LocalIntranet" />
      </applicationRequestMinimum>
    </security>
</trustInfo>
```

 第三个示例说明了 FullTrust 安全区域内可用的默认权限的 `trustInfo` 元素。

```xml
<trustInfo>
  <security>
    <applicationRequestMinimum>
      <PermissionSet ID="FullTrust" Unrestricted="true" />
      <defaultAssemblyRequest permissionSetReference="FullTrust" />
    </applicationRequestMinimum>
  </security>
</trustInfo>
```

## <a name="see-also"></a>请参阅
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)