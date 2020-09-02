---
title: '&lt;命令 &gt; 元素 (引导程序) |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Commands> element [bootstrapper]
ms.assetid: e61d5787-fe1f-4ebf-b0cf-0d7909be7ffb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f52c862adcdaf7a95de6a90c2c330c39edcea13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900339"
---
# <a name="ltcommandsgt-element-bootstrapper"></a>&lt;命令 &gt; 元素 (引导程序) 
`Commands`元素实现元素下的元素所描述的测试 `InstallChecks` ，并在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 测试失败时声明要安装引导程序的包。

## <a name="syntax"></a>语法

```xml
<Commands
    Reboot
>
    <Command
        PackageFile
        Arguments
        EstimatedInstallSeconds
        EstimatedDiskBytes
        EstimatedTempBytes
        Log
    >
        <InstallConditions>
            <BypassIf
                Property
                Compare
                Value
                Schedule
            />
            <FailIf
                Property
                Compare
                Value
                String
                Schedule
            />
        </InstallConditions>
        <ExitCodes>
            <ExitCode
                Value
                Result
                String
            />
        </ExitCodes>
    </Command>
</Commands>
```

## <a name="elements-and-attributes"></a>元素和属性
 `Commands` 元素是必需的。 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Reboot`|可选。 确定在任何包返回重新启动退出代码时是否应重新启动系统。 以下列表显示了有效值：<br /><br /> `Defer`. 重新启动将推迟到将来的某个时间。<br /><br /> `Immediate`. 如果其中一个包返回了重新启动退出代码，则会立即重新启动。<br /><br /> `None`. 导致忽略任何重新启动请求。<br /><br /> 默认值为 `Immediate`。|

## <a name="command"></a>命令
 `Command` 元素是 `Commands` 元素的一个子元素。 `Commands`元素可以有一个或多个 `Command` 元素。 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`PackageFile`|必需。 要安装的包的名称应为指定的一个或多个条件 `InstallConditions` 返回 false。 必须使用元素在同一文件中定义包 `PackageFile` 。|
|`Arguments`|可选。 要传递到包文件中的一组命令行参数。|
|`EstimatedInstallSeconds`|可选。 安装包所需的估计时间（以秒为单位）。 此值确定引导程序向用户显示的进度栏的大小。 默认值为0，在这种情况下，不指定时间估算。|
|`EstimatedDiskBytes`|可选。 安装完成后包的估计磁盘空间量（以字节为单位）。 此值用于引导程序向用户显示的硬盘空间要求。 默认值为0，在这种情况下，引导程序不会显示任何硬盘空间要求。|
|`EstimatedTempBytes`|可选。 包将需要的估计临时磁盘空间量（以字节为单位）。|
|`Log`|可选。 包生成的日志文件的路径（相对于包的根目录）。|

## <a name="installconditions"></a>InstallConditions
 `InstallConditions`元素是元素的子元素 `Command` 。 每个 `Command` 元素最多只能有一个 `InstallConditions` 元素。 如果 `InstallConditions` 元素不存在，则由指定的包 `Condition` 将始终运行。

## <a name="bypassif"></a>BypassIf
 `BypassIf`元素是元素的子元素 `InstallConditions` ，并描述了不应执行命令的正则表达式。 每个 `InstallConditions` 元素可包含零个或多个 `BypassIf` 元素。

 `BypassIf` 具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Property`|必需。 要测试的属性的名称。 属性之前必须已由元素的子 `InstallChecks` 元素定义。 有关详细信息，请参阅 [\<InstallChecks> 元素](../deployment/installchecks-element-bootstrapper.md)。|
|`Compare`|必需。 要执行的比较的类型。 以下列表显示了有效值：<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必需。 要与属性进行比较的值。|
|`Schedule`|可选。 `Schedule`定义此规则的计算时间的标记的名称。|

## <a name="failif"></a>FailIf
 `FailIf`元素是元素的子元素 `InstallConditions` ，并且描述安装应停止的正则表达式。 每个 `InstallConditions` 元素可包含零个或多个 `FailIf` 元素。

 `FailIf` 具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Property`|必需。 要测试的属性的名称。 属性之前必须已由元素的子 `InstallChecks` 元素定义。 有关详细信息，请参阅 [\<InstallChecks> 元素](../deployment/installchecks-element-bootstrapper.md)。|
|`Compare`|必需。 要执行的比较的类型。 以下列表显示了有效值：<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必需。 要与属性进行比较的值。|
|`String`|可选。 失败时向用户显示的文本。|
|`Schedule`|可选。 `Schedule`定义此规则的计算时间的标记的名称。|

## <a name="exitcodes"></a>ExitCodes
 `ExitCodes`元素是元素的子元素 `Command` 。 `ExitCodes`元素包含一个或多个 `ExitCode` 元素，这些元素确定安装应执行的操作，以响应包中的退出代码。 元素下可以有一个可选 `ExitCode` 元素 `Command` 。 `ExitCodes` 没有属性。

## <a name="exitcode"></a>ExitCode
 `ExitCode`元素是元素的子元素 `ExitCodes` 。 `ExitCode`元素确定安装应执行的操作，以响应包中的退出代码。 `ExitCode` 不包含任何子元素，并且具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Value`|必需。 此元素应用到的退出代码值 `ExitCode` 。|
|`Result`|必需。 安装应如何应对此退出代码。 以下列表显示了有效值：<br /><br /> `Success`. 将包标记为已成功安装。<br /><br /> `SuccessReboot`. 将包标记为已成功安装，并指示系统重启。<br /><br /> `Fail`. 将包标记为失败。<br /><br /> `FailReboot`. 将包标记为失败，并指示系统重启。|
|`String`|可选。 为响应此退出代码而向用户显示的值。|
|`FormatMessageFromSystem`|可选。 确定是使用系统提供的错误消息和退出代码，还是使用中提供的值 `String` 。 有效值为 `true` ，这意味着使用系统提供的错误和 `false` ，这意味着使用提供的字符串 `String` 。 默认值为 `false`。 如果此属性为 `false` ，但 `String` 未设置，则将使用系统提供的错误。|

## <a name="example"></a>示例
 下面的代码示例定义了用于安装 .NET Framework 2.0 的命令。

```xml
<Commands Reboot="Immediate">
    <Command PackageFile="instmsia.exe"
             Arguments= ' /q /c:"msiinst /delayrebootq"'
             EstimatedInstallSeconds="20" >
        <InstallConditions>
           <BypassIf Property="VersionNT" Compare="ValueExists"/>
             BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="2.0"/>
        </InstallConditions>
        <ExitCodes>
            <ExitCode Value="0" Result="SuccessReboot"/>
            <ExitCode Value="1641" Result="SuccessReboot"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>
    </Command>
    <Command PackageFile="WindowsInstaller-KB884016-v2-x86.exe"
             Arguments= '/quiet /norestart'
             EstimatedInstallSeconds="20" >
      <InstallConditions>
          <BypassIf Property="Version9x" Compare="ValueExists"/>
          <BypassIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3"/>
          <BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="3.0"/>
          <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>
      </InstallConditions>
      <ExitCodes>
          <ExitCode Value="0" Result="Success"/>
          <ExitCode Value="1641" Result="SuccessReboot"/>
          <ExitCode Value="3010" Result="SuccessReboot"/>
          <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
      </ExitCodes>
    </Command>
    <Command PackageFile="dotnetfx.exe"
         Arguments=' /q:a /c:"install /q /l"'
         EstimatedInstalledBytes="21000000"
         EstimatedInstallSeconds="300">

        <!-- These checks determine whether the package is to be installed -->
        <InstallConditions>
            <!-- Either of these properties indicates the .NET Framework is already installed -->
            <BypassIf Property="DotNetInstalled" Compare="ValueNotEqualTo" Value="0"/>

            <!-- Block install if user does not have adminpermissions -->
            <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>

            <!-- Block install on Windows 95 -->
            <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatformWin9x"/>

            <!-- Block install on Windows 2000 SP 2 or less -->
            <FailIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3" String="InvalidPlatformWinNT"/>

            <!-- Block install if Internet Explorer 5.01 or later is not present -->
            <FailIf Property="IEVersion" Compare="ValueNotExists" String="InvalidPlatformIE" />
            <FailIf Property="IEVersion" Compare="VersionLessThan" Value="5.01" String="InvalidPlatformIE" />

            <!-- Block install if the operating system does not support x86 -->
            <FailIf Property="ProcessorArchitecture" Compare="ValueNotEqualTo" Value="Intel" String="InvalidPlatformArchitecture" />
       </InstallConditions>

        <ExitCodes>
            <ExitCode Value="0" Result="Success"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <ExitCode Value="4097" Result="Fail" String="AdminRequired"/>
            <ExitCode Value="4098" Result="Fail" String="WindowsInstallerComponentFailure"/>
            <ExitCode Value="4099" Result="Fail" String="WindowsInstallerImproperInstall"/>
            <ExitCode Value="4101" Result="Fail" String="AnotherInstanceRunning"/>
            <ExitCode Value="4102" Result="Fail" String="OpenDatabaseFailure"/>
            <ExitCode Value="4113" Result="Fail" String="BetaNDPFailure"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>

    </Command>
</Commands>
```

## <a name="see-also"></a>另请参阅
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
- [\<InstallChecks> element](../deployment/installchecks-element-bootstrapper.md)