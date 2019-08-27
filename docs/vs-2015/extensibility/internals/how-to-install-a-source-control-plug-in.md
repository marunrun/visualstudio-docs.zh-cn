---
title: 如何：安装源代码管理插件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 997e734f6d2ab6bcf70e3a4843ac66564683c79b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443312"
---
# <a name="how-to-install-a-source-control-plug-in"></a>如何：安装源代码管理插件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建源代码管理插件过程包括三个步骤：  
  
1. 使用本文档的源控制插件 API 参考部分中定义的函数创建一个 DLL。  
  
2. 实现源控件插件 API 定义的函数。 当[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调用它，使接口和对话框可从该插件。  
  
3. 相应的注册表项，从而注册该 DLL。  
  
## <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 支持源代码管理插件符合源控制插件 API。  
  
### <a name="registering-the-source-control-plug-in"></a>注册的源代码管理插件  
 正在运行的集成的开发环境 (IDE) 可以调入源代码管理系统之前，必须首先找到源控制导出 API 的插件 DLL。  
  
##### <a name="to-register-the-source-control-plug-in-dll"></a>若要注册的源控件插件 DLL  
  
1. 添加指定你的产品名称子项后跟你公司名称子项软件子项中的 HKEY_LOCAL_MACHINE 项下的两个条目。 模式是 HKEY_LOCAL_MACHINE\SOFTWARE\\ *[公司名称]*\\ *[产品名称]*\\ *[entry]* = value。 SCCServerName 和 SCCServerPath 始终调用两个条目。 每个是规则的字符串。  
  
     例如，如果你的公司名称为 Microsoft 和您的源代码管理产品名为 SourceSafe 中，则此注册表路径将为 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe。 此子项中的第一个条目，SCCServerName，是命名您的产品的用户可读字符串。 第二个条目，SCCServerPath，是对源的完整路径来控制 IDE 应连接到的插件 DLL。 下面提供了示例注册表项：  
  
    |示例注册表项|示例值|  
    |---------------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerPath|c:\vss\win32\ssscc.dll|  
  
    > [!NOTE]
    > SCCServerPath 是 SourceSafe 插件的完整路径。 您的源代码管理插件将使用不同的公司和产品名称，但相同的注册表项路径。  
  
2. 可以使用以下可选的注册表项来修改您的源代码管理插件的行为。 这些项进入 SccServerPath SccServerName 以及相同的子项。  
  
    - 如果不希望您的源控制即插即用-接程序显示的插件选择列表中，可以使用 HideInVisualStudioregistry 条目[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 此项还会影响自动切换到源代码管理插件。 为此条目的可能用途之一是如果您提供替换您的源代码管理插件源代码管理包，但你想要方便用户使用源代码管理插件到源代码管理包进行迁移。 安装源代码管理包时，它会设置此注册表项，将隐藏该插件。  
  
         HideInVisualStudio 是一个 DWORD 值，并设置为 1 可隐藏该插件或 0，以显示该插件。 如果未显示的注册表项，默认行为是显示该插件。  
  
    - 可以使用 DisableSccManager 注册表项来禁用或隐藏**启动\<源代码管理服务器 >** 在正常情况下出现的菜单选项**文件** ->  **源代码管理**子菜单。 选择此菜单选项调用[SccRunScc](../../extensibility/sccrunscc-function.md)函数。 您的源代码管理插件可能不支持外部程序，因此你可能想要禁用或甚至隐藏**启动**菜单选项。  
  
         DisableSccManager 是 DWORD 值设置为 0，以启用**启动\<源代码管理服务器 >** 菜单选项，设置为 1 可禁用的菜单选项，并将设置为 2，若要隐藏菜单选项。 如果未显示此注册表项，默认行为是显示菜单选项。  
  
    |示例注册表项|示例值|  
    |---------------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\DisableSccManager|1|  
  
3. 添加该子项，SourceCodeControlProvider，在软件的子项中的 HKEY_LOCAL_MACHINE 项下。  
  
     在此子项下的注册表项 ProviderRegKey 设置为一个字符串，表示放在步骤 1 中在注册表中的子项。 模式是 HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey = 软件\\ *[公司名称]*\\ *[产品名称]*。  
  
     下面是此子项的示例内容。  
  
    |注册表项|示例值|  
    |--------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|  
  
    > [!NOTE]
    > 您的源代码管理插件将使用相同的子项和项的名称，但将不同的值。  
  
4. 创建下 SourceCodeControlProvider 子项中，名为 InstalledSCCProviders 一个子项，然后进行该子项下的一个条目。  
  
     此项的名称为提供程序 （与相同 SCCServerName 条目为指定的值），用户可读名称，值为再次重申，步骤 1 中创建的子项。 模式是 HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\\ *[显示名称]* = 软件\\ *[公司名称]* \\ *[产品名称]*。  
  
     例如：  
  
    |示例注册表项|示例值|  
    |---------------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|  
  
    > [!NOTE]
    > 可以有多个源控制插件在这种方式中注册。 这是如何[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]查找所有已安装的基于源控制插件 API 的插件。  
  
## <a name="how-an-ide-locates-the-dll"></a>IDE 如何定位 DLL  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE 提供两种方法可以查找源控制插件 DLL:  
  
- 查找默认的源代码管理插件，并以无提示方式连接到它。  
  
- 查找所有已注册的源控制插件，从中可以选择一个。  
  
  要在第一种方法中查找该 DLL，IDE 将查找条目 ProviderRegKey HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider 子项下。 此项的值将指向另一个子项。 IDE 将然后查找名 SccServerPath 为 HKEY_LOCAL_MACHINE 下的第二个子项中的条目。 此项的值指向该 DLL 的 IDE。  
  
> [!NOTE]
> IDE 不会从相对路径 (例如，.\NewProvider.DLL) 加载 Dll。 必须指定 DLL 的完整路径 (例如，c:\Providers\NewProvider.DLL)。 这可通过阻止未经授权或模拟插件 Dll 加载增强安全性的 IDE。  
  
 要在第二种方法中查找该 DLL，IDE 将查找所有条目的 HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider\InstalledSCCProviders 子项下<em>。</em> 每个项包含一个名称和值。 IDE 将向用户显示这些名称的列表<em>。</em> 当用户选择一个名称时，IDE 将查找指向一个子项的所选名称的值。 IDE 将查找名 SccServerPath 为 HKEY_LOCAL_MACHINE 下的子项中的条目。 该条目的值指向正确的 DLL 的 IDE。  
  
 源代码管理插件需要支持查找 DLL 的两种方式，并因此，设置 ProviderRegKey，覆盖任何以前的设置。 更重要的是，它必须本身向列表添加的 InstalledSccProviders 因此，用户可以选择的源代码管理插件，以使用。  
  
> [!NOTE]
> 由于使用 HKEY_LOCAL_MACHINE 项，因此可以将只有一个源代码管理插件注册为默认的源代码管理插件在给定计算机上 (但是，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]使用户能够确定哪些源代码管理插件他们想要实际使用的特定的解决方案）。 在安装过程中，检查以查看是否已设置源代码管理插件;如果是这样，，询问用户要设置新的源代码管理插件安装为默认值。 取消-在安装期间，不要删除通用的所有源代码控制插件在 HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider; 其他注册表子项删除仅在特定的 SCC 子项。  
  
## <a name="how-the-ide-detects-version-1213-support"></a>IDE 如何检测版本 1.2/1.3 支持  
 如何 does[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]检测是否插件支持源控制插件 API 版本 1.2 和 1.3 功能？ 若要声明高级的功能，源代码管理插件必须实现相应的函数。  
  
 首先，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]检查通过调用返回的值[SccGetVersion](../../extensibility/sccgetversion-function.md)。 它必须大于或等于 1.2。  
  
 下一步，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]确定是否将特定的新功能支持通过检查`lpSccCaps`上的参数[SccInitialize](../../extensibility/sccinitialize-function.md)。  
  
 如果满足这两个条件，可以调用在版本 1.2 和 1.3 中支持的新函数。  
  
## <a name="see-also"></a>请参阅  
 [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
