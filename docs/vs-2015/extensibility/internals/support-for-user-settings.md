---
title: 支持用户设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 80734d9859df2e06bc51d40e1fffa40c7d97c7a7
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691810"
---
# <a name="support-for-user-settings"></a>支持用户设置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage 可以定义一个或多个设置类别，是一组保留在用户选择时的状态变量**导入/导出设置**命令**工具**菜单。 若要启用此持久性，您使用的设置 Api 中[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]。  
  
 自定义设置点和一个 GUID 称为一个注册表项定义的 VSPackage 的设置类别。 VSPackage 可以支持多个设置类别，每个定义的自定义设置点。  
  
- 实现基于互操作程序集的设置 (使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings>接口) 应通过编辑注册表，或者使用注册器脚本 （.rgs 文件） 创建自定义设置点。 有关详细信息，请参阅 [Creating Registrar Scripts](https://msdn.microsoft.com/library/cbd5024b-8061-4a71-be65-7fee90374a35)。  
  
- 使用托管包框架 (MPF) 的代码应通过将附加创建自定义设置点<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>到每个自定义设置点的 VSPackage。  
  
     如果单个 VSPackage 支持多个自定义设置点，由一个单独的类，实现每个自定义设置点并且每个注册的唯一实例<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>类。 因此，实现类设置可以支持多个设置类别。  
  
## <a name="custom-settings-point-registry-entry-details"></a>自定义设置点注册表项的详细信息  
 在以下位置的注册表条目中创建自定义设置点：HKLM\Software\Microsoft\VisualStudio\\ *\<版本 >* \UserSettings\\`<CSPName>`，其中`<CSPName>`是 VSPackage 支持的自定义设置点的名称并 *\<版本 >* 是版本[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，例如 8.0。  
  
> [!NOTE]
> 根路径的 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<版本 >* 可以重写使用备用根时[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成的开发环境 (IDE) 是初始化。 有关详细信息，请参阅[命令行开关](../../extensibility/command-line-switches-visual-studio-sdk.md)。  
  
 注册表项的结构如下图所示：  
  
 HKLM\Software\Microsoft\VisualStudio\\ *\<Version>* \UserSettings\  
  
 `<CSPName`>= s '#12345'  
  
 包 = ' {XXXXXX XXXX XXXX XXXX XXXXXXXXX}  
  
 Category = '{YYYYYY YYYY YYYY YYYY YYYYYYYYY}'  
  
 ResourcePackage = '{ZZZZZZ ZZZZ ZZZZ ZZZZ ZZZZZZZZZ}'  
  
 AlternateParent = CategoryName  
  
|名称|类型|数据|描述|  
|----------|----------|----------|-----------------|  
|(默认)|REG_SZ|自定义设置点的名称|密钥的名称， `<CSPName`>，是自定义设置点的未本地化的名称。<br /><br /> 为基于 MPF 实现，该密钥的名称获取通过组合`categoryName`并`objectName`的参数<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>构造函数到`categoryName_objectName`。<br /><br /> 键可以是空的也可以包含在附属 DLL 中的本地化字符串的引用的 ID。 此值从获取`objectNameResourceID`自变量<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>构造函数。|  
|package|REG_SZ|GUID|实现自定义设置点的 VSPackage 的 GUID。<br /><br /> 实现基于使用 MPF<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>类中，使用构造函数的`objectType`参数，其中包含 VSPackage 的<xref:System.Type>和反射来获取此值。|  
|类别|REG_SZ|GUID|标识设置类别的 GUID。<br /><br /> 对于基于互操作程序集的实现，此值可以是任意选定的 GUID，这[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 将传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A>方法。 这两种方法的所有实现应都验证其 GUID 参数。<br /><br /> 对于基于 MPF 实现，此 GUID 通过<xref:System.Type>类实现的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]设置机制。|  
|ResourcePackage|REG_SZ|GUID|可选。<br /><br /> 如果实现 VSPackage 不提供它们，则路径以附属 DLL 包含本地化字符串。<br /><br /> MPF 使用反射来获取正确的资源的 VSPackage，因此<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>类不会设置此参数。|  
|AlternateParent|REG_SZ|包含此自定义设置点的工具选项页下的文件夹的名称。|可选。<br /><br /> 仅当设置实现支持，必须设置此值**工具选项**使用中的持久性机制的页[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]而不是在自动化模型来保存状态的机制。<br /><br /> AlternateParent 密钥中的值是在这些情况下，`topic`一部分`topic.sub-topic`用来确定特定字符串**ToolsOptions**页。 例如，对于**ToolsOptions**页面`"TextEditor.Basic"`AlternateParent 的值将为`"TextEditor"`。<br /><br /> 当<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>生成自定义设置点，它是类别名称相同。|
