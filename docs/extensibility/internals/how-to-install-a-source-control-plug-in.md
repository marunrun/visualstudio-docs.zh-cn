---
title: 如何：安装源代码管理插件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9de10f1aebd47093a3cc3f41343e73cefdde473a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334915"
---
# <a name="how-to-install-a-source-control-plug-in"></a>如何：安装源代码管理插件
创建源代码管理插件过程包括三个步骤：

1. 使用本文档的源控制插件 API 参考部分中定义的函数创建一个 DLL。

2. 实现源控件插件 API 定义的函数。 当[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调用它，使接口和对话框可从该插件。

3. 相应的注册表项，从而注册该 DLL。

## <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持源代码管理插件符合源控制插件 API。

### <a name="register-the-source-control-plug-in"></a>注册的源代码管理插件
 正在运行的集成的开发环境 (IDE) 可以调入源代码管理系统之前，必须首先找到源控制导出 API 的插件 DLL。

#### <a name="to-register-the-source-control-plug-in-dll"></a>若要注册的源控件插件 DLL

1. 添加两个条目下的**HKEY_LOCAL_MACHINE**中的键**软件**指定你的公司名称子项的子项后, 跟你的产品名称子项。 模式是**HKEY_LOCAL_MACHINE\SOFTWARE\\\<公司名称 >\\\<产品名称 >\\\<条目 >**  =  *值*。 始终调用两个条目**SCCServerName**并**SCCServerPath**。 每个是规则的字符串。

    例如，如果你的公司名称是 Microsoft 和 SourceSafe 名为你的源代码管理产品，则此注册表路径应**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe**。 在第一个项，此子项**SCCServerName**，是命名您的产品的用户可读字符串。 第二个条目**SCCServerPath**，是对源的完整路径来控制 IDE 应连接到的插件 DLL。 下面提供了示例注册表项：

   |示例注册表项|示例值|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerPath|*c:\vss\win32\ssscc.dll*|

   > [!NOTE]
   > SCCServerPath 是 SourceSafe 插件的完整路径。 您的源代码管理插件将使用不同的公司和产品名称，但相同的注册表项路径。

2. 可以使用以下可选的注册表项来修改您的源代码管理插件的行为。 这些项进入作为相同的子项**SccServerName**并**SccServerPath**。

   - **HideInVisualStudioregistry**如果不希望您的源控制即插即用-接程序显示在中，可以使用条目**插件选择**系列[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 此项还会影响自动切换到源代码管理插件。 为此条目的可能用途之一是如果您提供替换您的源代码管理插件源代码管理包，但你想要方便用户使用源代码管理插件到源代码管理包进行迁移。 安装源代码管理包时，它会设置此注册表项，将隐藏该插件。

      **HideInVisualStudio**是一个 DWORD 值并将设置为*1*若要隐藏该插件或*0*以显示该插件。 如果未显示的注册表项，默认行为是显示该插件。

   - **DisableSccManager**注册表项可用于禁用或隐藏**启动\<源代码管理服务器 >** 下正常情况下出现的菜单选项**文件** > **源代码管理**子菜单。 选择此菜单选项调用[SccRunScc](../../extensibility/sccrunscc-function.md)函数。 您的源代码管理插件可能不支持外部程序，因此你可能想要禁用或甚至隐藏**启动**菜单选项。

      **DisableSccManager**是一个 DWORD 值并将设置为*0*若要启用**启动\<源代码管理服务器 >** 菜单选项，将设置为*1*到禁用的菜单选项，并将设置为*2*隐藏菜单选项。 如果未显示此注册表项，默认行为是显示菜单选项。

   | 示例注册表项 | 示例值 |
   | - |--------------|
   | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio | 1 |
   | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\DisableSccManager | 1 |

3. 添加子项**SourceCodeControlProvider**下**HKEY_LOCAL_MACHINE**中的键**软件**子项。

    此子项的注册表项下**ProviderRegKey**设置为一个字符串，表示放在步骤 1 中在注册表中的子项。 模式是**HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey** = *软件\\< 公司名称\>\\< 产品名称\>* .

    下面是此子项的示例内容。

   |注册表项|示例值|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > 您的源代码管理插件将使用相同的子项和项的名称，但将不同的值。

4. 创建名为子项**InstalledSCCProviders**下**SourceCodeControlProvider**子项，并且然后放入该子项下的一个条目。

    此项的名称为提供程序 （与相同 SCCServerName 条目为指定的值），用户可读名称，值为再次重申，步骤 1 中创建的子项。 模式是**HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\\< 显示名称\>**  = *软件\\< 公司名称\>\\< 产品名称\>* 。

    例如：

   |示例注册表项|示例值|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > 可以有多个源控制插件在这种方式中注册。 这是如何[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]查找所有已安装的基于源控制插件 API 的插件。

## <a name="how-an-ide-locates-the-dll"></a>IDE 如何定位 DLL
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 提供两种方法可以查找源控制插件 DLL:

- 查找默认的源代码管理插件，并以无提示方式连接到它。

- 查找所有已注册的源控制插件，从中可以选择一个。

  要在第一种方法中查找该 DLL，IDE 将查找下**HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider**子项的项**ProviderRegKey**。 此项的值将指向另一个子项。 IDE 将然后查找名为的条目**SccServerPath**中的第二个子项下**HKEY_LOCAL_MACHINE**。 此项的值指向该 DLL 的 IDE。

> [!NOTE]
> IDE 不会从相对路径加载 Dll (例如， *.\NewProvider.DLL*)。 必须指定 DLL 的完整路径 (例如， *c:\Providers\NewProvider.DLL*)。 这可通过阻止未经授权或模拟插件 Dll 加载增强安全性的 IDE。

 要在第二种方法中查找该 DLL，IDE 将查找下**HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider\InstalledSCCProviders**子项的所有项。 每个项包含一个名称和值。 IDE 将向用户显示这些名称的列表。 当用户选择一个名称时，IDE 将查找指向一个子项的所选名称的值。 IDE 将查找名为的条目**SccServerPath**下的子项中**HKEY_LOCAL_MACHINE**。 该条目的值指向正确的 DLL 的 IDE。

 源代码管理插件必须支持这两种查找 DLL，并因此，设置**ProviderRegKey**，覆盖任何以前的设置。 更重要的是，它必须将自身添加到的列表**InstalledSccProviders**因此，用户可以选择的源代码管理插件，以使用。

> [!NOTE]
> 因为**HKEY_LOCAL_MACHINE**只有一个源代码管理插件可以注册为默认的源代码管理插件在给定计算机上，使用密钥 (但是，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用户能够确定哪些源代码管理插件他们想要实际用于特定的解决方案）。 在安装过程中，检查以查看是否已设置源代码管理插件;如果是这样，，询问用户要设置新的源代码管理插件安装为默认值。 在卸载，请不要删除通用的所有源代码控制插件在其他注册表子项**HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider**; 仅在特定的 SCC 子项中删除。

## <a name="how-the-ide-detects-version-1213-support"></a>IDE 如何检测版本 1.2/1.3 支持
 如何 does[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]检测是否插件支持源控制插件 API 版本 1.2 和 1.3 功能？ 若要声明高级的功能，源代码管理插件必须实现相应的函数：

 首先，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]检查通过调用返回的值[SccGetVersion](../../extensibility/sccgetversion-function.md)。 它必须大于或等于 1.2。

 下一步，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]确定是否将特定的新功能支持通过检查`lpSccCaps`上的参数[SccInitialize](../../extensibility/sccinitialize-function.md)。

 如果满足这两个条件，可以调用在版本 1.2 和 1.3 中支持的新函数。

## <a name="see-also"></a>请参阅
- [开始使用源代码管理插件](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)