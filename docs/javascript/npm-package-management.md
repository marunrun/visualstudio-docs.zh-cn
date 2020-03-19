---
title: 管理 npm 包
description: Visual Studio 可帮助你使用 Node.js 包管理器 (npm) 来管理包
ms.custom: seodec18
ms.date: 06/06/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: de92c3f1f0d0e29d1ba2dfaf5d536a42e636be2c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307219"
---
# <a name="manage-npm-packages-in-visual-studio"></a>在 Visual Studio 中管理 npm 包

可以使用 npm 来安装和管理要在 Node.js 应用程序中使用的包。 如果不熟悉 npm 并想要详细了解，请转到 [npm 文档](https://docs.npmjs.com/)。

使用 Visual Studio 可轻松地通过 UI 或直接与 npm 交互并发出 npm 命令。 可以使用以下方法：
* [从解决方案资源管理器安装包](#npmInstallWindow)
* [从解决方案资源管理器管理安装的包](#solutionExplorer)
* [在 Node.js 交互式窗口中使用 `.npm` 命令](#interactive)

这些功能协同工作，并与项目系统和项目中的 package.json  文件同步。

> [!Important]
> NPM 在项目根目录中需要 node_modules 文件夹和 package.json   。 如果应用的文件夹结构不同，并且希望使用 Visual Studio 来管理 npm 包，则可以更新文件夹结构。

> [!NOTE]
> 对于现有的 NPM 项目，请使用“基于现有 Node.js 代码”解决方案模板  。

## <a name="npmInstallWindow"></a>从解决方案资源管理器安装包

安装 npm 包的最简单方法是通过 npm 包安装窗口。 若要访问此窗口，右键单击项目中的“npm”节点并选择“安装新的 npm 包”   。

![从解决方案资源管理器安装新的 npm 包](../javascript/media/solution-explorer-install-package.png)

在此窗口中可以搜索包、指定选项并安装。

![搜索 npm 包](../javascript/media/search-package.png)

* 依赖项类型 - 在“标准”、“开发”和“可选”包间进行选择     。 “标准”指定包是一个运行时依赖项，而“开发”指定只在开发过程中需要包。
* 添加到 package.json  - 此选项已弃用
* 所选版本  - 选择你想要安装的包版本。
* 其他 npm 参数  - 指定其他标准参数。 例如，可以输入版本值（如 `@~0.8`），安装版本列表中不可用的特定版本。

可以在“输出”窗口的 npm 选项卡中查看安装进度。 这可能需要一些时间。

> [!TIP]
> 可以在搜索查询前添加感兴趣的范围，进而搜索范围内的包，例如键入 `@types/mocha` 来查找 mocha 的 TypeScript 定义文件。 此外，安装 TypeScript 的类型定义时，可以在 npm 参数字段中添加 `@ts2.6`，指定你面向的 TypeScript 版本。

## <a name="solutionExplorer"></a>在解决方案资源管理器中管理安装的包

npm 包显示在解决方案资源管理器中。 “npm”节点下的条目模拟 package.json 文件中的依赖项   。

![搜索 npm 包](../javascript/media/solution-explorer-status.png)

### <a name="package-status"></a>包状态
* ![已安装的包](../javascript/media/installed-npm.png) - 已安装并列在 package.json 中
* ![无关包](../javascript/media/extraneous-npm.png) - 已安装但未显式列在 package.json 中
* ![缺失的包](../javascript/media/missing-npm.png) - 未安装，但列在 package.json 中

右键单击包节点或“npm”  节点，执行以下操作之一：
* 安装 package.json 中列出的缺失的包  
* 将包更新到最新版本 
* 卸载包  ，并从 package.json  中删除

## <a name="interactive"></a>在 Node.js 交互式窗口中使用 .npm 命令

还可在 Node.js 交互式窗口中使用 `.npm` 命令来执行 npm 命令。 若要打开该窗口，请右键单击解决方案资源管理器中的项目，然后选择“打开 Node.js 交互式窗口”  。

在窗口中，可以使用如下命令来安装包：

`.npm install azure@4.2.3`

 > [!Tip]
 > 默认情况下，npm 将在项目的主目录中执行。 如果解决方案中有多个项目，请在方括号中指定项目的名称或路径。
 > `.npm [MyProjectNameOrPath] install azure@4.2.3`

 > [!Tip]
 > 如果项目不包含 package.json 文件，请使用 `.npm init -y` 创建含默认条目的新 package.json 文件。
