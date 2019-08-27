---
title: '&lt;命令&gt;元素 （引导程序） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Commands> element [bootstrapper]
ms.assetid: e61d5787-fe1f-4ebf-b0cf-0d7909be7ffb
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: af10c9e0b26a6ef2c8e7a98bc345b8e86017682b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205338"
---
# <a name="ltcommandsgt-element-bootstrapper"></a>&lt;命令&gt;元素 （引导程序）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Commands`元素实现下面的元素描述的测试`InstallChecks`元素，并声明哪个包[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]如果测试失败，应安装引导程序。  
  
## <a name="syntax"></a>语法  
  
```  
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
 `Commands`元素是必需的。 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Reboot`|可选。 确定是否的任何包返回重新启动退出代码应重新启动系统。 以下列表显示了有效的值：<br /><br /> `Defer`。 在重启推迟到将来的某个时间。<br /><br /> `Immediate`。 如果某个包返回了重新启动退出代码，会导致立即重新启动。<br /><br /> `None`。 使被忽略的任何重新启动请求。<br /><br /> 默认值为 `Immediate`。|  
  
## <a name="command"></a>命令  
 `Command` 元素是 `Commands` 元素的一个子元素。 一个`Commands`元素可以具有一个或多个`Command`元素。 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`PackageFile`|必需。 要安装的包的名称应该为一个或多个指定的条件`InstallConditions`返回 false。 必须通过使用在同一文件中定义包`PackageFile`元素。|  
|`Arguments`|可选。 一组命令行参数将传递到包文件。|  
|`EstimatedInstallSeconds`|可选。 估计的时间 （秒），需要安装包。 此值确定引导程序向用户显示进度栏的大小。 默认值为 0，这种情况下指定估计没有时间。|  
|`EstimatedDiskBytes`|可选。 已完成的磁盘空间，以字节为单位，在安装后将占用包的估计的大小。 在引导程序向用户显示的硬盘空间要求中使用此值。 默认值为的 0，用例引导程序不会显示任何硬盘空间要求。|  
|`EstimatedTempBytes`|可选。 临时磁盘空间，以字节为单位，包将需要的估计的量。|  
|`Log`|可选。 为包生成，相对于包的根目录的日志文件路径。|  
  
## <a name="installconditions"></a>InstallConditions  
 `InstallConditions`元素是子元素的`Command`元素。 每个`Command`元素可以具有最多一个`InstallConditions`元素。 如果没有`InstallConditions`元素存在，则指定的包`Condition`将始终运行。  
  
## <a name="bypassif"></a>BypassIf  
 `BypassIf`元素是子元素的`InstallConditions`元素，并描述了正条件在其下不应执行该命令。 每个`InstallConditions`元素可以具有零个或多`BypassIf`元素。  
  
 `BypassIf` 具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Property`|必需。 要测试的属性的名称。 该属性必须之前已由定义的子`InstallChecks`元素。 有关详细信息，请参阅[ \<InstallChecks > 元素](../deployment/installchecks-element-bootstrapper.md)。|  
|`Compare`|必需。 要执行的比较类型。 以下列表显示了有效的值：<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|  
|`Value`|必需。 要与属性比较的值。|  
|`Schedule`|可选。 名称`Schedule`定义应何时计算此规则的标记。|  
  
## <a name="failif"></a>FailIf  
 `FailIf`元素是子元素的`InstallConditions`元素，并描述了正条件应停止安装。 每个`InstallConditions`元素可以具有零个或多`FailIf`元素。  
  
 `FailIf` 具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Property`|必需。 要测试的属性的名称。 该属性必须之前已由定义的子`InstallChecks`元素。 有关详细信息，请参阅[ \<InstallChecks > 元素](../deployment/installchecks-element-bootstrapper.md)。|  
|`Compare`|必需。 要执行的比较类型。 以下列表显示了有效的值：<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|  
|`Value`|必需。 要与属性比较的值。|  
|`String`|可选。 要向用户在失败时显示的文本。|  
|`Schedule`|可选。 名称`Schedule`定义应何时计算此规则的标记。|  
  
## <a name="exitcodes"></a>ExitCodes  
 `ExitCodes`元素是子元素的`Command`元素。 `ExitCodes`元素包含一个或多个`ExitCode`元素，用于确定安装应执行什么操作来响应来自包的退出代码。 可以有一个可选`ExitCode`元素下的`Command`元素。 `ExitCodes` 没有属性。  
  
## <a name="exitcode"></a>ExitCode  
 `ExitCode`元素是子元素的`ExitCodes`元素。 `ExitCode`元素可确定安装应执行什么操作来响应来自包的退出代码。 `ExitCode` 不包含任何子元素，并具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Value`|必需。 退出代码值此`ExitCode`元素将适用。|  
|`Result`|必需。 如何安装应响应此退出代码。 以下列表显示了有效的值：<br /><br /> `Success`。 标记为已成功安装的包。<br /><br /> `SuccessReboot`。 将该包标记为已成功安装，并指示系统在重新启动。<br /><br /> `Fail`。 标记为失败的包。<br /><br /> `FailReboot`。 将该包标记为失败，并指示系统在重新启动。|  
|`String`|可选。 要对此退出代码的响应中向用户显示的值。|  
|`FormatMessageFromSystem`|可选。 确定是否使用系统提供的错误消息对应的退出代码，或使用中提供的值`String`。 有效的值为`true`，这意味着若要使用的系统提供的错误，并`false`，这意味着若要使用提供的字符串`String`。 默认值为 `false`。 如果此属性为`false`，但`String`未设置，将使用系统提供错误。|  
  
## <a name="example"></a>示例  
 下面的代码示例定义用于安装.NET Framework 2.0 的命令。  
  
```  
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
  
## <a name="see-also"></a>请参阅  
 [产品和包架构引用](../deployment/product-and-package-schema-reference.md)   
 [\<InstallChecks> 元素](../deployment/installchecks-element-bootstrapper.md)
