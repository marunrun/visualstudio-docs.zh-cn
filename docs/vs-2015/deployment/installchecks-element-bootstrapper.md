---
title: '&lt;InstallChecks &gt; 元素（引导程序） |Microsoft Docs'
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
- <InstallChecks> element [bootstrapper]
ms.assetid: ad329c87-b0ad-4304-84de-ae9496514c42
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e78f3c1174d2a288a9ffc432f0206aed4956fe8f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531815"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;InstallChecks &gt; 元素（引导程序）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`InstallChecks`元素支持对本地计算机启动各种测试，以确保已安装应用程序的所有适当的先决条件。  
  
## <a name="syntax"></a>语法  
  
```  
<InstallChecks>  
    <AssemblyCheck   
        Property  
        Name  
        PublicKeyToken  
        Version  
        Language  
        ProcessorArchitecture  
    />  
    <RegistryCheck  
        Property  
        Key  
        Value  
    />  
    <ExternalCheck   
        PackageFile  
        Property  
        Arguments  
    />  
    <FileCheck   
        Property  
        FileName  
        SearchPath  
        SpecialFolder  
        SearchDepth  
    />  
    <MsiProductCheck   
        Property  
        Product  
        Feature  
    />  
    <RegistryFileCheck   
        Property  
        Key  
        Value  
        FileName  
        SearchDepth  
    />  
</InstallChecks>  
```  
  
## <a name="assemblycheck"></a>AssemblyCheck  
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `AssemblyCheck` ，引导程序将确保由元素标识的程序集存在于全局程序集缓存（GAC）中。 它不包含任何元素，并且具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|  
|`Name`|必需。 要检查的程序集的完全限定名称。|  
|`PublicKeyToken`|必需。 与此强名称程序集关联的公钥的缩写形式。 GAC 中存储的所有程序集都必须具有名称、版本和公钥。|  
|`Version`|必需。 该程序集的版本。<br /><br /> 版本号的格式为 \<*major version*> ... \<*minor version*> \<*build version*> \<*revision version*> 。|  
|`Language`|可选。 本地化程序集的语言。 默认值为 `neutral`。|  
|`ProcessorArchitecture`|可选。 此安装所针对的计算机处理器。 默认值为 `msil`。|  
  
## <a name="externalcheck"></a>ExternalCheck  
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `ExternalCheck` ，引导程序将在单独的进程中执行命名的外部程序，并在指示的属性中存储其退出代码 `Property` 。 `ExternalCheck`对于实现复杂的依赖项检查非常有用，或者当检查组件是否存在的唯一方法是对其进行实例化时。  
  
 `ExternalCheck`不包含任何元素，并且具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|  
|`PackageFile`|必需。 要执行的外部程序。 此程序必须是安装分发包的一部分。|  
|`Arguments`|可选。 向名为的可执行文件提供命令行参数 `PackageFile` 。|  
  
## <a name="filecheck"></a>FileCheck  
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `FileCheck` ，引导程序将确定指定的文件是否存在，并返回该文件的版本号。 如果文件没有版本号，则引导程序会将名为的属性设置 `Property` 为0。 如果该文件不存在， `Property` 则不会将设置为任何值。  
  
 `FileCheck`不包含任何元素，并且具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|  
|`FileName`|必需。 要查找的文件的名称。|  
|`SearchPath`|必需。 要在其中查找文件的磁盘或文件夹。 如果分配了，则此路径必须是相对路径 `SpecialFolder` ; 否则，它必须是绝对路径。|  
|`SpecialFolder`|可选。 对 Windows 或的具有特殊意义的文件夹 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。 默认值是解释 `SearchPath` 为绝对路径。 有效值包括以下值：<br /><br /> `AppDataFolder`. 此应用程序的应用程序数据文件夹 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ; 特定于当前用户。<br /><br /> `CommonAppDataFolder`. 所有用户使用的应用程序数据文件夹。<br /><br /> `CommonFilesFolder`. 当前用户的 "公共文件" 文件夹。<br /><br /> `LocalDataAppFolder`. 非漫游应用程序的数据文件夹。<br /><br /> `ProgramFilesFolder`. 32位应用程序的标准 Program Files 文件夹。<br /><br /> `StartUpFolder`. 包含系统启动时启动的所有应用程序的文件夹。<br /><br /> `SystemFolder`. 包含32位系统 Dll 的文件夹。<br /><br /> `WindowsFolder`. 包含 Windows 系统安装的文件夹。<br /><br /> `WindowsVolume`. 包含 Windows 系统安装的驱动器或分区。|  
|`SearchDepth`|可选。 在其中搜索指定文件的子文件夹的深度。 搜索深度优先。 默认值为0，该值将搜索限制为由和 SearchPath 指定的顶层文件夹 `SpecialFolder` 。 **SearchPath**|  
  
## <a name="msiproductcheck"></a>MsiProductCheck  
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `MsiProductCheck` ，引导程序将进行检查，以确定指定的 Microsoft Windows Installer 安装是否已运行完毕。 根据安装的产品的状态设置属性值。 正值表示已安装产品，0或-1 表示未安装该产品。 （有关详细信息，请参阅 Windows Installer SDK 函数 MsiQueryFeatureState。）. 如果未在计算机上安装 Windows Installer， `Property` 则不设置。  
  
 `MsiProductCheck`不包含任何元素，并且具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|  
|`Product`|必需。 已安装产品的 GUID。|  
|`Feature`|可选。 已安装应用程序的特定功能的 GUID。|  
  
## <a name="registrycheck"></a>RegistryCheck  
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `RegistryCheck` ，引导程序将进行检查以确定指定的注册表项是否存在，或其是否具有指示的值。  
  
 `RegistryCheck`不包含任何元素，并且具有以下属性。  
  
|特性|说明|  
|---------------|-----------------|  
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|  
|`Key`|必需。 注册表项的名称。|  
|`Value`|可选。 要检索的注册表值的名称。 默认值为返回默认值的文本。 `Value`必须是字符串或 DWORD。|  
  
## <a name="registryfilecheck"></a>RegistryFileCheck  
 此元素是的可选子元素 `InstallChecks` 。 对于每个实例 `RegistryFileCheck` ，引导程序将检索指定文件的版本，并首先尝试从指定的注册表项检索文件的路径。 如果要在注册表中指定为值的目录中查找文件，此方法特别有用。  
  
 `RegistryFileCheck`不包含任何元素，并且具有以下属性。  
  
|特性|说明|  
|---------------|-----------------|  
|`Property`|必需。 要存储结果的属性的名称。 可以从元素下的测试中引用此属性 `InstallConditions` ，该元素是元素的子元素 `Command` 。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|  
|`Key`|必需。 注册表项的名称。 它的值被解释为文件的路径，除非 `File` 已设置该属性。 如果此项不存在， `Property` 则不设置。|  
|`Value`|可选。 要检索的注册表值的名称。 默认值为返回默认值的文本。 `Value`必须是字符串。|  
|`FileName`|可选。 文件的名称。 如果已指定，则假定从注册表项获取的值为目录路径，此名称追加到该路径。 如果未指定，则假定从注册表返回的值为文件的完整路径。|  
|`SearchDepth`|可选。 在其中搜索指定文件的子文件夹的深度。 搜索深度优先。 默认值为0，该值将搜索限制为注册表项的值所指定的顶级文件夹。|  
  
## <a name="remarks"></a>备注  
 当下的元素 `InstallChecks` 定义要运行的测试时，它们不执行这些测试。 若要执行测试，必须 `Command` 在元素下创建元素 `Commands` 。  
  
## <a name="example"></a>示例  
 下面的代码示例演示了 `InstallChecks` 在的产品文件中使用的元素 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。  
  
```  
<InstallChecks>  
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />  
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />  
</InstallChecks>  
```  
  
## <a name="installconditions"></a>InstallConditions  
 `InstallChecks`计算时，它们将生成属性。 然后使用这些属性 `InstallConditions` 来确定包是否应安装、绕过或失败。 下表列出了 `InstallConditions` ：  
  
|“属性”|描述|
|-|-|  
|`FailIf`|如果任何 `FailIf` 条件的计算结果都为 true，包将失败。 其余条件将不会进行计算。|  
|`BypassIf`|如果任何 `BypassIf` 条件的计算结果都为 true，则将绕过包。 其余条件将不会进行计算。|  
  
## <a name="predefined-properties"></a>预定义属性  
 下表列出了 `BypassIf` 和 `FailIf` 元素：  
  
|属性|注释|可能的值|  
|--------------|-----------|---------------------|  
|`Version9X`|Windows 9X 操作系统的版本号。|4.10 = Windows 98|  
|`VersionNT`|基于 Windows NT 的操作系统的版本号。|Major.Minor.ServicePack<br /><br /> 5.0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|  
|`VersionNT64`|64位基于 Windows NT 的操作系统的版本号。|与前面所述相同。|  
|`VersionMsi`|Windows Installer 服务的版本号。|2.0 = Windows Installer 2。0|  
|`AdminUser`|指定用户在基于 Windows NT 的操作系统上是否具有管理员权限。|0 = 无管理员权限<br /><br /> 1 = 管理员权限|  
  
 例如，若要在运行 Windows 95 的计算机上阻止安装，请使用如下所示的代码：  
  
```  
<!-- Block install on Windows 95 -->  
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>  
```  
  
## <a name="see-also"></a>另请参阅  
 [\<Commands>Element](../deployment/commands-element-bootstrapper.md)   
 [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
