---
title: 安装 Visual Studio
titleSuffix: ''
description: 了解如何逐步安装 Visual Studio。
ms.date: 04/16/2019
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- vs.about
helpviewer_keywords:
- install Visual Studio
- dev15
- set up Visual Studio
- Visual Studio setup
- Visual Studio installer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 4833c6e8e1391028fbb034ff96967450d006356a
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263726"
---
# <a name="install-visual-studio"></a>安装 Visual Studio

::: moniker range="vs-2019"

欢迎使用 Visual Studio 2019！ 在此版本中，可轻松选择并仅安装所需功能。 并且由于其最小占用减小，因此其安装速度快且对系统的影响极小。

::: moniker-end

::: moniker range="vs-2017"

欢迎以全新方式安装 Visual Studio！ 在此版本中，可更轻松地选择并仅安装所需功能。 此外，我们还减少了 Visual Studio 的最小内存需求量，使其安装速度变得更快，对系统的影响更小。

::: moniker-end

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[安装 Visual Studio for Mac](/visualstudio/mac/installation/)。

::: moniker range="vs-2019"

想要详细了解此版本的其他新增功能？ 请参阅我们的[发行说明](/visualstudio/releases/2019/release-notes/)。

::: moniker-end

::: moniker range="vs-2017"

想要详细了解此版本的其他新增功能？ 请参阅我们的[发行说明](/visualstudio/releasenotes/vs2017-relnotes)。

::: moniker-end

准备安装？ 我们将逐步引导你完成安装。

## <a name="step-1---make-sure-your-computer-is-ready-for-visual-studio"></a>第 1 步 - 确保计算机支持 Visual Studio

开始安装 Visual Studio 前：

::: moniker range="vs-2017"

1. 查看[系统要求](/visualstudio/productinfo/vs2017-system-requirements-vs)。 这些要求有助于了解计算机是否支持 Visual Studio 2017。

1. 应用最新的 Windows 更新。 这些更新可确保计算机包含最新的安全更新程序和 Visual Studio 所需的系统组件。

1. 重新启动。 重新启动可确保挂起的任何安装或更新都不会影响 Visual Studio 安装。

1. 释放空间。 通过运行磁盘清理应用程序等方式，从 %SystemDrive% 删除不需要的文件和应用程序。

::: moniker-end

::: moniker range="vs-2019"

1. 查看[系统要求](/visualstudio/releases/2019/system-requirements)。 这些要求有助于了解计算机是否支持 Visual Studio 2019。

1. 应用最新的 Windows 更新。 这些更新可确保计算机包含最新的安全更新程序和 Visual Studio 所需的系统组件。

1. 重新启动。 重新启动可确保挂起的任何安装或更新都不会影响 Visual Studio 安装。

1. 释放空间。 通过运行磁盘清理应用程序等方式，从 %SystemDrive% 删除不需要的文件和应用程序。 

::: moniker-end

::: moniker range="vs-2017"

若对如何并行运行旧版 Visual Studio 和 Visual Studio 2017 有疑问，请参阅 [Visual Studio 兼容性详细信息](/visualstudio/productinfo/vs2017-compatibility-vs#compatibility-with-previous-releases)。

::: moniker-end

::: moniker range="vs-2019"

有关使用 Visual Studio 2019 并排运行 Visual Studio 先前版本的问题，请参阅 [Visual Studio 2019 平台目标和兼容性](/visualstudio/releases/2019/compatibility/)页面。

::: moniker-end

## <a name="step-2---download-visual-studio"></a>第 2 步 - 下载 Visual Studio

接下来，下载 Visual Studio 引导程序文件。 为此，请选择下面的按钮，选择所需的 Visual Studio 版本，选择“保存”，然后选择“打开文件夹”。

::: moniker range="vs-2017"

 > [!div class="button"]
 > [下载 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

 > [!div class="button"]
 > [下载 Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019)

::: moniker-end

## <a name="step-3---install-the-visual-studio-installer"></a>第 3 步 - `打开` Visual Studio 安装程序

运行引导程序文件以安装 Visual Studio 安装程序。 这个新的轻型安装程序包括安装和自定义 Visual Studio 所需的一切。

1. 在“下载”文件夹中，双击与下列文件之一匹配或类似的引导程序文件：

   * 对于 Visual Studio Community，请运行 **vs_community.exe**
   * 对于 Visual Studio Professional，请运行 **vs_professional.exe**
   * 对于 Visual Studio Enterprise，请运行 **vs_enterprise.exe**

   如果收到用户帐户控制通知，请选择“是”。

2. 我们会要求确认 Microsoft [许可条款](https://visualstudio.microsoft.com/license-terms/)和 Microsoft [隐私声明](https://privacy.microsoft.com/privacystatement)。 选择“继续”。

   ![许可条款和隐私声明](media/privacy-and-license-terms.png "Microsoft 许可条款和隐私声明")

## <a name="step-4---choose-workloads"></a>第 4 步 - 选择工作负载

安装该安装程序后，可以通过选择所需的功能集或工作负载来使用该程序自定义安装。 操作方法如下。

 ::: moniker range="vs-2017"

1. 在“安装 Visual Studio”屏幕中找到所需的工作负载。

   ![Visual Studio 2017：安装工作负载](../install/media/vs-installer-installing-workloads.png)

     例如，选择“.NET 桌面开发”工作负载。 它附带默认核心编辑器，该编辑器针对超过 20 种语言提供基本代码编辑支持，能够打开和编辑任意文件夹中的代码（而无需使用项目），还提供集成的源代码管理。

1. 选择所需的工作负载后，选择“安装”。

    接下来，会出现多个显示 Visual Studio 安装进度的状态屏幕。

 ::: moniker-end

::: moniker range="vs-2019"

1. 安装完新的工作负载和组件后，选择“启动”。

   ![Visual Studio 2019：安装工作负载](../install/media/vs-2019/vs-installer-workloads.png)

     例如，选择“ASP.NET 和 Web 开发”工作负载。 它附带默认核心编辑器，该编辑器针对超过 20 种语言提供基本代码编辑支持，能够打开和编辑任意文件夹中的代码（而无需使用项目），还提供集成的源代码管理。

1. 选择所需的工作负载后，选择“安装”。

    接下来，会出现多个显示 Visual Studio 安装进度的状态屏幕。

 ::: moniker-end

> [!TIP]
> 在安装之后，可以随时安装最初未安装的工作负荷或组件。 如果已打开 Visual Studio，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序。 或者，从“开始”菜单打开“Visual Studio 安装程序”。 在此处可以选择要安装的工作负载或组件。 然后，选择“修改”。

## <a name="step-5---choose-individual-components-optional"></a>第 5 步 - 选择各个组件（可选）

如果不想使用工作负载功能来自定义 Visual Studio 安装，或者想要添加比工作负载安装更多的组件，可通过从“各个组件”选项卡上安装或添加各个组件来完成此操作。选择所需组件，然后按照提示进行操作。

::: moniker range="vs-2017"

  ![Visual Studio 2017 - 安装各个组件](media/vs-installer-installing-components.png "安装 Visual Studio 各个组件")

::: moniker-end

::: moniker range="vs-2019"

  ![Visual Studio 2019 - 安装各个组件](media/vs-2019/vs-installer-individual-components.png "安装 Visual Studio 各个组件")

::: moniker-end

## <a name="step-6---install-language-packs-optional"></a>第 6 步 - 安装语言包（可选）

默认情况下，安装程序首次运行时会尝试匹配操作系统语言。 若要以所选语言安装 Visual Studio，请从 Visual Studio 安装程序中选择“语言包”选项卡，然后按照提示进行操作。

::: moniker range="vs-2017"

  ![Visual Studio 2017 - 安装语言包](media/vs-installer-installing-language-packs.png "安装 Visual Studio 语言包")

::: moniker-end

::: moniker range="vs-2019"

  ![Visual Studio 2019 - 安装语言包](media/vs-2019/vs-installer-language-packs.png "安装 Visual Studio 语言包")

::: moniker-end

### <a name="change-the-installer-language-from-the-command-line"></a>从命令行更改安装程序语言

更改默认语言的另一种方法是从命令行运行安装程序。 例如，可以通过运行以下命令来强制安装程序用英语运行：`vs_installer.exe --locale en-US`。 安装程序下一次运行时会记住此设置。 安装程序支持以下语言标记：zh-cn、zh-tw、cs-cz、en-us、es-es、fr-fr、de-de、it-it、ja-jp、ko-kr、pl-pl、pt-br、ru-ru 和 tr-tr。

## <a name="step-7---select-the-installation-location-optional"></a>第 7 步 - 选择安装位置（可选）

::: moniker range="vs-2017"

**15.7 中的新增功能**：现在可减少系统驱动器上 Visual Studio 的安装量。 可以选择将下载缓存、共享组件、SDK 和工具移动到不同驱动器，并将 Visual Studio 安装在其运行速度最快的驱动器上。

  ![Visual Studio 2017 - 更改安装位置](media/installation-options-by-location.png "更改安装位置")

::: moniker-end

::: moniker range="vs-2019"

可减少系统驱动器上 Visual Studio 的安装占用。 可以选择将下载缓存、共享组件、SDK 和工具移动到不同驱动器，并将 Visual Studio 安装在其运行速度最快的驱动器上。

  ![Visual Studio 2019 - 选择安装位置](media/vs-2019/vs-installer-installation-locations.png "选择安装位置")

::: moniker-end

> [!IMPORTANT]
> 仅当首次安装 Visual Studio 时，才可选择其他驱动器。 如果已安装 Visual Studio 并要更改驱动器，则必须先将其卸载然后再重新安装。

有关详细信息，请参阅[选择安装位置](change-installation-locations.md)页面。

## <a name="step-8---start-developing"></a>第 8 步 - 开始开发

::: moniker range="vs-2017"

1. 在 Visual Studio 安装完成后，选择“启动”按钮，开始使用 Visual Studio 进行开发。

2. 选择“文件”，然后选择“新建项目”。

3. 选择一种项目类型。

   例如，若要[生成 C++ 应用](../ide/getting-started-with-cpp-in-visual-studio.md)，请选择“已安装”，展开“Visual C++”，然后选择要生成的 C++ 项目类型。

   若要[生成 C# 应用](../get-started/csharp/tutorial-console.md)，请选择“已安装”，展开“Visual C#”，然后选择要生成的 C# 项目类型。

::: moniker-end

::: moniker range="vs-2019"

1. 在 Visual Studio 安装完成后，选择“启动”按钮，开始使用 Visual Studio 进行开发。

1. 在“开始”窗口上，选择“创建新项目”。

1. 在搜索框中，输入要创建的应用类型，查看可用模板列表。 模板列表取决于在安装期间选择的工作负载。 若要查看其他模板，请选择其他工作负载。

   此外，还可使用“语言”下拉列表筛选搜索特定编程语言。 也可使用“平台”列表和“项目类型”列表进行筛选。 

1. Visual Studio 会打开新的项目，然后便可开始编码！

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [更新 Visual Studio](update-visual-studio.md)
* [修改 Visual Studio](modify-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
* [创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [安装 Visual Studio for Mac](/visualstudio/mac/installation)