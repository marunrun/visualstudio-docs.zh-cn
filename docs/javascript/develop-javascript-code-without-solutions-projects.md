---
title: 在无需解决方案或项目的情况下在 Visual Studio 中编写 JavaScript 代码
titleSuffix: ''
description: Visual Studio 支持创建代码，而无需依赖于项目文件或解决方案文件
ms.custom: seodec18
ms.date: 09/24/2018
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 187ca5ea0d0232e0ca8b99165e77ee265b81e801
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285083"
---
# <a name="develop-javascript-and-typescript-code-in-visual-studio-without-solutions-or-projects"></a>在 Visual Studio 中开发 JavaScript 和 TypeScript 代码，而无需解决方案或项目

在 Visual Studio 2017 中开始，可[开发代码而无需项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)，这样便可打开代码的文件夹并立即开始使用丰富的编辑器支持，如 IntelliSense、搜索、重构、调试等。 除了这些功能，针对 Visual Studio 的 Node.js 工具还支持生成 TypeScript 文件、管理 npm 包和运行 npm 脚本。

若要开始，请从工具栏中选择“文件” > “打开” > “文件夹”    。 解决方案资源管理器显示文件夹中的所有文件，你可以打开任何文件以开始编辑。 在后台，Visual Studio 对文件编制索引，启用 npm、生成和调试功能。

> [!IMPORTANT]
> 本文所述的很多功能（包括 npm 集成）均要求 Visual Studio 2017 版本 15.8 或更高版本。 必须安装 Visual Studio Node.js 开发工作负载  。

## <a name="npm-integration"></a>npm 集成

如果打开的文件夹包含 package.json 文件，可以右键单击 package.json，显示特定于 npm 的上下文菜单（快捷菜单）   。

![解决方案资源管理器中的 npm 菜单](../javascript/media/solution-explorer-npm-ctx.png)

在快捷菜单中，可以管理由 npm 安装的包，如同使用项目文件时[管理 npm 包](npm-package-management.md)一样。

此外，菜单还允许运行 package.json 中 `scripts` 元素定义的脚本  。 这些脚本将使用 `PATH` 环境变量上提供的 Node.js 版本。 脚本在新窗口中运行。 这是执行生成或运行脚本的好办法。

## <a name="build-and-debug"></a>生成和调试

### <a name="packagejson"></a>package.json
如果文件夹中的 package.json  指定 `main` 元素，“调试”  命令将出现在 package.json 的右击快捷菜单中  。
单击此项将启动 node.exe  ，使用指定脚本作为其参数。

### <a name="javascript-files"></a>JavaScript 文件
右键单击文件并从快捷菜单中选择“调试”，可以调试 JavaScript 文件  。 这将启动 node.exe  ，使用该 JavaScript 文件作为其参数。

### <a name="typescript-files-and-tsconfigjson"></a>TypeScript 文件和 tsconfig.json
如果文件夹中没有任何 tsconfig.json  ，可以右键单击 TypeScript 文件，查看快捷菜单命令来生成和调试该文件。 使用这些命令时，使用 tsc.exe 通过默认选项来进行生成或调试  。 （需要生成文件，才可进行调试。）

> [!NOTE]
> 生成 TypeScript 代码时，我们使用 `C:\Program Files (x86)\Microsoft SDKs\TypeScript` 中安装的最新版本。

如果文件夹中存在 tsconfig.json 文件  ，可以右键单击 TypeScript 文件，查看菜单命令来调试该 TypeScript 文件。 仅当 tsconfig.json 中未指定任何 `outFile` 时，该选项才出现  。 如果指定了 `outFile`，可以右键单击 tsconfig.json 并选择正确选项来调试该文件  。 `tsconfig.json` 文件还提供生成选项，可借此指定编译器选项。

> [!NOTE]
> 若要了解 tsconfig.json 的详细信息，可查找 [tsconfig.json TypeScript 手册页](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)  。

## <a name="unit-tests"></a>单元测试
可通过在 package.json 中指定测试根，在 Visual Studio 中启用单元测试集成  ：

```json
{
    // ...
    "vsTest":{
        "testRoot": "./tests"
    }
    // ...
}
```

测试运行程序枚举本地安装的包，确定要使用的测试框架。
如果未识别出任何受支持的框架，则测试运行程序默认为 ExportRunner  。 支持的其他框架：
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))

打开测试资源管理器（选择“测试” > “Windows” > “测试资源管理器”）后，Visual Studio 发现并显示测试    。

> [!NOTE]
> 测试运行程序只枚举测试根目录中的 JavaScript 文件，如果应用采用 TypeScript 编写而成，则需要先构建这些文件。
