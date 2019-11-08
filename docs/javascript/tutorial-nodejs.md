---
title: 创建 Node.js 和 Express 应用
description: 在本教程中，使用 Visual Studio 的 Node.js 工具创建应用
ms.date: 09/24/2018
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: ecc14e4dc98caa17ac3849e9231ab17491f2acc8
ms.sourcegitcommit: 2f64b3b231900018fceafb72b5a1c65140213a18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "73428781"
---
# <a name="tutorial-create-a-nodejs-and-express-app-in-visual-studio"></a>教程：在 Visual Studio 中创建 Node.js 和 Express 应用

本教程介绍如果使用 Node.js 和 Express 进行 Visual Studio 开发，教程会创建一个简单的 Node.js Web 应用，添加一些代码，浏览 IDE 的某些功能并运行应用。 

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

在本教程中，你将了解：
> [!div class="checklist"]
> * 创建 Node.js 项目
> * 添加一些代码
> * 使用 IntelliSense 编辑代码
> * 运行应用
> * 命中调试程序中的断点

## <a name="before-you-begin"></a>在开始之前

下面是一个快速 FAQ，介绍一些关键概念。

### <a name="what-is-nodejs"></a>什么是 Node.js？

Node.js 是执行 JavaScript 服务器端的服务器端 JavaScript 运行时环境。

### <a name="what-is-npm"></a>什么是 npm？

Npm 是 Node.js 的默认包管理器。 包管理器使程序员更容易发布和共享 Node.js 库的源代码，并且可简化库的安装、更新和卸载。

### <a name="what-is-express"></a>Express 是什么？

Express 是一个 Web 应用程序框架，用作 Node.js 构建 Web 应用程序的服务器框架。 Express 允许使用不同的前端框架来创建 UI，例如 Pug（以前称为 Jade）。 本教程中使用了 Pug。

## <a name="prerequisites"></a>系统必备

* 须安装 Visual Studio 且具有 Node.js 开发工作负载。

    ::: moniker range=">=vs-2019"
    如果尚未安装 Visual Studio 2019，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。
    ::: moniker-end
    ::: moniker range="vs-2017"
    如果尚未安装 Visual Studio 2017，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。
    ::: moniker-end

    如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“Node.js 开发”工作负载，然后选择“修改”   。

    ![VS 安装程序中的 Node.js 工作负载](../ide/media/quickstart-nodejs-workload.png)

* 须安装 Node.js 运行时。

    如果未安装，请从 [Node.js](https://nodejs.org/en/download/) 网站安装 LTS 版本。 一般情况下，Visual Studio 会自动检测已安装的 Node.js 运行时。 如果系统未检测到已安装运行时，则可以将项目配置为引用属性页中已安装的运行时（创建项目后，右键单击项目节点并选择“属性”）  。

    本教程已使用 Node.js 8.10.0 进行测试。

## <a name="create-a-new-nodejs-project"></a>创建新的 Node.js 项目

Visual Studio 管理项目中的单个应用程序的文件  。 该项目包括源代码、资源和配置文件。

在本教程中，将从一个包含 Node.js 和 express 应用的代码的简单项目开始。

1. 打开 Visual Studio。

1. 创建新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 键入 Ctrl+Q 以打开搜索框，键入“Node.js”，然后选择“创建新的基本 Azure Node.js Express 4 应用程序”(JavaScript)    。 在出现的对话框中，选择“创建”  。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在顶部菜单栏，依次选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，展开“JavaScript”，然后选择“Node.js”    。 在中间窗格中，选择“基本 Azure Node.js Express 4 应用程序”，然后选择“确定”   。
    ::: moniker-end
    如果未看到“基本 Azure Node.js Express 4 应用程序”项目模板，必须添加 Node.js 开发工作负载   。 有关详细说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并在右窗格中打开项目。 在编辑器（左窗格）中打开 App.js  项目文件。

    ![项目结构](../javascript/media/tutorial-project-structure.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称   。 在文件系统中，此项目由项目文件夹中的 .njsproj 文件表示  。 可以右键单击项目并选择“属性”，设置与项目相关的属性和环境变量  。 可以使用其他开发工具执行往返，因为项目文件不对 Node.js 项目源做出自定义更改。

    (2) 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

    (3) Npm 节点显示任何已安装的 npm 包。 可右键单击 npm 节点以使用对话框搜索并安装 npm 包，也可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项  。

    (4) package.json 是 npm 用于管理本地安装包的包依赖关系和包版本的文件  。 有关此文件的详细信息，请参阅 [package.json 配置](../javascript/configure-packages-with-package-json.md)

    (5) 项目文件（例如 app.js）显示在项目节点下  。 app.js 是项目启动文件，因此它以粗体形式显示   。 可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。

1. 打开“npm”节点，确保其中存在所有必需的 npm 包  。

    如果缺少任何包（感叹号图标），可右键单击“npm”节点并选择“安装缺少的 npm 包”   。

## <a name="add-some-code"></a>添加一些代码

该应用程序将 Pug 用于前端 JavaScript 框架。 Pug 使用编译为 HTML 的简单标记代码。 （将 Pug 设置为 app.js 中的视图引擎  。 在 app.js 中设置视图引擎的代码是 `app.set('view engine', 'pug');`  。）

1. 在解决方案资源管理器（右窗格）中，打开“视图”文件夹，然后打开 index.pug  。

1. 将内容替换为以下标记。

    ```js
    extends layout

    block content
      h1= title
      p Welcome to #{title}
      script.
        var f1 = function() { document.getElementById('myImage').src='#{data.item1}' }
      script.
        var f2 = function() { document.getElementById('myImage').src='#{data.item2}' }
      script.
        var f3 = function() { document.getElementById('myImage').src='#{data.item3}' }

      button(onclick='f1()') One!
      button(onclick='f2()') Two!
      button(onclick='f3()') Three!
      p
      a: img(id='myImage' height='200' width='200' src='')
    ```

    之前的代码用于动态生成带有标题和欢迎消息的 HTML 页面。 该页面还包含代码，用于显示每当按一个按钮时就会更改的图像。

1. 在“路由”文件夹中，打开 index.js  。

1. 在 `router.get` 的调用前添加以下代码：

    ```js
    var getData = function () {
        var data = {
            'item1': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-76.jpg',
            'item2': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-77.jpg',
            'item3': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-78.jpg'
        }
        return data;
    }
    ````

    此代码创建一个数据对象，将其传递给动态生成的 HTML 页面。

1. 使用以下代码替换 `router.get` 函数调用：

    ```js
    router.get('/', function (req, res) {
        res.render('index', { title: 'Express', "data" });
    });
    ```

    之前的代码使用 Express 路由器对象设置当前页并呈现该页，将标题和数据对象传递给页面。 Index.pug 文件在此处指定为运行 index.js 时要加载的页面   。 Index.js 配置为 app.js 代码中的默认路由（未显示）   。

    为了演示 Visual Studio 的几个功能，我们有意在包含 `res.render` 的代码行中包含一个错误。 需要修复该错误应用才能运行，下一部分中将执行该操作。

## <a name="use-intellisense"></a>使用 IntelliSense

IntelliSense 是一款可帮助编写代码的 Visual Studio 工具。

1. 在 index.js 中，转到包含 `res.render` 的代码行  。

1. 将光标置于 `data` 字符串后，键入 `: get`，IntelliSense 将显示之前在代码中定义的 `getData` 函数。 选择 `getData`。

    ![使用 IntelliSense](../javascript/media/tutorial-nodejs-intellisense.png)

1. 添加括号，使其成为函数调用 `getData()`。

1. 删除 `"data"` 前的逗号 (`,`)，将看到针对该表达式的绿色语法突出显示。 将鼠标悬停在语法突出显示上。

    ![查看语法错误](../javascript/media/tutorial-nodejs-syntax-checking.png)

    此消息的最后一行告诉你，JavaScript 解释器需要一个逗号 (`,`)。

1. 在下方的窗格中，单击“错误列表”选项卡  。

    可看到警告和描述，以及文件名和行号。

    ![查看错误列表](../javascript/media/tutorial-nodejs-error-list.png)

1. 在 `"data"` 前添加逗号 (`,`)，修复代码。

    更正后，代码行应如下所示：`res.render('index', { title: 'Express', "data": getData() });`

## <a name="set-a-breakpoint"></a>设置断点

接着使用附加的 Visual Studio 调试程序来运行应用。 执行该操作之前，需要设置断点。

1. 在 index.js 中，单击以下代码行前左测的装订线，设置一个断点  ：

    `res.render('index', { title: 'Express', "data": getData() });`

    断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

    ![设置断点](../javascript/media/tutorial-nodejs-set-breakpoint.png)

## <a name="run-the-application"></a>运行此应用程序

1. 在“调试”工具栏中选择调试目标，例如 Microsoft Edge 或 Chrome。

    ::: moniker range=">=vs-2019"
    ![选择调试目标](../javascript/media/vs-2019/tutorial-nodejs-deploy-target.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![选择调试目标](../javascript/media/tutorial-nodejs-deploy-target.png)
    ::: moniker-end

    如果计算机上有 Chrome，但未显示为选项，请从调试目标下拉列表中选择  “浏览方式”，然后选择 Chrome 作为默认浏览器目标（选择“设为默认值”  ）。

1. 按 F5  （“调试”   > “启动调试”  ）来运行该应用程序。

    调试器会在设置的断点处暂停。 现在，可以检查应用状态。

1. 将鼠标悬停在 `getData` 上，查看其在数据提示中的属性

    ![检查变量](../javascript/media/tutorial-nodejs-inspect-variables.png)

1. 按 F5  （“调试”   > “继续”  ）继续。

    应用将在浏览器中打开。

    在浏览器窗口中，将看到“Express”为标题，“Welcome to Express”位于第一个段。

1. 单击这些按钮可显示不同的图像。

    ![在浏览器中运行应用](../javascript/media/tutorial-nodejs-running-in-browser.png)

1. 关闭 Web 浏览器。

## <a name="optional-publish-to-azure-app-service"></a>（可选）发布到 Azure 应用服务

1. 在解决方案资源管理器中，右键单击项目，选择“发布”  。

   ![发布到 Azure 应用服务](../javascript/media/tutorial-nodejs-publish-to-azure.png)

1. 选择“Microsoft Azure 应用服务”  。

    在“应用服务”  对话框中，可登录 Azure 帐户并连接到现有的 Azure 订阅。

1. 按其余步骤来选择订阅、选择或创建资源组、选择或创建应用服务计划，然后在系统提示发布到 Azure 时按照步骤操作。 有关更详细的说明，请参阅 [Publish to Azure Website using Web Deploy](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy)（使用 Web 部署发布到 Azure 网站）。

1. “输出”  窗口显示部署到 Azure 的进度。

    成功部署后，应用将在 Azure 应用服务中运行的浏览器中打开。 单击按钮可显示图像。

   ![Azure 应用服务中运行的应用](../javascript/media/tutorial-nodejs-running-in-azure.png)

恭喜你完成本教程！

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)
