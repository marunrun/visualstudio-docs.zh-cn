---
title: 使用 NuGet 编译和生成 TypeScript 代码
description: 了解如何在 Visual Studio 中编译和生成 TypeScript。
ms.date: 7/23/2020
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: ac917248915129b8d93dc776ac7d35a2ed227069
ms.sourcegitcommit: b8ec700fc4c14c68c6ce280f29c19870261990d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87454615"
---
# <a name="compile-typescript-code-aspnet-core"></a>编译 TypeScript 代码 (ASP.NET Core)

可使用 TypeScript SDK 将 TypeScript 支持添加到项目中，默认情况下，可在 Visual Studio 安装程序中使用，也可以使用 NuGet 包提供。 对于在 Visual Studio 2019 中开发的项目，建议使用 TypeScript NuGet，以实现跨不同平台和环境的更高可移植性。

对于 ASP.NET Core 项目，NuGet 包的一个常见用法是使用 .NET Core CLI 编译 TypeScript。 除非手动编辑项目文件以从 TypeScript SDK 安装导入生成目标，否则 NuGet 包是使用 .NET Core CLI 命令（如 `dotnet build` 和 `dotnet publish`）启用 TypeScript 编译的唯一方法。 此外，对于与 ASP.NET Core 和 TypeScript 集成的 [MSBuild](https://www.staging-typescript.org/docs/handbook/compiler-options-in-msbuild.html)，请选择 NuGet 包而不是 npm 包。

## <a name="add-typescript-support-with-nuget"></a>使用 NuGet 添加 TypeScript 支持

[TypeScript NuGet 包](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)添加 TypeScript 支持。 当 TypeScript 3.2 或更高版本的 NuGet 包安装到项目中时，将在编辑器中加载相应版本的 TypeScript 语言服务。

如果安装了 Visual Studio，那么与之捆绑的 node.exe 将自动由 Visual Studio 选取。 如果尚未安装 Node.js，则建议从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本。

1. 在 Visual Studio 中打开 ASP.NET Core 项目。

1. 在解决方案资源管理器中（右侧窗格）。 右键单击项目节点，然后选择“管理 NuGet 包”。 在“浏览”选项卡中，搜索“Microsoft.TypeScript.MSBuild”，然后单击右侧的“安装”来安装包。

   ![添加 NuGet 包](../javascript/media/aspnet-core-ts-nuget.png)

   Visual Studio 会将 NuGet 包添加到解决方案资源管理器中的“依赖项”节点下。 以下包引用将添加到 *.csproj 文件。

   ```xml
   <PackageReference Include="Microsoft.TypeScript.MSBuild" Version="3.9.7">
      <PrivateAssets>all</PrivateAssets>
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
   </PackageReference>
   ```

1. 右键单击项目节点，然后选择“添加”>“新项”。 选择“TypeScript JSON 配置文件”，然后单击“添加”。

   Visual Studio 会将 tsconfig.json 文件添加到项目根目录中。 可以使用此文件为 TypeScript 编译器[配置选项](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

1. 打开 tsconfig.json 并更新，以设置所需的编译器选项。

   下面是一个简单的 tsconfig.json 文件示例。

   ```json
   {
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "wwwroot/js"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   在此示例中：
   - include 告诉编译器在何处查找 TypeScript (*.ts) 文件。
   - outDir 选项指定 TypeScript 编译器转译的普通 JavaScript 文件的输出文件夹。
   - “sourceMap”选项指示编译器是否生成 sourceMap 文件。

   以前的配置仅提供配置 TypeScript 的基本简介。 有关其他选项的信息，请参阅 [tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

### <a name="build-the-application"></a>生成应用程序

1. 将 TypeScript (.ts) 或 TypeScript JSX (.tsx) 文件添加到项目，然后添加 TypeScript 代码。 有关 TypeScript 的简单示例，请使用以下内容：

   ```typescript
   let message: string = 'Hello World';
   console.log(message);
   ```

1. 如果使用的是较旧的非 SDK 样式项目，请在生成前按照[删除默认导入](#remove-default-imports)中的说明进行操作。

1. 选择“生成”>“生成解决方案”。

   尽管应用程序会在运行时自动生成，但我们想要查看在生成过程中发生的一些事情：

   如果生成了源映射，请打开在“outDir”选项中指定的文件夹，并找到生成的 *.js 文件以及生成的 *js.map 文件。

   调试需要源映射文件。

1. 如果要在每次保存项目时进行编译，请使用 *.tsconfig 中的“compileOnSave”选项。

   ```json
   ```{
      "compileOnSave":  true,
      "compilerOptions": {
      }
   }
   ```

有关将 gulp 与任务运行程序结合使用来生成应用的示例，请参阅 [ASP.NET Core 和 TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)。

如果遇到 Visual Studio 使用的 Node.js 或第三方工具的版本不同于所需版本的问题，则可能需要设置 Visual Studio 要使用的路径。 选择“工具” > “选项”。 在“项目和解决方案”下，选择“Web 包管理” > “外部 Web 工具”。

### <a name="nuget-package-structure-details"></a>NuGet 包结构详细信息

`Microsoft.TypeScript.MSBuild.nupkg` 包含两个主要文件夹：

- build 文件夹

    此文件夹中有两个文件。
    两者均为入口点，分别用于主要 TypeScript 目标文件和属性文件。

    1. Microsoft.TypeScript.MSBuild.targets

        此文件设置指定运行时平台的变量（如 TypeScript.Tasks.dll 的路径），然后从 tools 文件夹中导入 Microsoft.TypeScript.targets。

    2. Microsoft.TypeScript.MSBuild.props

        此文件从 tools 文件夹中导入 Microsoft.TypeScript.Default.props，并设置指示已通过 NuGet 启动生成的属性。

- tools 文件夹

    2\.3 之前的包版本只包含一个 tsc 文件夹。 Microsoft.TypeScript.targets 和 TypeScript.Tasks.dll 位于根级别。

    在包版本 2.3 及更高版本中，根级别包含 `Microsoft.TypeScript.targets` 和 `Microsoft.TypeScript.Default.props`。 有关这些文件的更多详细信息，请参阅 [MSBuild 配置](https://www.typescriptlang.org/docs/handbook/compiler-options-in-msbuild.html)。

    此外，文件夹包含三个子文件夹：

    1. net45

        此文件夹包含 `TypeScript.Tasks.dll` 以及它所依赖的其他 DLL。
        在 Windows 平台上生成项目时，MSBuild 将使用此文件夹中的 DLL。

    2. netstandard1.3

        此文件夹包含 `TypeScript.Tasks.dll` 的另一版本，该版本在非 Windows 计算机上生成项目时使用。

    3. tsc

        此文件夹包含 `tsc.js`、`tsserver.js` 及它们作为节点脚本运行所需的所有依赖项文件。

        > [!NOTE]
        > 如果安装了 Visual Studio，则会自动选择与之捆绑的 node.js。 否则，必须在计算机上安装 Node.js。

        3\.1 之前的版本包含运行编译的 `tsc.exe` 可执行文件。 在版本 3.1 中，已删除此文件，以便使用 `node.exe`。

### <a name="remove-default-imports"></a>删除默认导入

在使用[非 SDK 样式格式](https://docs.microsoft.com/nuget/resources/check-project-format)的旧 ASP.NET Core 项目中，可能需要删除某些项目文件元素。

如果使用 NuGet 包为项目提供 MSBuild 支持，则项目文件不得导入 `Microsoft.TypeScript.Default.props` 或 `Microsoft.TypeScript.targets`。 这些文件是通过 NuGet 包导入的，因此单独添加它们可能会导致意外的行为。

1. 右键单击项目，然后选择“卸载项目”  。

1. 右键单击项目并选择“编辑 \<*project file name*\>”。

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
