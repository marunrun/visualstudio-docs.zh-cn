---
title: 对用户设置的支持 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691810"
---
# <a name="support-for-user-settings"></a>支持用户设置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage 可以定义一个或多个设置类别，这些类别是用户选择 "**工具**" 菜单上的 "**导入/导出设置**" 命令时保留的状态变量组。 若要启用此持久性，请使用中的 "设置" Api [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 。  
  
 称为自定义设置点和 GUID 的注册表项定义 VSPackage 的设置类别。 VSPackage 可以支持多个设置类别，每个类别都由自定义设置点定义。  
  
- 使用接口)  (基于互操作程序集的设置的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings> 应通过以下方法来创建自定义设置点：编辑注册表或使用注册器脚本 ( .rgs 文件) 。 有关更多信息，请参见 [Creating Registrar Scripts](https://msdn.microsoft.com/library/cbd5024b-8061-4a71-be65-7fee90374a35)。  
  
- 使用托管包框架 (MPF) 的代码应通过将附加 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 到每个自定义设置点的 VSPackage，来创建自定义设置点。  
  
     如果单个 VSPackage 支持多个自定义设置点，则每个自定义设置点都由单独的类实现，并且每个点都由类的唯一实例注册 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 。 因此，实现类的设置可以支持多个设置类别。  
  
## <a name="custom-settings-point-registry-entry-details"></a>自定义设置点注册表条目详细信息  
 在以下位置的注册表项中创建自定义设置点： HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \UserSettings \\ `<CSPName>` ，其中 `<CSPName>` 是 VSPackage 支持的自定义设置点的名称， *\<Version>* 是的版本 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，例如8.0。  
  
> [!NOTE]
> \\ *\<Version>* 当 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 初始化集成开发环境 (IDE) 时，可以使用备用根覆盖 HKEY_LOCAL_MACHINE \software\microsoft\visualstudio 的根路径。 有关详细信息，请参阅 [命令行开关](../../extensibility/command-line-switches-visual-studio-sdk.md)。  
  
 注册表项的结构如下所示：  
  
 HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \UserSettings\  
  
 `<CSPName`>= s "#12345"  
  
 Package = "{XXXXXX XXXX xxxx XXXXXXXXX}"  
  
 Category = "{YYYYYY YYYY yyyy YYYYYYYYY}"  
  
 ResourcePackage = ' {ZZZZZZ ZZZZ ZZZZ ZZZZ ZZZZZZZZZ} '  
  
 AlternateParent = 类别名称  
  
|名称|类型|数据|说明|  
|----------|----------|----------|-----------------|  
|（默认值）|REG_SZ|自定义设置点的名称|密钥的名称 `<CSPName`> 是自定义设置点的未本地化名称。<br /><br /> 对于基于 MPF 的实现，密钥的名称是通过将 `categoryName` 构造函数的和 `objectName` 自变量组合 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 到来获取的 `categoryName_objectName` 。<br /><br /> 该键可以为空，也可以包含附属 DLL 中本地化字符串的引用 ID。 此值从自变量获取 `objectNameResourceID` 到 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 构造函数。|  
|包|REG_SZ|GUID|实现自定义设置点的 VSPackage 的 GUID。<br /><br /> 基于 MPF 的实现使用 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 类，使用构造函数的 `objectType` 参数，其中包含 VSPackage 的 <xref:System.Type> 和反射来获取此值。|  
|类别|REG_SZ|GUID|标识设置类别的 GUID。<br /><br /> 对于基于互操作程序集的实现，此值可以是任意选择的 GUID，IDE 会将其 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 传递到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A> 方法。 这两种方法的所有实现都应该验证其 GUID 参数。<br /><br /> 对于基于 MPF 的实现，此 GUID 由 <xref:System.Type> 实现设置机制的类的来获取 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。|  
|ResourcePackage|REG_SZ|GUID|可选。<br /><br /> 包含本地化字符串的附属 DLL 的路径（如果实现 VSPackage 未提供）。<br /><br /> MPF 使用反射来获取正确的资源 VSPackage，因此， <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 该类不会设置此参数。|  
|AlternateParent|REG_SZ|包含此自定义设置点的 "工具选项" 页下的文件夹名称。|可选。<br /><br /> 仅当设置实现支持在中使用持久性机制（而不是自动化模型中的机制）保存状态的 **工具选项** 页时，才必须设置此值 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 。<br /><br /> 在这些情况下，AlternateParent 键中的值是 `topic` `topic.sub-topic` 用于标识特定 **ToolsOptions** 页的字符串部分。 例如，对于 **ToolsOptions** 页， `"TextEditor.Basic"` AlternateParent 的值为 `"TextEditor"` 。<br /><br /> 当 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 生成自定义设置点时，它与类别名称相同。|
