---
title: 如何：安装源代码管理插件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f88e4781115fa7a5fac54826304ab32472eeefb
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905366"
---
# <a name="how-to-install-a-source-control-plug-in"></a>如何：安装源代码管理插件
创建源代码管理插件涉及三个步骤：

1. 使用本文档的 "源代码管理插件 API 参考" 部分中定义的函数创建一个 DLL。

2. 实现源代码管理插件 API 定义的函数。 当对 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 它进行调用时，请从插件提供接口和对话框。

3. 通过创建适当的注册表项来注册 DLL。

## <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持符合源代码管理插件 API 的源代码管理插件。

### <a name="register-the-source-control-plug-in"></a>注册源代码管理插件
 在运行的集成开发环境（IDE）可以调入源代码管理系统之前，它必须首先查找导出 API 的源代码管理插件 DLL。

#### <a name="to-register-the-source-control-plug-in-dll"></a>注册源代码管理插件 DLL

1. 在指定你的公司名称子密钥后跟产品名称子项的**软件**子项中**HKEY_LOCAL_MACHINE** ，添加两个条目。 模式为**HKEY_LOCAL_MACHINE \\ \<company name> \\ \<product name> \software \\ 值 \<entry> **  =  *value*。 这两个条目始终称为**SCCServerName**和**SCCServerPath**。 每个都是一个常规字符串。

    例如，如果你的公司名称为 Microsoft，并且你的源代码管理产品名为 SourceSafe，则此注册表路径将**HKEY_LOCAL_MACHINE \software\microsoft\sourcesafe**中。 在此子项中，第一项**SCCServerName**是用户可读的用于命名产品的字符串。 第二个条目**SCCServerPath**是 IDE 应连接到的源代码管理插件 DLL 的完整路径。 下面提供了示例注册表项：

   |示例注册表项|示例值|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\SCCServerPath|*c:\vss\win32\ssscc.dll*|

   > [!NOTE]
   > SCCServerPath 是 SourceSafe 插件的完整路径。 源代码管理插件将使用不同的公司和产品名称，而不是相同的注册表项路径。

2. 以下可选的注册表项可用于修改源代码管理插件的行为。 这些项与**SccServerName**和**SccServerPath**位于同一子项中。

   - 如果你不希望源代码管理插件出现在的**插件选择**列表中，则可以使用**HideInVisualStudioregistry**项 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 此项还会影响自动切换到源代码管理插件。 此项的一种可能用途是，如果你提供了一个源代码管理包用于替换源代码管理插件，但你想要使用户更轻松地从使用源代码管理插件到源代码管理包的迁移。 在安装源代码管理包时，它将设置此注册表项，这将隐藏插件。

      **HideInVisualStudio**为 DWORD 值，设置为*1*以隐藏插件，或设置为*0*以显示插件。 如果注册表项未出现，则默认行为是显示插件。

   - **DisableSccManager**注册表项可用于禁用或隐藏通常显示在 " ** \<Source Control Server> ** **文件**  >  **源代码管理**" 子菜单下的 "启动" 菜单选项。 选择此菜单选项将调用[SccRunScc](../../extensibility/sccrunscc-function.md)函数。 你的源代码管理插件可能不支持外部程序，因此你可能想要禁用甚至隐藏 "**启动**" 菜单选项。

      **DisableSccManager**是一个 DWORD 值，设置为*0*时，将启用 **" \<Source Control Server> 启动**" 菜单选项，将设置为*1*可禁用菜单选项，并将设置为*2*以隐藏菜单选项。 如果此注册表项未出现，则默认行为是显示菜单选项。

   | 示例注册表项 | 示例值 |
   | - |--------------|
   | HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio | 1 |
   | HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\DisableSccManager | 1 |

3. 在**SOFTWARE**子项的**HKEY_LOCAL_MACHINE**项下添加子项**SourceCodeControlProvider**。

    在此子项下，注册表项**ProviderRegKey**设置为一个字符串，该字符串表示在步骤1中放置在注册表中的子项。 模式为**HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider\providerregkey**  =  *SOFTWARE \\<公司名称 \> \\<产品名称 \> *。

    下面是此子项的示例内容。

   |注册表项|示例值|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE \SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > 源代码管理插件将使用相同的子项和条目名称，但值会不同。

4. 在**SourceCodeControlProvider**子项下创建名为**InstalledSCCProviders**的子项，然后在该子项下放置一个条目。

    此项的名称是提供程序的用户可读名称（与为 SCCServerName 项指定的值相同），并且值也是在步骤1中创建的子项。 模式为**HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider\installedsccproviders \\<显示名称 \> **  =  *软件 \\<公司名称 \> \\<产品名称 \> *。

    例如：

   |示例注册表项|示例值|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE \SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > 可以通过这种方式注册多个源代码管理插件。 这就是如何 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 查找所有安装的源代码管理插件基于 API 的插件。

## <a name="how-an-ide-locates-the-dll"></a>IDE 如何查找 DLL
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 提供了两种方法来查找源代码管理插件 DLL：

- 查找默认的源代码管理插件，并以无提示方式连接到该插件。

- 查找所有已注册的源代码管理插件，用户从中选择一个插件。

  为了以第一种方式查找 DLL，IDE 将在 " **HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider** " 子项的**ProviderRegKey**项中查找。 此项的值指向另一个子项。 IDE 随后会在**HKEY_LOCAL_MACHINE**下的第二个子项中查找名为**SccServerPath**的条目。 此项的值将 IDE 指向 DLL。

> [!NOTE]
> IDE 不会从相对路径（例如 *.\NewProvider.DLL*）加载 dll。 必须指定 DLL 的完整路径（例如*c:\Providers\NewProvider.DLL*）。 这会阻止加载未经授权或模拟的插件 Dll，从而增强了 IDE 的安全性。

 若要以第二种方式查找 DLL，IDE 将在 " **HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider\installedsccproviders** " 子项的所有条目中查找。 每个项都有一个名称和一个值。 IDE 将向用户显示这些名称的列表。 当用户选择一个名称时，IDE 将查找指向子项的选定名称的值。 IDE 会在**HKEY_LOCAL_MACHINE**下的该子项中查找名为 " **SccServerPath** " 的条目。 该项的值将 IDE 指向正确的 DLL。

 源代码管理插件需要同时支持这两种方法来查找 DLL，进而设置**ProviderRegKey**，覆盖任何以前的设置。 更重要的是，它必须将自身添加到**InstalledSccProviders**列表，以便用户可以选择要使用的源代码管理插件。

> [!NOTE]
> 由于使用的是**HKEY_LOCAL_MACHINE**键，因此只有一个源代码管理插件可以注册为给定计算机上的默认源代码管理插件（不过， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用户可以使用它来确定要为特定解决方案实际使用的源代码管理插件）。 在安装过程中，请检查是否已设置源代码管理插件;如果是这样，请询问用户是否将新的源代码管理插件安装为默认值。 在卸载过程中，不要删除**HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider**中的所有源代码管理插件所共有的其他注册表子项。仅删除特定的 SCC 子项。

## <a name="how-the-ide-detects-version-1213-support"></a>IDE 如何检测版本 1.2/1.3 支持
 如何 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 检测插件是否支持源代码管理插件 API 版本1.2 和1.3 功能？ 若要声明高级功能，源代码管理插件必须实现相应的函数：

 首先， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 检查通过调用[SccGetVersion](../../extensibility/sccgetversion-function.md)返回的值。 它必须大于或等于1.2。

 接下来， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 通过检查 SccInitialize 的参数来确定是否支持特定的新功能 `lpSccCaps` 。 [SccInitialize](../../extensibility/sccinitialize-function.md)

 如果同时满足这两个条件，则可以调用版本1.2 和1.3 中支持的新函数。

## <a name="see-also"></a>另请参阅
- [源代码管理插件入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
