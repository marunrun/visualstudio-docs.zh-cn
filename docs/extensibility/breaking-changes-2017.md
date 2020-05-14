---
title: 视觉工作室 2017 扩展性的突发变化
titleSuffix: ''
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b3a04c925ef897171de51c73c90973a12c3b17d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739970"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Visual Studio 2017 扩展性的变化

Visual Studio 2017 提供了[更快、更轻巧的 Visual Studio 安装体验](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer)，减少了 Visual Studio 对用户系统的影响，同时为用户提供了对已安装工作负载和功能的更多选择。 为了支持这些改进，我们对扩展性模型进行了更改，包括一些重大更改。 本文介绍了这些更改的技术细节，以及可以采取哪些措施来解决这些问题。

> [!NOTE]
> 某些信息是时间点实现详细信息，以后可能会更改。

## <a name="changes-affecting-vsix-format-and-installation"></a>影响 VSIX 格式和安装的更改

Visual Studio 2017 引入了 VSIX v3（版本 3）格式，以支持轻量级安装体验。

对 VSIX 格式的更改包括：

* 设置先决条件声明。 为了兑现轻巧、快速安装的 Visual Studio 的承诺，安装程序现在为用户提供了更多的配置选项。 因此，为了确保安装扩展所需的功能和组件，扩展需要声明其依赖项。

  * Visual Studio 2017 安装程序自动提供为用户获取和安装必要的组件，作为安装扩展的一部分。
  * 尝试安装未使用新的 VSIX v3 格式构建的扩展时，即使用户在其清单中标记为目标版本 15.0，也会收到警告。

* VSIX 格式的增强功能。 为了提供同样支持并行安装的 Visual Studio[的低影响安装](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install)，我们不再将大多数配置数据保存到系统注册表，并且将特定于 Visual Studio 的程序集移出 GAC。 我们还增加了 VSIX 格式和 VSIX 安装引擎的功能，允许您使用它，而不是 MSI 或 EXE 来安装某些安装类型的扩展。

新功能包括：

* 注册到指定的可视化工作室实例。
* 在[扩展文件夹之外安装](set-install-root.md)。
* 检测处理器架构。
* 依赖于语言分离的语言包。
* 安装与[NGEN支持](ngen-support.md)。

## <a name="build-an-extension-for-visual-studio-2017"></a>为 2017 年可视化工作室构建扩展

用于创作新的 VSIX v3 清单格式的设计器工具可在 Visual Studio 2017 中使用。 有关使用设计器工具或对项目和清单进行手动更新以开发 VSIX v3 扩展的详细信息，请参阅随附的文档[：将扩展性项目迁移到 Visual Studio 2017。](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)

## <a name="change-visual-studio-user-data-path"></a>更改：可视化工作室用户数据路径

以前，每台计算机上只能安装一个 Visual Studio 的每个主要版本。 为了支持 Visual Studio 2017 的并行安装，Visual Studio 的多个用户数据路径可能存在于用户的计算机上。

应在可视化工作室进程内运行的代码更新为使用可视化工作室设置管理器。 运行在 Visual Studio 进程之外的代码可以[按照此处的指导](locating-visual-studio.md)找到特定 Visual Studio 安装的用户路径。

## <a name="change-global-assembly-cache-gac"></a>更改：全局程序集缓存 （GAC）

大多数 Visual Studio 核心组件不再安装到 GAC 中。 进行了以下更改，以便在 Visual Studio 进程中运行的代码在运行时仍可以找到所需的程序集。

> [!NOTE]
> [INSTALLDIR] 下面是指可视化工作室的安装根目录。 *VSIXInstaller.exe*将自动填充此内容，但要编写自定义部署代码，请阅读[定位 Visual Studio](locating-visual-studio.md)。

* 仅安装到 GAC 中的程序集：

  这些程序集现在安装在<em>[INSTALLDIR]_Common7_IDE、[INSTALLDIR]_\*公共程序集</em>或 *[INSTALLDIR]_通用7_IDE_私有程序集*下。 这些文件夹是可视化工作室进程探测路径的一部分。

* 安装在非探测路径和 GAC 中的程序集：

  * GAC 中的副本从设置中删除。
  * 添加了 *.pkgdef*文件以指定程序集的代码基条目。

    例如：

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    在运行时，Visual Studio pkgdef 子系统将这些条目合并到 Visual Studio 进程的运行时配置文件（*在 [VSAPPDATA]_devenv.exe.config*下）作为[`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element)元素。 这是让 Visual Studio 进程找到程序集的推荐方法，因为它可以避免通过探测路径进行搜索。

### <a name="reacting-to-this-breaking-change"></a>应对这一重大变革

* 如果您的扩展在可视化工作室进程中运行：

  * 您的代码将能够找到 Visual Studio 核心程序集。
  * 如有必要，请考虑使用 *.pkgdef*文件指定程序集的路径。

* 如果您的扩展在可视化工作室进程之外运行：

  请考虑在<em>[INSTALLDIR]_Common7_IDE\*下查找 Visual Studio 核心程序集，[INSTALLDIR]_公共程序集\IDE_公共程序集</em>或 *[INSTALLDIR]\通用7_IDE_使用*配置文件或程序集解析器的私有程序集。

## <a name="change-reduce-registry-impact"></a>更改：减少注册表影响

### <a name="global-com-registration"></a>全球注册注册

* 以前，Visual Studio 在HKEY_CLASSES_ROOT中安装了许多注册表项，HKEY_LOCAL_MACHINE配置单元以支持本机 COM 注册。 为了消除这种影响，Visual Studio 现在使用[COM 组件的无注册激活](https://msdn.microsoft.com/library/ms973913.aspx)。
* 因此，在 %程序文件 （x86）%%%下的大多数 TLB / OLB / DLL 文件都不再默认由 Visual Studio 安装。 这些文件现在安装在 [INSTALLDIR] 下，与 Visual Studio 主机进程使用的相应无注册 COM 清单一起安装。
* 因此，依赖于 Visual Studio COM 接口的全局 COM 注册的外部代码将不再找到这些注册。 在 Visual Studio 进程内运行的代码不会看到差异。

### <a name="visual-studio-registry"></a>视觉工作室注册表

* 以前，Visual Studio 在系统的**HKEY_LOCAL_MACHINE**中安装了许多注册表项，并在特定于 Visual Studio 的密钥下**HKEY_CURRENT_USER**配置单元：

  * **HKLM_软件[微软]VisualStudio\{版本*：** 由 MSI 安装程序和每台计算机扩展创建的注册表项。
  * **HKCU_软件[微软]VisualStudio\{版本*：Visual**Studio 创建的注册表项，用于存储特定于用户的设置。
  * **HKCU_软件[微软]VisualStudio\{版本]_Config：** 上面的 Visual Studio HKLM 密钥的副本，以及按扩展名从 *.pkgdef*文件合并的注册表项。

* 为了减少对注册表的影响，Visual Studio 现在使用[RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya)函数在 *[VSAPPDATA]\privateregistry.bin*下将注册表项存储在私有二进制文件中。 系统注册表中仅保留极少数特定于 Visual Studio 的密钥。
* 在可视化工作室进程内运行的现有代码不受影响。 Visual Studio 会将 HKCU 视觉工作室特定密钥下的所有注册表操作重定向到专用注册表。 读取和写入其他注册表位置将继续使用系统注册表。
* 外部代码将需要加载和读取此文件为 Visual Studio 注册表条目。

### <a name="react-to-this-breaking-change"></a>应对这一重大变革

* 外部代码也应转换为对 COM 组件使用无注册激活。
* 外部组件可以[按照此处的指导](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup)找到 Visual Studio 位置。
* 我们建议外部组件使用[外部设置管理器](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager)，而不是直接读取/写入 Visual Studio 注册表项。
* 检查扩展正在使用的组件是否实现了另一种注册技术。 例如，调试器扩展可能能够利用新的[msvsmon JSON 文件 COM 注册](migrate-debugger-COM-registration.md)。
