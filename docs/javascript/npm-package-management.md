---
title: 管理 npm 包
description: Visual Studio 可帮助你使用 Node.js 包管理器 (npm) 来管理包
ms.custom: seodec18
ms.date: 03/12/2020
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: dba657d30eedef26337c708e7ede6c5ab85ed4cc
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "79549966"
---
# <a name="manage-npm-packages-in-visual-studio"></a>在 Visual Studio 中管理 npm 包

可以使用 npm 来安装和管理要在 Node.js 应用程序中使用的包。 使用 Visual Studio 可轻松地通过 UI 或直接与 npm 交互并发出 npm 命令。 如果不熟悉 npm 并想要详细了解，请转到 [npm 文档](https://docs.npmjs.com/)。

Visual Studio 与 npm 的集成因项目类型而异。
* [Node.js](#nodejs-projects)
* [ASP.NET Core](#aspnet-core-projects)
* [打开文件夹 (Node.js)](../javascript/develop-javascript-code-without-solutions-projects.md)

> [!Important]
> npm 在项目根目录中需要 node_modules 文件夹和 package.json   。 如果应用的文件夹结构不同，并且希望使用 Visual Studio 来管理 npm 包，则可以修改文件夹结构。

> [!NOTE]
> 对于现有的 Node.js 项目，请使用“基于现有 Node.js 代码”解决方案模板来在项目中启用 npm  。

## <a name="nodejs-projects"></a>Node.js 项目

对于 Node.js 项目，请使用以下方法之一：
* [从解决方案资源管理器安装包](#npmInstallWindow)
* [从解决方案资源管理器管理安装的包](#solutionExplorer)
* [在 Node.js 交互式窗口中使用 `.npm` 命令](#interactive)

这些功能协同工作，并与项目系统和项目中的 package.json  文件同步。

### <a name="install-packages-from-solution-explorer-nodejs"></a><a name="npmInstallWindow"></a>从解决方案资源管理器安装包 (Node.js)

对于 Node.js 项目，安装 npm 包的最简单方法是通过 npm 包安装窗口。 若要访问此窗口，右键单击项目中的“npm”节点并选择“安装新的 npm 包”   。

![从解决方案资源管理器安装新的 npm 包](../javascript/media/solution-explorer-install-package.png)

在此窗口中可以搜索包、指定选项并安装。

![搜索 npm 包](../javascript/media/search-package.png)

* 依赖项类型 - 在“标准”、“开发”和“可选”包间进行选择     。 “标准”指定包是一个运行时依赖项，而“开发”指定只在开发过程中需要包。
* 添加到 package.json  - 此选项已弃用
* 所选版本  - 选择你想要安装的包版本。
* 其他 npm 参数  - 指定其他标准参数。 例如，可以输入版本值（如 `@~0.8`），安装版本列表中不可用的特定版本。

可以在“输出”窗口的 npm 输出中查看安装进度   。 这可能需要一些时间。

![npm 输出](../javascript/media/npm-output.png)

> [!TIP]
> 可以在搜索查询前添加感兴趣的范围，进而搜索范围内的包，例如键入 `@types/mocha` 来查找 mocha 的 TypeScript 定义文件。 此外，安装 TypeScript 的类型定义时，可以在 npm 参数字段中添加 `@ts2.6`，指定要面向的 TypeScript 版本。

### <a name="manage-installed-packages-in-solution-explorer-nodejs"></a><a name="solutionExplorer"></a>在解决方案资源管理器中管理安装的包 (Node.js)

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

### <a name="use-the-npm-command-in-the-nodejs-interactive-window-nodejs"></a><a name="interactive"></a>在 Node.js 交互式窗口中使用 .npm 命令 (Node.js)

还可在 Node.js 交互式窗口中使用 `.npm` 命令来执行 npm 命令。 若要打开该窗口，请右键单击解决方案资源管理器中的项目，然后选择“打开 Node.js 交互式窗口”  。

在窗口中，可以使用如下命令来安装包：

`.npm install azure@4.2.3`

 > [!Tip]
 > 默认情况下，npm 将在项目的主目录中执行。 如果解决方案中有多个项目，请在方括号中指定项目的名称或路径。
 > `.npm [MyProjectNameOrPath] install azure@4.2.3`

 > [!Tip]
 > 如果项目不包含 package.json 文件，请使用 `.npm init -y` 创建含默认条目的新 package.json 文件。

 ## <a name="aspnet-core-projects"></a>ASP.NET Core 项目

对于 ASP.NET Core 项目之类的项目，可以在项目中集成 npm 支持，并使用 npm 安装包。
* [向项目添加 npm 支持](#npmAdd)
* [使用 package.json 安装包](#npmInstallPackage)

>[!NOTE]
> 对于 ASP.NET Core 项目，还可以使用[库管理器](https://docs.microsoft.com/aspnet/core/client-side/libman/?view=aspnetcore-3.1)或 yarn（而非 npm）来安装客户端 JavaScript 和 CSS 文件。

### <a name="add-npm-support-to-a-project-aspnet-core"></a><a name="npmAdd"></a>向项目添加 npm 支持 (ASP.NET Core)

如果项目尚未包含 package.json  文件，则可以通过将 package.json 文件添加到该项目来添加一个启用 npm 支持。

1. 要添加文件，请右键单击解决方案资源管理器中的项目，然后选择“添加” > “新项”   。 选择“npm 配置文件”，使用默认名称，然后单击“添加”   。

   ![将 package.json 添加到项目](../javascript/media/npm-add-package-json.png)

1. 在 package.json 的 `dependencies` 或 `devDependencies` 部分中添加一个或多个 npm 包  。 例如，可以向文件添加以下内容：

   ```json
   "devDependencies": {
      "gulp": "4.0.2",
      "@types/jquery": "3.3.33"
   }
   ```

保存文件时，Visual Studio 会将包添加到解决方案资源管理器中的“依赖项/npm”节点下  。 如果未显示该节点，请右键单击“package.json”并选择“还原包”   。

>[!NOTE]
> 在某些情况下，解决方案资源管理器可能会指示由于[此处](https://github.com/aspnet/Tooling/issues/479)所述的已知问题，npm 包与 package.json 不同步  。 例如，在安装包时，可能会显示为未安装。 在大多数情况下，可以通过删除 package.json，重启 Visual Studio 并重新添加 package.json 文件来更新解决方案资源管理器，如本文前面所述   。

### <a name="install-packages-using-packagejson-aspnet-core"></a><a name="npmInstallPackage"></a>使用 package.json 安装包 (ASP.NET Core)

对于包含 npm 的项目，可以使用 `package.json` 配置 npm 包。 右键单击解决方案资源管理器中的 npm 节点，并选择“打开 package.json”  。

![搜索 npm 包](../javascript/media/npm-add-package.png)

package.json 中的 IntelliSense 可帮助选择特定版本的 npm 包  。

![搜索 npm 包](../javascript/media/npm-add-package-intellisense.png)

保存文件时，Visual Studio 会将包添加到解决方案资源管理器中的“依赖项/npm”节点下  。 如果未显示该节点，请右键单击“package.json”并选择“还原包”   。

安装包可能需要几分钟的时间。 通过在“输出”窗口中切换到“npm”输出来查看包的安装进度   。

![npm 输出](../javascript/media/npm-output.png)

