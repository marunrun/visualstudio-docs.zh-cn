---
title: 并排安装 Visual Studio 版本
ms.date: 07/24/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.openlocfilehash: 717a9cd3f4157c276ce7d0dd5c41cac625581ba6
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88250249"
---
# <a name="install-visual-studio-versions-side-by-side"></a>并排安装 Visual Studio 版本

你可以在已安装 Visual Studio 早期版本或更高版本的计算机上安装 Visual Studio。

::: moniker range="vs-2017"

在并行安装各版本之前，你应了解以下情况：

* 如果使用 Visual Studio 2017 打开在 Visual Studio 2015 中创建的解决方案，则稍后可以在旧版本中再次打开和修改该解决方案，前提是你没有执行任何 Visual Studio 2017 特有的功能。

* 如果你尝试使用 Visual Studio 2017 打开在 Visual Studio 2015 或更早的版本中创建的解决方案，则可能需要修改你的项目和文件才能与 Visual Studio 2017 兼容。 有关详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017)页。

::: moniker-end

::: moniker range=">= vs-2019"

在并行安装各版本之前，你应了解以下情况：

* 如果使用 Visual Studio 2019 打开在 Visual Studio 2017 中创建的解决方案，则稍后可以在旧版本中再次打开和修改该解决方案，前提是你没有执行任何 Visual Studio 2019 特有的功能。

* 如果你尝试使用 Visual Studio 2019 打开在 Visual Studio 2017 或更早的版本中创建的解决方案，则可能需要修改你的项目和文件才能与 Visual Studio 2019 兼容。 有关详细信息，请参阅[移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)页。

::: moniker-end

* 如果在已安装多个版本的计算机上卸载 Visual Studio 的一个版本，则将为所有版本移除 Visual Studio 的文件关联。

* 因为并非所有扩展都兼容，所以 Visual Studio 不会自动升级扩展。 必须从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 或软件发行者处重新安装扩展。

## <a name="install-minor-visual-studio-versions-side-by-side"></a>并行安装 Visual Studio 次要版本

默认情况下，从 Visual Studio 的一个次要版本升级到下一个版本时，Visual Studio 安装程序会将当前安装版本更新为该通道中的下一个版本。 例如，在安装 16.6.4 预览版时，安装程序将尝试替换当前安装的 16.6.3 预览版，因为这两个版本都处于 16.6 预览通道中。 这有助于确保较早版本的 Visual Studio 不会占用计算机上的空间。 在某些特定情况下，并行安装次要版本可能会有所帮助。 在本示例中，这意味着同一台计算机上同时具备 16.6.3 和 16.6.4。

1. 下载要与现有 Visual Studio 版本并行安装的次要版本的 [Visual Studio 引导程序文件](https://docs.microsoft.com/visualstudio/releases/2019/history#installing-an-earlier-release)。
2. 在管理员模式下打开命令提示符。 为此，请打开 Windows“开始”菜单，键入“cmd”，右键单击命令提示符搜索结果，然后选择“以管理员身份运行”。 在命令提示符中，将目录更改为 Visual Studio 引导程序文件所在的文件夹。
3. 运行以下命令，为安装位置指定一个新文件夹路径，并将 .exe 文件名替换为要安装的 Visual Studio 版本的相应引导程序名称。 .exe 文件名应与以下文件名之一匹配或类似：
   * 对于 Visual Studio Community，应与 vs_community.exe 匹配或类似
   * 对于 Visual Studio Professional，应与 vs_professional.exe 匹配或类似
   * 对于 Visual Studio Enterprise，应与 vs_enterprise.exe 匹配或类似

   ```
   vs_Enterprise.exe --installPath "C:\Program Files (x86)\Microsoft Visual Studio\<2019 AddNewPath>"
   ```

4. 按照安装程序对话框选择安装所需的组件。 有关详细信息，请参阅[安装 Visual Studio](install-visual-studio.md#step-4---choose-workloads)。

## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework 版本和并行安装

Visual Basic、Visual C# 和 Visual F# 项目使用“项目设计器”中的“目标框架”选项来指定项目使用的 .NET Framework 版本 。 对于 C++ 项目，您可以通过修改 .vcxproj 文件手动更改目标框架。 有关详细信息，请参阅 [.NET Framework 的版本兼容性](/dotnet/framework/migration-guide/version-compatibility)页。

创建项目时，可以在 **“新建项目”** 对话框中的 **“.NET Framework”** 列表中指定项目针对的 .NET Framework 版本。

有关语言特定的信息，请参见下表中的相应主题。

::: moniker range="vs-2017"

| 语言 | 主题 |
|--------------|-----------|
| Visual Basic | [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md?view=vs-2017) |
| Visual C# | [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md?view=vs-2017) |
| Visual F# | [在 Visual Studio 中使用 Visual F# 进行开发](../ide/fsharp-visual-studio.md?view=vs-2017) |
|C++ | [如何：修改目标框架和平台工具集](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md?view=vs-2017)
* [移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017)
* [生成 C/C++ 独立应用程序和并行程序集](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end

::: moniker range=">= vs-2019"

| 语言 | 主题 |
|--------------|-----------|
| Visual Basic | [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md) |
| Visual C# | [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md) |
| Visual F# | [在 Visual Studio 中使用 Visual F# 进行开发](../ide/fsharp-visual-studio.md) |
| C++ | [如何：修改目标框架和平台工具集](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [移植、迁移和升级 Visual Studio 项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
* [生成 C/C++ 独立应用程序和并行程序集](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end
