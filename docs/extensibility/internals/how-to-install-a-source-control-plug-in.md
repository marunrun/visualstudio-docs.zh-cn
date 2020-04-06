---
title: 如何：安装源代码管理插件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c0ac87aec3d6ac2532909772238e020e33bf78f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707992"
---
# <a name="how-to-install-a-source-control-plug-in"></a>如何：安装源代码管理插件
创建源代码管理插件包括三个步骤：

1. 使用本文档的源代码管理插件 API 引用部分中定义的函数创建 DLL。

2. 实现源代码管理插件 API 定义的功能。 调用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时，使接口和对话框可从插件。

3. 通过进行适当的注册表项来注册 DLL。

## <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持符合源代码管理插件 API 的源代码管理插件。

### <a name="register-the-source-control-plug-in"></a>注册源代码管理插件
 在正在运行的集成开发环境 （IDE） 可以调用源代码管理系统之前，必须首先找到导出 API 的源代码管理插件 DLL。

#### <a name="to-register-the-source-control-plug-in-dll"></a>注册源代码管理插件 DLL

1. 在 **"软件"** 子键中**HKEY_LOCAL_MACHINE**键下添加两个条目，该键指定公司名称子键后跟产品名称子键。 该模式是**HKEY_LOCAL_MACHINE_软件\\\<公司名称>\\\<产品名称>\\\<条目>** = *值*。 这两个条目始终称为**SCCServer 名称**和**SCCServerPath**。 每个字符串都是常规字符串。

    例如，如果您的公司名称是 Microsoft，并且源代码管理产品名为 SourceSafe，则此注册表路径将为**HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_SourceSafe**。 在此子键中，第一个条目**SCCServerName**是用户可读的字符串，用于命名您的产品。 第二个条目**SCCServerPath**是 IDE 应连接到的源代码管理插件 DLL 的完整路径。 下面提供了示例注册表项：

   |示例注册表条目|示例值|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE_SOFTWARE_微软\来源安全\SCCServer名称|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE_SOFTWARE_微软\来源安全\SCCServer路径|*c：\vss_win32_sscc.dll*|

   > [!NOTE]
   > SCCServerPath 是源安全插件的完整路径。 源代码管理插件将使用不同的公司和产品名称，但相同的注册表输入路径。

2. 以下可选注册表项可用于修改源代码管理插件的行为。 这些条目与**SccServerName**和**SccServerPath**位于同一个子键中。

   - 如果您不希望源代码管理插件出现在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的**插件选择**列表中，可以使用**HideInVisualStudio 注册表**。 此条目还将影响自动切换到源代码管理插件。 此项的一个可能用途是，如果提供一个源代码管理包，以替换源代码管理插件，但您希望使用户更容易从使用源代码管理插件迁移到源代码管理包。 安装源代码管理包时，它会设置此注册表项，该注册表项将隐藏插件。

      **HideInVisualStudio**是一个 DWORD 值，设置为*1*以隐藏插件或*0*以显示插件。 如果未显示注册表项，则默认行为是显示插件。

   - **"禁用SccManager**注册表"可用于禁用或隐藏启动**\<源控制服务器>** 菜单选项，该菜单通常出现在 **"文件** > **源控制"** 子菜单下。 选择此菜单选项将调用[SccRunScc](../../extensibility/sccrunscc-function.md)函数。 源代码管理插件可能不支持外部程序，因此您可能需要禁用甚至隐藏 **"启动"** 菜单选项。

      **禁用SccManager**是一个 DWORD 值，设置为*0*以启用**启动\<源控制服务器>** 菜单选项，设置为*1*以禁用菜单选项，并设置为*2*以隐藏菜单选项。 如果未显示此注册表项，则默认行为是显示菜单选项。

   | 示例注册表项 | 示例值 |
   | - |--------------|
   | HKEY_LOCAL_MACHINE_SOFTWARE_微软_来源安全_隐藏视觉工作室 | 1 |
   | HKEY_LOCAL_MACHINE_SOFTWARE_微软\来源安全\禁用Scc管理器 | 1 |

3. 在**软件**子键中**HKEY_LOCAL_MACHINE**键下添加子键 **"源代码控制提供程序**"。

    在此子键下，注册表项**提供程序 RegKey**设置为一个字符串，该字符串表示您在步骤 1 中放置在注册表中的子键。 模式是**HKEY_LOCAL_MACHINE_SOFTWARE_源代码控制提供商\提供商RegKey** = *软件\\<公司名称\>\\<产品名称\>*。

    以下是此子键的示例内容。

   |注册表项|示例值|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE_SOFTWARE_源代码控制提供商\提供商雷吉|软件\微软\来源安全|

   > [!NOTE]
   > 源代码管理插件将使用相同的子键和条目名称，但值将不同。

4. 在**源代码管理提供程序**子键下创建名为 **"已安装SCC提供程序"** 的子键，然后将一个条目放在该子键下。

    此条目的名称是提供程序的用户可读名称（与为 SCCServerName 条目指定的值相同），该值再次成为步骤 1 中创建的子键。 模式是**HKEY_LOCAL_MACHINE_SOFTWARE_源代码控制提供程序\已安装SCC\\提供商<显示名称\>***\\\>\\\>* = 软件<公司名称<产品名称。

    例如：

   |示例注册表项|示例值|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE_SOFTWARE_源代码控制提供程序\已安装SCC提供商\微软视觉源安全|软件\微软\来源安全|

   > [!NOTE]
   > 可以以这种方式注册多个源代码管理插件。 这是查找[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]所有已安装的基于 API 的源代码管理插件的方式。

## <a name="how-an-ide-locates-the-dll"></a>IDE 如何定位 DLL
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 有两种查找源代码管理插件 DLL 的方法：

- 查找默认源代码管理插件并静默连接到它。

- 查找用户从中选择一个的所有已注册的源代码管理插件。

  要以第一种方式定位 DLL，IDE 将查找条目**提供程序 RegKey****的HKEY_LOCAL_MACHINE\软件\源代码管理提供程序**子键下。 此条目的值指向另一个子键。 然后，IDE 在**HKEY_LOCAL_MACHINE**下的第二个子键中查找名为**SccServerPath**的条目。 此条目的值将 IDE 指向 DLL。

> [!NOTE]
> IDE 不会从相对路径加载 DLL（例如 *，._NewProvider.DLL*）。 必须指定 DLL 的完整路径（例如 *，c：\提供程序\NewProvider.DLL）。* 这通过防止加载未经授权的或模拟的插件 DLL 来增强 IDE 的安全性。

 要以第二种方式查找 DLL，IDE 会查找所有条目**的HKEY_LOCAL_MACHINE\软件\源代码管理提供程序\已安装SCCProviders**子键下。 每个条目都有一个名称和一个值。 IDE 向用户显示这些名称的列表。 当用户选择名称时，IDE 会查找指向子键的选定名称的值。 IDE 在**HKEY_LOCAL_MACHINE**下该子键中查找名为**SccServerPath**的条目。 该条目的值将 IDE 指向正确的 DLL。

 源代码管理插件需要支持找到 DLL 的方法，从而设置**提供程序 RegKey，** 覆盖任何以前的设置。 更重要的是，它必须将自己添加到**已安装 Scc 提供程序**列表中，以便用户可以选择要使用的源代码管理插件。

> [!NOTE]
> 由于使用了**HKEY_LOCAL_MACHINE**密钥，因此在给定计算机上只能将一个源代码管理插件注册为默认源代码管理插件（但是，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]允许用户确定要实际用于特定解决方案的源代码管理插件）。 在安装过程中，请检查是否设置了源代码管理插件;如果安装过程，请检查是否已设置源代码管理插件。如果是这样，请询问用户是否将安装的新源代码管理插件设置为默认值。 在卸载期间，不要删除**HKEY_LOCAL_MACHINE_SOFTWARE_SourceCodeControlProvider**; 中所有源代码插件所共有的其他注册表子键。仅删除您的特定 SCC 子密钥。

## <a name="how-the-ide-detects-version-1213-support"></a>IDE 如何检测版本 1.2/1.3 支持
 如何[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]检测插件是否支持源代码管理插件 API 版本 1.2 和 1.3 功能？ 要声明高级功能，源代码管理插件必须实现相应的功能：

 首先，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过调用[SccGetVersion](../../extensibility/sccgetversion-function.md)检查返回的值。 它必须大于或等于 1.2。

 接下来，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过检查`lpSccCaps`[Scc初始化](../../extensibility/sccinitialize-function.md)上的参数来确定是否支持特定的新功能。

 如果满足这两个条件，则可以调用版本 1.2 和 1.3 中支持的新功能。

## <a name="see-also"></a>请参阅
- [开始使用源代码管理插件](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
