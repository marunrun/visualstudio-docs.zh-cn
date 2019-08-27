---
title: 属性函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, property functions
ms.assetid: 2253956e-3ae0-4bdc-9d3a-4881dfae4ddb
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4108e478e9e77a5ed5699b39dfae44884a6befd3
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67826180"
---
# <a name="property-functions"></a>属性函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 .NET Framework 4 和 4.5 版中，可以使用属性函数来计算 MSBuild 脚本。 可以在出现属性的任何位置使用属性函数。 与任务不同，属性函数可在目标外部使用，并在任何目标运行之前进行计算。  
  
 可以在生成脚本中读取系统时间、比较字符串、匹配正则表达式及执行其他操作，而无需使用 MSBuild 任务。 MSBuild 将尝试将字符串转换为数字、将数字转换为字符串，并根据需要进行其他转换。  
  
 **在本主题中：**  
  
- [属性函数语法](#BKMK_Syntax)  
  
  - [字符串属性函数](#BKMK_String)  

  - [静态属性函数](#BKMK_Static)  

  - [对静态属性调用实例方法](#BKMK_InstanceMethods)  

  - [MSBuild 属性函数](#BKMK_PropertyFunctions)  
  
- [嵌套的属性函数](#BKMK_Nested)  
  
- [MSBuild DoesTaskHostExist](#BKMK_DoesTaskHostExist)  
  
- [MSBuild GetDirectoryNameOfFileAbove](#BKMK_GetDirectoryNameOfFileAbove)  
  
- [MSBuild GetRegistryValue](#BKMK_GetRegistryValue)  
  
- [MSBuild GetRegistryValueFromView](#BKMK_GetRegistryValueFromView)  
  
- [MSBuild MakeRelative](#BKMK_MakeRelative)  
  
- [MSBuild ValueOrDefault](#BKMK_ValueOrDefault)  
  
## <a name="BKMK_Syntax"></a>属性函数语法  
 下面列出了三种属性函数；每种函数都有不同的语法：  
  
- 字符串（实例）属性函数  
  
- 静态属性函数  
  
- MSBuild 属性函数  
  
### <a name="BKMK_String"></a>字符串属性函数  
 所有生成属性值都只是字符串值。 可以使用字符串（实例）方法来操作任何属性值。 例如，可以使用以下代码，从表示完整路径的生成属性中提取驱动器名称（前三个字符）：  
  
 `$(ProjectOutputFolder.Substring(0,3))`  
  
### <a name="BKMK_Static"></a>静态属性函数  
 在生成脚本中，可以访问许多系统类的静态属性和方法。 要获取静态属性的值，请使用以下语法，其中 *Class* 是系统类的名称，*Property* 是属性的名称。  
  
 `$([Class]::Property)`  
  
 例如，可以使用以下代码将生成属性设置为当前日期和时间。  
  
 `<Today>$([System.DateTime]::Now)</Today>`  
  
 要调用静态方法，请使用以下语法，其中 *Class* 是系统类的名称，*Method* 是方法的名称，而 *(Parameters)* 是方法的参数列表：  
  
 `$([Class]::Method(Parameters))`  
  
 例如，要将生成属性设置为新的 GUID，可以使用以下脚本：  
  
 `<NewGuid>$([System.Guid]::NewGuid())</NewGuid>`  
  
 在静态属性函数中，可以使用以下系统类的任何静态方法或属性：  
  
- System.Byte  
  
- System.Char  
  
- System.Convert  
  
- System.DateTime  
  
- System.Decimal  
  
- System.Double  
  
- System.Enum  
  
- System.Guid  
  
- System.Int16  
  
- System.Int32  
  
- System.Int64  
  
- System.IO.Path  
  
- System.Math  
  
- System.UInt16  
  
- System.UInt32  
  
- System.UInt64  
  
- System.SByte  
  
- System.Single  
  
- System.String  
  
- System.StringComparer  
  
- System.TimeSpan  
  
- System.Text.RegularExpressions.Regex  
  
- Microsoft.Build.Utilities.ToolLocationHelper  
  
  此外，还可以使用以下静态方法和属性：  
  
- System.Environment::CommandLine  
  
- System.Environment::ExpandEnvironmentVariables  
  
- System.Environment::GetEnvironmentVariable  
  
- System.Environment::GetEnvironmentVariables  
  
- System.Environment::GetFolderPath  
  
- System.Environment::GetLogicalDrives  
  
- System.IO.Directory::GetDirectories  
  
- System.IO.Directory::GetFiles  
  
- System.IO.Directory::GetLastAccessTime  
  
- System.IO.Directory::GetLastWriteTime  
  
- System.IO.Directory::GetParent  
  
- System.IO.File::Exists  
  
- System.IO.File::GetCreationTime  
  
- System.IO.File::GetAttributes  
  
- System.IO.File::GetLastAccessTime  
  
- System.IO.File::GetLastWriteTime  
  
- System.IO.File::ReadAllText  
  
### <a name="BKMK_InstanceMethods"></a>对静态属性调用实例方法  
 如果访问返回对象实例的静态属性，则可以调用该对象的实例方法。 要调用实例方法，请使用以下语法，其中 *Class* 是系统类的名称，*Property* 是属性的名称，*Method* 是方法的名称，而 *(Parameters)* 是方法的参数列表：  
  
 `$([Class]::Property.Method(Parameters))`  
  
 类的名称必须用命名空间加以完全限定。  
  
 例如，使用以下代码可以将生成属性设置为当天的日期：Today。  
  
 `<Today>$([System.DateTime]::Now.ToString("yyyy.MM.dd"))</Today>`  
  
### <a name="BKMK_PropertyFunctions"></a>MSBuild 属性函数  
 可以访问生成中的许多静态方法，以提供算术、按位逻辑和转义字符支持。 可以使用以下语法访问这些方法，其中 *Method* 是方法的名称，*Parameters* 是方法的参数列表。  
  
 `$([MSBuild]::Method(Parameters))`  
  
 例如，要一起添加两个具有数字值的属性，请使用以下代码。  
  
 `$([MSBuild]::Add($(NumberOne), $(NumberTwo))`  
  
 下面列出了 MSBuild 属性函数：  
  
|函数签名|说明|  
|------------------------|-----------------|  
|double Add(双精度型值 a, 双精度型值 b)|将两个双精度型值相加。|  
|long Add(长型值 a, 长型值 b)|将两个长型值相加。|  
|double Subtract(双精度型值 a, 双精度型值 b)|将两个双精度型值相减。|  
|long Subtract(长型值 a, 长型值 b)|将两个长型值相减。|  
|double Multiply(双精度型值 a, 双精度型值 b)|将两个双精度型值相乘。|  
|long Multiply(长型值 a, 长型值 b)|将两个长型值相乘。|  
|double Divide(双精度型值 a, 双精度型值 b)|将两个双精度型值相除。|  
|long Divide(长型值 a, 长型值 b)|将两个长型值相除。|  
|double Modulo(双精度型值 a, 双精度型值 b)|对两个双精度型值取模。|  
|long Modulo(长型值 a, 长型值 b)|对两个长型值取模。|  
|string Escape(未转义字符串)|根据 MSBuild 转义规则对字符串进行转义。|  
|string Unescape(已转义字符串)|根据 MSBuild 转义规则取消对字符串进行转义。|  
|int BitwiseOr(第一个整型值, 第二个整型值)|对第一个值和第二个值执行按位 `OR`（第一个值 &#124; 第二个值）。|  
|int BitwiseAnd(第一个整型值, 第二个整型值)|对第一个值和第二个值执行按位 `AND`（第一个值 & 第二个值）。|  
|int BitwiseXor(第一个整型值, 第二个整型值)|对第一个值和第二个值执行按位 `XOR`（第一个值 ^ 第二个值）。|  
|int BitwiseNot(第一个整型值)|执行按位 `NOT`（~第一个值）。|  
  
## <a name="BKMK_Nested"></a>嵌套的属性函数  
 可将属性函数组合在一起，组成更复杂的函数，如下例所示。  
  
 `$([MSBuild]::BitwiseAnd(32,   $([System.IO.File]::GetAttributes(tempFile))))`  
  
 此示例返回由路径 <xref:System.IO.FileAttributes> 所指定文件的 `Archive``tempFile` 位（32 或 0）的值。 请注意，枚举的数据值不能以名称形式显示在属性函数内。 必须改用数字值 (32)。  
  
 元数据也可以出现在嵌套的属性函数中。 有关详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。  
  
## <a name="BKMK_DoesTaskHostExist"></a>MSBuild DoesTaskHostExist  
 MSBuild 中的 `DoesTaskHostExist` 属性函数将返回当前是否针对特定运行时和体系结构值安装了任务宿主。  
  
 此属性函数具有以下语法：  
  
```  
$[MSBuild]::DoesTaskHostExist(string theRuntime, string theArchitecture)  
```  
  
## <a name="BKMK_GetDirectoryNameOfFileAbove"></a>MSBuild GetDirectoryNameOfFileAbove  
 MSBuild `GetDirectoryNameOfFileAbove` 属性函数在路径中当前目录的上级目录中查找文件。  
  
 此属性函数具有以下语法：  
  
```  
$[MSBuild]::GetDirectoryNameOfFileAbove(string ThePath, string TheFile)  
```  
  
 下面的代码是此语法的示例。  
  
```  
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))\EnlistmentInfo.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))' != '' " />  
```  
  
## <a name="BKMK_GetRegistryValue"></a>MSBuild GetRegistryValue  
 MSBuild `GetRegistryValue` 属性函数返回注册表项的值。 此函数采用两个参数（项名称和值名称），并从注册表中返回值。 如果未指定值名称，则返回默认值。  
  
 下面的示例演示如何使用此函数：  
  
```  
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, ``))                                  // default value  
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, `SymbolCacheDir`))  
$([MSBuild]::GetRegistryValue(`HKEY_LOCAL_MACHINE\SOFTWARE\(SampleName)`, `(SampleValue)`))             // parens in name and value  
  
```  
  
## <a name="BKMK_GetRegistryValueFromView"></a>MSBuild GetRegistryValueFromView  
 MSBuild `GetRegistryValueFromView` 属性函数在给定了注册表项、值以及一个或多个经过排序的注册表视图的情况下，获取系统注册表数据。 该属性函数将按顺序在每个注册表视图中搜索注册表项和值，直至找到它们。  
  
 该属性函数的语法是：  
  
 [MSBuild\]::GetRegistryValueFromView(string keyName, string valueName, object defaultValue, params object[] views)  
  
 Windows 64 位操作系统维护一个 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node 注册表项，它表示 32 位应用程序的 HKEY_LOCAL_MACHINE\SOFTWARE 注册表视图。  
  
 默认情况下，在 WOW64 上运行的 32 位应用程序将访问 32 位注册表视图，而 64 位应用程序将访问 64 位注册表视图。  
  
 以下这些注册表视图是可用的：  
  
|注册表视图|定义|  
|-------------------|----------------|  
|RegistryView.Registry32|32 位应用程序注册表视图。|  
|RegistryView.Registry64|64 位应用程序注册表视图。|  
|RegistryView.Default|与应用程序正在其中运行的进程匹配的注册表视图。|  
  
 下面是一个示例。  
  
 `$([MSBuild]::GetRegistryValueFromView('HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SDKs\Silverlight\v3.0\ReferenceAssemblies', 'SLRuntimeInstallPath', null, RegistryView.Registry64, RegistryView.Registry32))`  
  
 首先在 64 位注册表视图中查找，然后在 32 位注册表视图中查找，以获取 ReferenceAssemblies 项的 SLRuntimeInstallPath 数据。  
  
## <a name="BKMK_MakeRelative"></a>MSBuild MakeRelative  
 MSBuild `MakeRelative` 属性函数将返回第二条路径的相对路径（相对于第一条路径）。 每条路径可以是文件或文件夹。  
  
 此属性函数具有以下语法：  
  
```  
$[MSBuild]::MakeRelative($(FileOrFolderPath1), $(FileOrFolderPath2))  
```  
  
 下面的代码是此语法的示例。  
  
```xml  
<PropertyGroup>  
    <Path1>c:\users\</Path1>  
    <Path2>c:\users\username\</Path2>  
</PropertyGroup>  
  
<Target Name = "Go">  
    <Message Text ="$([MSBuild]::MakeRelative($(Path1), $(Path2)))" />  
    <Message Text ="$([MSBuild]::MakeRelative($(Path2), $(Path1)))" />  
</Target>  
  
<!--  
Output:  
   username\  
   ..\  
-->  
```  
  
## <a name="BKMK_ValueOrDefault"></a>MSBuild ValueOrDefault  
 MSBuild `ValueOrDefault` 属性函数将返回第一个参数，除非它为 null 或空。 如果第一个参数为 null 或空，则该函数将返回第二个参数。  
  
 下面的示例演示如何使用此函数。  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <Value1>$([MSBuild]::ValueOrDefault(`$(UndefinedValue)`, `a`))</Value1>  
        <Value2>$([MSBuild]::ValueOrDefault(`b`, `$(Value1)`))</Value2>  
    </PropertyGroup>  
  
    <Target Name="MyTarget">  
        <Message Text="Value1 = $(Value1)" />  
        <Message Text="Value2 = $(Value2)" />  
    </Target>  
</Project>  
  
<!--  
Output:   
  Value1 = a  
  Value2 = b  
-->  
```

## <a name="see-also"></a>另请参阅
[MSBuild 属性](msbuild-properties1.md)   
[MSBuild 概述](msbuild.md)
