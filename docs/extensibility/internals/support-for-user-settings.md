---
title: 支持用户设置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 02bb2450196de76917e9cffc2f5f5acc6c8ee7b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704779"
---
# <a name="support-for-user-settings"></a>支持用户设置
VSPackage 可以定义一个或多个设置类别，这些类别是当用户在 **"工具**"菜单上选择 **"导入/导出设置"** 命令时仍然存在的状态变量组。 要启用此持久性，请使用 中的[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]设置 API。

 称为自定义设置点和 GUID 的注册表项定义 VSPackage 的设置类别。 VSPackage 可以支持多个设置类别，每个类别由自定义设置点定义。

- 基于互操作程序集（使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings>接口）的设置的实现应通过编辑注册表或使用注册器脚本（.rgs 文件）创建自定义设置点。 有关更多信息，请参见 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)。

- 使用托管包框架 （MPF） 的代码应通过为每个自定义设置点<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>附加到 VS 包来创建自定义设置点。

     如果单个 VSPackage 支持多个自定义设置点，则每个自定义设置点由单独的类实现，并且每个设置点都由<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>类的唯一实例注册。 因此，实现类的设置可以支持多个设置类别。

## <a name="custom-settings-point-registry-entry-details"></a>自定义设置点注册表条目详细信息
 自定义设置点在以下位置的注册表项中创建：HKLM_Software_Microsoft_VisualStudio\\*\<版本>*[用户设置\\`<CSPName>`]，`<CSPName>`其中是 VSPackage 支持的自定义设置点的名称，*\<版本>* 是[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的版本，例如 8.0。

> [!NOTE]
> 在初始化[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 时\\，可以使用备用根覆盖 HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio*\<版本>* 的根路径。 有关详细信息，请参阅[命令行开关](../../extensibility/command-line-switches-visual-studio-sdk.md)。

 注册表项的结构如下图所示：

 HKLM_软件_微软_VisualStudio\\*\<版本>[* 用户设置]

 `<CSPName`>= #12345

 包 = 'XXXXXX XXXX XXXX XXXX XXXX XXXXXX]"

 类别 = "*YyyyyyYYYYYyyyyyyyyy}"

 资源包 = "_ZZZZ ZZ ZZ ZZ ZZZZZZZZZZZZZZZZZZZZZZ_zZZ__"

 备用父项 = 类别名称

| 名称 | 类型 | 数据 | 描述 |
|-----------------|--------| - | - |
| （默认值） | REG_SZ | 自定义设置点的名称 | 键的名称`<CSPName`>是自定义设置点的未本地化名称。<br /><br /> 对于基于 MPF 的`categoryName`实现，通过将`objectName`<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>构造函数 的 和 参数合并到`categoryName_objectName`中获取密钥的名称。<br /><br /> 密钥可以是空的，也可以包含对附属 DLL 中本地化字符串的引用 ID。 此值从`objectNameResourceID`参数获取到<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>构造函数。 |
| 程序包 | REG_SZ | GUID | 实现自定义设置点的 VS 包的 GUID。<br /><br /> 基于 MPF 使用<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>类实现的使用构造函数的`objectType`参数包含 VSPackage 的<xref:System.Type>和反射以获取此值。 |
| 类别 | REG_SZ | GUID | 识别设置类别的 GUID。<br /><br /> 对于基于内部程序集的实现，此值可以是任意选择的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]GUID，IDE 将 GUID 传递给 和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A>方法。 这两种方法的所有实现都应验证其 GUID 参数。<br /><br /> 对于基于 MPF 的实现，此 GUID 由<xref:System.Type>实现设置机制的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]类获得。 |
| 资源包 | REG_SZ | GUID | 可选。<br /><br /> 如果实现 VSPackage 不提供本地化字符串，则卫星 DLL 的路径包含本地化字符串。<br /><br /> MPF 使用反射来获取正确的资源 VSPackage，因此<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>类不会设置此参数。 |
| 备用父级 | REG_SZ | 包含此自定义设置点的工具选项页面下的文件夹的名称。 | 可选。<br /><br /> 仅当设置实现支持**在**自动化模型中使用持久性机制[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]而不是自动化模型中的机制来保存状态的工具选项页时，才必须设置此值。<br /><br /> 在这些情况下，"备用父"键中的值是用于标识特定`topic`**ToolsOptions** `topic.sub-topic`页字符串的部分。 例如，对于 **"工具选项"** 页`"TextEditor.Basic"`，备用父项的值为`"TextEditor"`。<br /><br /> 生成<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>自定义设置点时，它与类别名称相同。 |
