---
title: 查找和使用扩展
ms.date: 01/30/2019
ms.topic: conceptual
f1_keywords:
- vs.ExtensionManager
helpviewer_keywords:
- install extensions
- install packages
- managing extensions visual studio
ms.assetid: 4ca92d93-31b9-47ef-8109-4a429d9e2ca3
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ca0b1defbec345acc02212498453972a3576f20
ms.sourcegitcommit: 0ef51e3517436a85cfb85bf492722d566ce602c4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65934348"
---
# <a name="find-and-use-visual-studio-extensions"></a>查找和使用 Visual Studio 扩展

Visual Studio 扩展是在 Visual Studio 内运行的代码包，并且提供了新的或者改进后的 Visual Studio 功能。 可以在此处找到有关 Visual Studio 扩展的详细信息：[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

::: moniker range="vs-2017"

使用“扩展和更新”对话框来安装和管理 Visual Studio 扩展。 若要打开“扩展和更新”对话框，请选择“工具” > “扩展和更新”，或在“快速启动”搜索框中键入“扩展”。

::: moniker-end

::: moniker range=">=vs-2019"

使用“管理扩展”对话框来安装和管理 Visual Studio 扩展。 若要打开“管理扩展”对话框，请选择“扩展” > “管理扩展”。 或者，在搜索框中键入“扩展”，然后选择“管理扩展”。

::: moniker-end

![Visual Studio 中的“扩展”窗口](media/finding-using-visual-studio-extensions/extensions-and-updates.png)

左侧窗格按照已安装的扩展、Visual Studio Marketplace（联机）上提供的扩展以及有可用更新的扩展对扩展进行分类。 漫游扩展管理器会保留已在 Visual Studio 的任何计算机或实例上安装的所有 Visual Studio 扩展的列表。 它旨在让你更轻松地找到自己喜欢的扩展程序。

## <a name="find-visual-studio-extensions"></a>查找 Visual Studio 扩展

可以安装来自 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) 的扩展。 这些扩展可以是控件、示例、模板、工具或其他组件，用于向 Visual Studio 添加功能。 Visual Studio 支持 VSIX 包格式的扩展，其中包括项目模板、项模板、 **工具箱** 项、托管扩展框架 (MEF) 组件和 VSPackage。

::: moniker range="vs-2017"

还可以下载和安装基于 MSI 的扩展，但是无法通过 **“扩展和更新”** 对话框启用或禁用它们。 Visual Studio Marketplace 包含 VSIX 和 MSI 扩展。

::: moniker-end

::: moniker range=">=vs-2019"

还可以下载和安装基于 MSI 的扩展，但是无法通过“管理扩展”对话框启用或禁用它们。 Visual Studio Marketplace 包含 VSIX 和 MSI 扩展。

::: moniker-end

## <a name="install-or-uninstall-visual-studio-extensions"></a>安装或卸载 Visual Studio 扩展

::: moniker range="vs-2017"

在“工具” > “扩展和更新”中，找到要安装的扩展。 （如果知道扩展的名称或部分名称，则可以在“搜索”窗口中进行搜索。）单击“下载”。 按计划安装扩展。 等所有 Visual Studio 实例都关闭后便会安装扩展。

如果尝试安装具有依赖项的扩展，安装程序将验证它们是否已安装。 如果未安装，则 **“扩展和更新”** 对话框将列出安装该扩展之前必须先安装的依赖项。

::: moniker-end

::: moniker range=">=vs-2019"

在“扩展” > “管理扩展”中，找到要安装的扩展。 （如果知道扩展的名称或部分名称，则可以在“搜索”窗口中进行搜索。）单击“下载”。 按计划安装扩展。 等所有 Visual Studio 实例都关闭后便会安装扩展。

如果尝试安装具有依赖项的扩展，安装程序将验证它们是否已安装。 如果未安装，则“管理扩展”对话框将列出安装该扩展之前必须先安装的依赖项。

::: moniker-end

如果要停止使用一个扩展，你可以将其禁用或卸载。 禁用扩展是使扩展保持安装状态，但不加载。 只能禁用 VSIX 扩展；使用 MSI 安装的扩展只能进行卸载。 找到扩展，然后单击 **“卸载”** 或 **“禁用”** 。 重新启动 Visual Studio 以卸载禁用的扩展。

## <a name="per-user-and-administrative-extensions"></a>每用户扩展和管理扩展

大多数扩展都是每用户扩展，安装在 *%LocalAppData%\Microsoft\VisualStudio\\<Visual Studio version\>\Extensions\\* 文件夹中。 有几个扩展是管理扩展，安装在 *\<Visual Studio 安装文件夹>\Common7\IDE\Extensions\\* 文件夹中。

若要针对可能包含错误或恶意代码的扩展保护你的系统，可以限制每用户扩展，以便只在使用正常用户权限运行 Visual Studio 时加载。 这意味着在使用管理用户权限运行 Visual Studio 时禁用每用户扩展。 若要执行此操作，请转到扩展选项页（“工具” > “选项” > “环境” > “扩展”）。 清除 **“以管理员身份运行时加载每用户扩展”** 复选框，然后重新启动 Visual Studio。

## <a name="automatic-extension-updates"></a>自动扩展更新

Visual Studio Marketplace 中有可用的新版本时，将自动更新扩展。 检测到扩展的新版本并已在后台安装。 下次打开 Visual Studio 时，将运行该扩展的新版本。

若要禁用自动更新，可为所有扩展或仅特定扩展禁用该功能。

::: moniker range="vs-2017"

- 若要为所有扩展禁用自动更新，请选择“工具” > “扩展和更新”对话框中的“更改扩展和更新设置”链接。 在“选项”对话框中，取消选中“自动更新扩展”。

- 若要为特定扩展禁用自动更新，请取消选中“扩展和更新”对话框右侧的扩展细节窗格中的“自动更新此扩展”选项。

::: moniker-end

::: moniker range=">=vs-2019"

- 若要为所有扩展禁用自动更新，请选择“扩展” > “管理扩展”对话框中的“更改扩展的设置”链接。 在“选项”对话框中，取消选中“自动更新扩展”。

- 若要为特定扩展禁用自动更新，请取消选中“管理扩展”对话框右侧的扩展详细信息窗格中的“自动更新此扩展”选项。

::: moniker-end

## <a name="extension-crash-and-unresponsiveness-notifications"></a>扩展崩溃和无响应通知

如果 Visual Studio 怀疑扩展已在之前的会话期间发生故障，将会发出通知。 Visual Studio 发生故障时，会存储异常堆栈。 下一次 Visual Studio 启动时，它会检查堆栈，同时开始处理叶和构建基础映像。 如果 Visual Studio 确定框架所属的模块属于已安装和已启用的扩展，它将显示一条通知。

如果 Visual Studio 怀疑某个扩展导致 UI 无响应，也会发出通知。

显示这些通知时，可以忽略它们，或者可以执行以下任一操作：

::: moniker range="vs-2017"

- 选择“禁用此扩展”。 Visual Studio 会禁用扩展，并告知是否需要重启系统才能使禁用生效。 如果需要，可以在“工具” > “扩展和更新”对话框中重新启用扩展。

::: moniker-end

::: moniker range=">=vs-2019"

- 选择“禁用此扩展”。 Visual Studio 会禁用扩展，并告知是否需要重启系统才能使禁用生效。 如果需要，可以在“扩展” > “管理扩展”对话框中重新启用扩展。

::: moniker-end

- 选择“不再显示此消息”。

  - 如果通知与以前会话中的故障有关，则在出现与该扩展相关联的故障时，Visual Studio 将不再显示通知。 当无响应可与该扩展相关联，或对于可与其他扩展相关联的故障或无响应，Visual Studio 仍将显示通知。
  - 如果通知与无响应有关，则当该扩展与无响应相关联时，IDE 将不再显示通知。 Visual Studio 仍会显示与该扩展相关的故障通知，以及其他扩展与故障和无响应相关的通知。

- 选择“了解详细信息”以转到此页。

- 选择通知末尾的“X”按钮可以取消通知。 对于以后与故障或 UI 无响应相关联的扩展实例将会显示新通知。

> [!NOTE]
> UI 无响应或故障通知意味着当 UI 无响应或出现故障时，只有其中一个扩展模块在堆栈上， 但它并不一定意味着是扩展本身所导致的。 它可能是扩展所调用的代码是 Visual Studio 的一部分，进而导致 UI 无响应或崩溃。 但是，如果导致 UI 无响应或崩溃的扩展对你不重要，那么通知还是有用的。 在这种情况下，禁用该扩展可避免将来 UI 无响应或发生故障，而不会影响工作效率。

## <a name="sample-master-copies-and-working-copies"></a>主控副本和工作副本示例

安装联机示例时，解决方案存储在两个位置：

- 工作副本存储在创建项目时指定的位置。

- 你的计算机上存储一个单独的主控副本。

::: moniker range="vs-2017"

你可以使用“工具”>“扩展和更新”对话框来执行这些与示例相关的任务：

::: moniker-end

::: moniker range=">=vs-2019"

你可以使用“扩展”>“管理扩展”对话框来执行这些与示例相关的任务：

::: moniker-end

- 列出已安装示例的主控副本。

- 禁用或卸载示例的主控副本。

- 安装示例包，示例包是与技术或功能相关的一系列示例的集合。

- 安装个别联机示例。

- 当发布已安装示例的源代码更改时，查看更新通知。

- 当存在更新通知时，更新已安装示例的主控副本。

::: moniker range="vs-2017"

## <a name="install-without-using-the-extensions-and-updates-dialog-box"></a>不使用“扩展和更新”对话框进行安装

可在 Visual Studio Marketplace 以外的位置获取已打包在 .vsix 文件中的扩展。 “工具” > “扩展和更新”对话框无法检测到这些文件，但可通过双击该文件，或者选择文件并按下 Enter 键来安装 .vsix 文件。 此后，只需按照说明操作。 当扩展安装完成后，可以使用 **“扩展和更新”** 对话框启用、禁用或卸载此扩展。

## <a name="extension-types-not-supported-by-the-extensions-and-updates-dialog-box"></a>“扩展和更新”对话框不支持的扩展类型

Visual Studio 会继续在无需修改的情况下，支持由 Microsoft 安装程序 (MSI) 安装、而不是通过“工具”>“扩展和更新”对话框安装的扩展。

> [!TIP]
> 如果基于 MSI 的扩展包含 extension.vsixmanifest 文件，则该扩展会出现在“扩展和更新”对话框中。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="install-without-using-the-manage-extensions-dialog-box"></a>不使用“管理扩展”对话框进行安装

可在 Visual Studio Marketplace 以外的位置获取已打包在 .vsix 文件中的扩展。 “扩展” > “管理扩展”对话框无法检测到这些文件，但可通过双击该文件，或者选择文件并按下 Enter 键来安装 .vsix 文件。 此后，只需按照说明操作。 当扩展安装完成后，可以使用“管理扩展”对话框启用、禁用或卸载此扩展。

## <a name="extension-types-not-supported-by-the-manage-extensions-dialog-box"></a>“管理扩展”对话框不支持的扩展类型

Visual Studio 会继续在无需修改的情况下，支持由 Microsoft 安装程序 (MSI) 安装、而不是通过“扩展”>“管理扩展”对话框安装的扩展。

> [!TIP]
> 如果基于 MSI 的扩展包含 extension.vsixmanifest 文件，则该扩展会出现在“管理扩展”对话框中。

::: moniker-end