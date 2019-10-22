---
title: 快速入门：使用 Visual Studio 创建你的第一个 Node.js 应用
description: 本快速入门中，将在 Visual Studio 中创建 Node.js 应用
ms.date: 06/27/2018
ms.technology: vs-javascript
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 4995c6b95ba12eb776130b17dab1911c47988871
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180338"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-nodejs-app"></a>快速入门：使用 Visual Studio 创建你的第一个 Node.js 应用

在这个对 Visual Studio 集成开发环境 (IDE) 的 5-10 分钟简介中，可以创建简单的 Node.js Web 应用程序。

## <a name="prerequisites"></a>系统必备

* 须安装 Visual Studio 且具有 Node.js 开发工作负载。

    ::: moniker range=">=vs-2019"
    如果尚未安装 Visual Studio 2019，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads) 页免费安装。
    ::: moniker-end
    ::: moniker range="vs-2017"
    如果尚未安装 Visual Studio 2017，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 页免费安装。
    ::: moniker-end

    如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“Node.js 开发”工作负载，然后选择“修改”   。

    ![VS 安装程序中的 Node.js 工作负载](../ide/media/quickstart-nodejs-workload.png)

* 须安装 Node.js 运行时。

    如果未安装，请从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本。 一般情况下，Visual Studio 会自动检测已安装的 Node.js 运行时。 如果系统未检测到已安装运行时，则可以将项目配置为引用属性页中已安装的运行时（创建项目后，右键单击项目节点并选择“属性”）  。

## <a name="create-a-project"></a>创建项目

首先，创建 Node.js Web 应用程序项目。

1. 如果尚未安装 Node.js 运行时，请从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本。

    一般情况下，Visual Studio 会自动检测已安装的 Node.js 运行时。 如果系统未检测到已安装运行时，则可以将项目配置为引用属性页中已安装的运行时（创建项目后，右键单击项目节点并选择“属性”）  。

1. 打开 Visual Studio。

1. 创建新项目。

    ::: moniker range=">=vs-2019"
    按 Esc  关闭启动窗口。 键入 Ctrl+Q 以打开搜索框，键入“Node.js”，然后选择“创建新的空白 Node.js Web 应用程序项目”(JavaScript)    。 在出现的对话框中，选择“创建”  。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在顶部菜单栏，依次选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，展开“JavaScript”，然后选择“Node.js”    。 在中间窗格中，选择“空 Node.js Web 应用程序”，然后选择“确定”   。
    ::: moniker-end
    如果没有看到“空白 Node.js Web 应用程序”项目模板，  必须添加 Node.js 开发工作负载  。 有关详细说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并打开项目。 server.js 在位于左侧窗格的编辑器中打开  。

## <a name="explore-the-ide"></a>探索 IDE

1. 查看右窗格中的“解决方案资源管理器”  。

   ![“解决方案资源管理器”](../ide/media/quickstart-nodejs-solution-explorer.png)

   - 粗体突出显示的是项目，其名称是在“新建项目”  对话框中指定的名称。 在磁盘上，此项目由项目文件夹中的 .njsproj 文件表示  。

   - 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

   - Npm 节点显示任何已安装的 npm 包。 可以右键单击 npm 节点搜索 npm 包，并使用对话框安装 npm 包。

1. 如果想要从命令提示符安装 npm 包或 Node.js 命令，请右键单击项目节点，然后选择“在此处打开命令提示符”  。

   ![Node.js 命令提示符](../ide/media/quickstart-nodejs-command-prompt.png)

1. 在编辑器（左窗格）的 server.js  文件中，选择 `http.createServer`然后按 F12  或选择上下文菜单（右键单击菜单）中的“转到定义”  。 此命令将转到 index.d.ts 中 `createServer` 函数的定义  。

   ![转到定义上下文菜单](../ide/media/quickstart-nodejs-gotodefinition.png)

1. 返回 server.js，然后将光标置于此代码行 `res.end('Hello World\n');` 中字符串的末尾处，并对其进行如下修改  ：

    `res.end('Hello World\n' + res.connection.`

    IntelliSense 会在键入 `connection.` 的位置提供选项，自动完成代码输入。

   ![IntelliSense 自动完成](../ide/media/quickstart-nodejs-intellisense.png)

1. 选择“localPort”  ，然后键入 `);` 完成该语句，使其如下所示：

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-application"></a>运行此应用程序

1. 按 Ctrl+F5（或“调试”>“开始执行(不调试)”）运行应用程序    。 应用将在浏览器中打开。

1. 在浏览器窗口中，将看到“Hello World”以及本地端口号。

1. 关闭 Web 浏览器。

恭喜完成本快速入门，现在你已对 Visual Studio IDE 和 Node.js 有所了解。 若要深入了解其功能，请继续阅读目录中“教程”部分的教程  。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)

- [Node.js 和 Express 教程](../javascript/tutorial-nodejs.md)
- [Node.js 和 React 教程](../javascript/tutorial-nodejs-with-react-and-jsx.md)