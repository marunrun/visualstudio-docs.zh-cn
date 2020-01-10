---
title: 并排安装 Visual Studio 版本
ms.date: 03/05/2019
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 62acf1c5e8cab960d4b670f7a05481644e9ffc1e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594079"
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

## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework 版本和并行安装

Visual Basic、Visual C# 和 Visual F# 项目使用“项目设计器”中的“目标框架”选项来指定项目使用的 .NET Framework 版本   。 对于 C++ 项目，您可以通过修改 .vcxproj 文件手动更改目标框架。 有关详细信息，请参阅 [.NET Framework 的版本兼容性](/dotnet/framework/migration-guide/version-compatibility)页。

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
