---
title: Visual Studio 2019 中的 JavaScript 和 TypeScript
ms.date: 03/16/2020
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.openlocfilehash: 199a27dbfef2b7297563e87d973137e2acd9c745
ms.sourcegitcommit: eef26de3d7a5c971baedbecf3b4941fb683ddb2d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81544284"
---
# <a name="javascript-and-typescript-in-visual-studio-2019"></a>Visual Studio 2019 中的 JavaScript 和 TypeScript

## <a name="overview"></a>概述

Visual Studio 2019 为 JavaScript 开发提供了丰富的支持，既可以直接使用 JavaScript，也可以使用 [TypeScript 编程语言](http://www.typescriptlang.org/)，其开发目的是提供更高效且充满乐趣的 JavaScript 开发体验，尤其是在大规模开发项目的时候。 对于许多应用程序类型和服务，可以在 Visual Studio 中编写 JavaScript 或 TypeScript 代码。

## <a name="javascript-language-service"></a>JavaScript 语言服务

Visual Studio 2019 中的 JavaScript 体验由提供 TypeScript 支持的相同引擎提供支持。 这为你提供更好的功能支持、丰富度和即时现成集成。

还原到旧版 JavaScript 语言服务的选项不再可用。 用户现在可以使用现成的新 JavaScript 语言服务。 新的语言服务仅基于 TypeScript 语言服务，由静态分析提供支持。 这使我们能够提供更好的工具，因此 JavaScript 代码可以从基于类型定义的更丰富的 IntelliSense 中受益。 新服务是轻量服务，比传统服务消耗更少的内存，代码可以缩放，因而可以提供更好的性能。 我们还改进了语言服务的性能以处理更大的项目。

## <a name="typescript-support"></a>TypeScript 支持

Visual Studio 2019 提供了若干选项，用于将 TypeScript 编译集成到项目中：

* [TypeScript NuGet 包](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)。 当 TypeScript 3.2 或更高版本的 NuGet 包安装到项目中时，将在编辑器中加载相应版本的 TypeScript 语言服务。
* [TypeScript npm 包](https://www.npmjs.com/package/typescript)。 当 TypeScript 2.1 或更高版本的 npm 包安装到项目中时，将在编辑器中加载相应版本的 TypeScript 语言服务。
* TypeScript SDK（在 Visual Studio 安装程序中默认提供），以及 [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.typescript-331-vs2017) 中提供的独立 SDK 下载。

> [!TIP]
> 对于使用 Visual Studio 2019 开发的项目，我们鼓励你使用 TypeScript NuGet 或 TypeScript npm 包，以实现跨不同平台和环境的更高可移植性。

NuGet 包的一个常见用法是使用 .NET Core CLI 编译 TypeScript。 除非手动编辑项目文件以从 TypeScript SDK 安装导入生成目标，否则 NuGet 包是使用 .NET Core CLI 命令（如 `dotnet build` 和 `dotnet publish`）启用 TypeScript 编译的唯一方法。

## <a name="remove-default-imports-aspnet-core-projects"></a>删除默认导入（ASP.NET Core 项目）

在使用[非 SDK 样式格式](https://docs.microsoft.com/nuget/resources/check-project-format)的旧项目中，可能需要删除某些项目文件元素。

如果使用 NuGet 包为项目提供 MSBuild 支持，则项目文件不得导入 `Microsoft.TypeScript.Default.props` 或 `Microsoft.TypeScript.targets`。 这些文件是通过 NuGet 包导入的，因此单独添加它们可能会导致意外的行为。

1. 右键单击项目，然后选择“卸载项目”  。

1. 右键单击项目，然后选择“编辑\<项目文件名\>”  。

   随即打开项目文件。

1. 删除对 `Microsoft.TypeScript.Default.props` 和 `Microsoft.TypeScript.targets` 的引用。

   要删除的导入如下所示：

   ```xml
   <Import
      Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.Default.props"
      Condition="Exists('$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.Default.props')" />

   <Import
      Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.targets"
      Condition="Exists('$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.targets')" />
   ```

## <a name="projects"></a>项目

Visual Studio 2019 不再支持 UWP JavaScript 应用。 无法创建或打开 JavaScript UWP 项目（扩展名为“.jsproj”  的文件）。 有关详细信息，请参阅有关[创建在 Windows 上运行良好的渐进式 Web 应用 (PWA)](/microsoft-edge/progressive-web-apps/get-started) 的文档。
