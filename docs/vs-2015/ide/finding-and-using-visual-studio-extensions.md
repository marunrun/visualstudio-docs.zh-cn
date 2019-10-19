---
title: 查找和使用扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.ExtensionManager
helpviewer_keywords:
- install extensions
- install packages
- managing extensions visual studio
ms.assetid: 4ca92d93-31b9-47ef-8109-4a429d9e2ca3
caps.latest.revision: 47
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: df6219a66b0f6c85e197b209741706abc7ce3d06
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655877"
---
# <a name="finding-and-using-visual-studio-extensions"></a>查找和使用 Visual Studio 扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 扩展是在 Visual Studio 内运行的代码包，并且提供了新的或者改进后的 Visual Studio 功能。 你可以在此处找到有关 Visual Studio 扩展的详细信息： [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

 你可以使用 **“扩展和更新”** 对话框安装来自网站或其他位置的 Visual Studio 扩展及示例，然后启用、禁用、更新或卸载这些扩展和示例。 （“工具”/“扩展和更新”，或在“快速启动” 窗口中输入 **扩展** ）。 该对话框还显示用于已安装的示例和扩展的更新。 还可以从网站下载扩展，或从其他开发人员处获取它们。

> [!NOTE]
> 从 Visual Studio 2015 开始，Visual Studio 库上托管的扩展将自动更新。  可以通过 **“扩展和更新”** 对话框更改此设置。  请参阅下面的 **“自动扩展更新”** 部分了解详细信息。

## <a name="finding-visual-studio-extensions"></a>查找 Visual Studio 扩展
 你可以从 Microsoft 网站上的[Visual Studio Marketplace](https://marketplace.visualstudio.com/)或[示例库](https://code.msdn.microsoft.com/vstudio)中安装扩展。 这些扩展可以是控件、示例、模板、工具或其他组件，用于向 Visual Studio 添加功能。 Visual Studio 支持 VSIX 包格式的扩展，其中包括项目模板、项模板、 **工具箱** 项、托管扩展框架 (MEF) 组件和 VSPackage。 还可以下载和安装基于 MSI 的扩展，但是无法通过 **“扩展和更新”** 对话框启用或禁用它们。 Visual Studio 库包含 VSIX 和 MSI 扩展。

## <a name="installing-or-uninstalling-visual-studio-extensions"></a>安装或卸载 Visual Studio 扩展
 在 **“扩展和更新”** 中，找到要安装的扩展。 （如果知道扩展的名称或部分名称，则可以在 "**搜索 Visual Studio 库**" 窗口中进行搜索。）单击 "**下载**"，然后单击 "**安装**"。 必须重新启动 Visual Studio 才能加载扩展。

 如果尝试安装具有依赖项的扩展，安装程序将验证它们是否已安装。 如果未安装，则 **“扩展和更新”** 对话框将列出安装该扩展之前必须先安装的依赖项。

 如果要停止使用一个扩展，你可以将其禁用或卸载。 禁用扩展是使扩展保持安装状态，但不加载。 只能禁用 VSIX 扩展；使用 MSI 安装的扩展只能进行卸载。 找到扩展，然后单击 **“卸载”** 或 **“禁用”** 。 必须重新启动 Visual Studio 才能卸载禁用的扩展。

## <a name="per-user-and-administrative-extensions"></a>每用户扩展和管理扩展
 大多数扩展都是每用户扩展，安装在 **%LocalAppData%\Microsoft\VisualStudio\\<Visual Studio version\>\Extensions\\** 文件夹中。 有几个扩展是管理扩展，安装在 **\<Visual Studio 安装文件夹>\Common7\IDE\Extensions\\** 文件夹中。

 若要针对可能包含错误或恶意代码的扩展保护你的系统，可以限制每用户扩展，以便只在使用正常用户权限运行 Visual Studio 时加载。 这意味着在使用管理用户权限运行 Visual Studio 时禁用每用户扩展。 若要执行此操作，请转到“扩展和更新” 选项页（“工具”/“选项”、“环境”、“扩展和更新”，或仅仅在“快速启动” 窗口中输入 **扩展** ）。 清除 **“以管理员身份运行时加载每用户扩展”** 复选框，然后重新启动 Visual Studio。

## <a name="automatic-extension-updates"></a>“自动扩展更新”
 当 Visual Studio 库里有可用的新版本时，每用户扩展将自动更新。  已检测到新版扩展并在后台进行安装，下次重启 Visual Studio 时将运行该新版扩展。

 仅每用户扩展可自动更新。  将不会更新为所有用户安装的管理扩展，仍通过 **“扩展和更新”** 对话框的 **“更新”** 节点手动安装新版本。 可以从 **“扩展和更新”** 对话框中的扩展详细信息窗格中看到哪些扩展将自动更新。

 若要禁用自动更新，可为所有扩展或仅特定扩展禁用该功能。

- 若要为所有扩展禁用自动更新，请单击 **“扩展和更新”** 对话框上的 **“更改扩展和更新设置”** 链接，并取消选中 **“自动更新扩展”** 。

- 若要为特定扩展禁用自动更新，请取消选中 **“扩展和更新”** 对话框右侧的扩展详细信息窗格中的 **“自动更新此扩展插件”** 选项。

> [!NOTE]
> 从 Visual Studio 2015 Update 2 开始，可以指定（在“工具”/“选项”/“环境”/“扩展和更新”中）是否需要为每用户扩展、所有用户扩展或两者（默认设置）进行自动更新。

## <a name="sample-master-copies-and-working-copies"></a>主控副本和工作副本示例
 安装联机示例时，解决方案存储在两个位置：

- 工作副本存储在你在 **“新建项目”** 对话框中指定的位置。

- 你的计算机上存储一个单独的主控副本。

  你可以使用 **“扩展和更新”** 对话框来执行这些与示例相关的任务：

- 列出已安装示例的主控副本。

- 禁用或卸载示例的主控副本。

- 安装示例包，示例包是与技术或功能相关的一系列示例的集合。

- 安装个别联机示例。 （你也可以在 **“新建项目”** 对话框中执行此操作。）

- 当发布已安装示例的源代码更改时，查看更新通知。

- 当存在更新通知时，更新已安装示例的主控副本。

## <a name="installing-without-using-the-extensions-and-updates-dialog-box"></a>不使用“扩展和更新”对话框进行安装
 可在 Visual Studio 库以外的位置获取已打包在 .vsix 文件中的扩展。 “扩展和更新” 对话框无法检测到这些文件，但你可以通过双击该文件，或者选择文件并按下 ENTER 键来安装 .vsix 文件。 此后，只需按照说明操作。 当扩展安装完成后，可以使用 **“扩展和更新”** 对话框启用、禁用或卸载此扩展。

## <a name="extension-types-not-supported-by-the-extensions-and-updates-dialog-box"></a>“扩展和更新”对话框不支持的扩展类型
 Visual Studio 会继续在无需修改的情况下，支持由 Microsoft 安装程序 (MSI) 安装、而不是通过 **“扩展和更新”** 对话框安装的扩展。

> [!TIP]
> 如果基于 MSI 的扩展包含 extension.vsixmanifest 文件，则扩展会出现在 **“扩展和更新”** 对话框中。
