---
title: 调试 JavaScript 或 TypeScript 应用
description: Visual Studio 支持在 Visual Studio 中调试 JavaScript 和 TypeScript 应用
ms.date: 11/01/2019
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 0405488f6f456f22711498e81789881ffc5a0a8a
ms.sourcegitcommit: 308a2bdbea81df78bffc3a01afce4ab13131fabc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2019
ms.locfileid: "73912996"
---
# <a name="debug-a-javascript-or-typescript-app-in-visual-studio"></a>在 Visual Studio 中调试 JavaScript 或 TypeScript 应用

可以使用 Visual Studio 调试 JavaScript 和 TypeScript 代码。 可以设置和命中断点、附加调试器、检查变量、查看调用堆栈以及使用其他调试功能。

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。 根据所展开的应用开发的类型，可能需要使用 Visual Studio 安装 Node.js 开发工作负荷  。

## <a name="debug-server-side-script"></a>调试服务器端脚本

1. 在 Visual Studio 中打开项目，然后打开服务器端 JavaScript 文件（例如“server.js”），单击左侧滚动条槽以设置断点  ：

    ![设置断点](../javascript/media/tutorial-nodejs-react-set-breakpoint.png)

    断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

1. 若要运行应用，请按“F5”（“调试” > “启动调试”）    。

    调试器将在设置的断点处暂停（当前语句用黄色标记）。 现在，可使用调试程序窗口（例如“局部变量”和“监视”窗口），通过将鼠标悬停在当前范围内的变量上来检查应用的状态   。

1. 按 F5 继续  。

1. 如果想要使用 Chrome 开发人员工具或 F12 工具，请按“F12”  。 可使用这些工具检查 DOM 并与使用 JavaScript 控制台的应用进行交互。

## <a name="debug-client-side-script"></a>调试客户端脚本

::: moniker range=">=vs-2019"
Visual Studio 仅为 Chrome 和 Microsoft Edge (Chromium) 提供客户端调试支持。 在某些情况下，调试器会自动命中 JavaScript 和 TypeScript 代码中以及 HTML 文件的嵌入脚本中的断点。 若要在 ASP.NET 应用中调试客户端脚本，请参阅博客文章[在 Microsoft Edge 中调试 JavaScript](https://devblogs.microsoft.com/visualstudio/debug-javascript-in-microsoft-edge-from-visual-studio/) 和 [Google Chrome 文章](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome)。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 仅为 Chrome 和 Internet 资源管理器提供客户端调试支持。 在某些情况下，调试器会自动命中 JavaScript 和 TypeScript 代码中以及 HTML 文件的嵌入脚本中的断点。 若要在 ASP.NET 应用中调试客户端脚本，请参阅博客文章[在 Google Chrome中对 ASP.NET 项目进行客户端调试](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/)。
::: moniker-end

对于 ASP.NET 以外的应用程序，请执行此处所述的步骤。

### <a name="prepare-your-app-for-debugging"></a>准备应用以进行调试

如果源是由 TypeScript 或 Babel 之类的转译器创建或经过其缩减，则需要使用[源映射](#generate_source_maps)以获得最佳调试体验。 如果没有源映射，仍可以将调试器附加到正在运行的客户端脚本。 但是，可能只能在缩减或转译的文件中设置和命中断点，而不能在原始源文件中设置和命中断点。 例如，在 Vue.js 应用中，缩减的脚本被作为字符串传递给 `eval` 语句，除非使用源映射，否则无法使用 Visual Studio 调试器有效地单步执行此代码。 在复杂的调试方案中，还可以改为使用 Chrome 开发人员工具或 Microsoft Edge 的 F12 工具。

为了帮助生成源映射，请参阅[生成用于调试的源映射](#generate_source_maps)。

### <a name="prepare_the_browser_for_debugging"></a> 准备浏览器以进行调试

::: moniker range=">=vs-2019"
对于此方案，请使用 Microsoft Edge (Chromium)（当前在 IDE 中命名为 Microsoft Edge Beta）或 Chrome  。
::: moniker-end
::: moniker range="vs-2017"
对于此方案，请选择 Chrome。
::: moniker-end

1. 关闭目标浏览器的所有窗口。

   其他浏览器实例可能会阻止打开浏览器并阻止调试。 （浏览器扩展可能正在运行并阻止完整的调试模式，因此你可能需要打开任务管理器才能找到意外的 Chrome 实例。）

   ::: moniker range=">=vs-2019"
   对于 Microsoft Edge (Chromium)，还需要关闭所有 Chrome 实例。 由于两个浏览器都使用 chromium 基本代码，因此可获得最佳结果。
   ::: moniker-end

2. 启动浏览器并启用调试。

    ::: moniker range=">=vs-2019"
    从 Visual Studio 2019 开始，可以在浏览器启动时设置 `--remote-debugging-port=9222` 标志，方法是从“调试”工具栏选择“浏览方式...”，然后选择“添加”，并在“参数”字段中设置标志     。 为浏览器使用其他易记名称，如“带有调试功能的 Edge”或“带有调试功能的 Chrome”   。 有关详细信息，请参阅[发行说明](/visualstudio/releases/2019/release-notes-v16.2)。

    ![将浏览器设置为打开并启用调试](../javascript/media/tutorial-nodejs-react-edge-with-debugging.png)

    或者，从 Windows“启动”按钮打开“运行”命令（右键单击并选择“运行”），然后输入以下命令    ：

    `msedge --remote-debugging-port=9222`

    或者，

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    ::: moniker range="vs-2017"
    从 Windows“启动”按钮打开“运行”命令（右键单击并选择“运行”），然后输入以下命令    ：

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    这样在启动浏览器时会同时启用调试。

    应用程序尚未运行，因此浏览器页面为空。

### <a name="attach-the-debugger-to-client-side-script"></a>将调试器附加到客户端脚本

若要从 Visual Studio 附加调试器并在客户端代码中命中断点，调试器需协助标识正确的进程。 以下是实现此目的的一种方法。

1. 切换到 Visual Studio，然后在源代码中设置断点，该断点可能是 JavaScript 文件、TypeScript 文件或 JSX 文件。 （在允许断点的代码行中设置断点，例如 return 语句或 var 声明。）

    ![设置断点](../javascript/media/tutorial-nodejs-react-set-breakpoint-client-code.png)

    若要在转译的文件中查找特定代码，请使用 Ctrl+F（“编辑” > “查找和替换” > “快速查找”）。     

    对于客户端代码，为了在 TypeScript 文件或 JSX 文件中命中断点，通常需要使用[源映射](#generate_source_maps)。 必须正确配置源映射，才支持在 Visual Studio 中进行调试。

2. 选择目标浏览器作为 Visual Studio 中调试目标，然后按 Ctrl+F5（“调试” > “启动时不调试”）在浏览器中运行应用     。

    ::: moniker range=">=vs-2019"
    如果创建了具有易记名称的浏览器配置，请选择该配置作为调试目标。
    ::: moniker-end

    应用随即在新的浏览器选项卡中打开。

3. 选择“调试” > “附加到进程”   。

    > [!TIP]
    > 从 Visual Studio 2017 开始，首次通过这些步骤附加到进程后，可选择“调试” > “重新附加到进程”，快速重新附加到同一进程   。

4. 在“附加到进程”  对话框中，获取可附加到的浏览器实例的筛选列表。

    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中，为“附加到”字段中的目标浏览器 JavaScript (Chrome) 或 JavaScript (Microsoft Edge - Chromium) 选择正确的调试器，在筛选器框中键入“chrome”或“edge”以筛选搜索结果      。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择“附加到”字段中的“WebKit 代码”，在筛选器框中键入“chrome”以筛选搜索结果    。
    ::: moniker-end

5. 使用正确的主机端口（此例中为 localhost）选择浏览器进程，然后选择“附加”  。

    端口（例如，1337）也可能出现在“标题”  字段中，以帮助你选择正确的浏览器实例。

    ::: moniker range=">=vs-2019"
    以下示例演示如何查找 Microsoft Edge (Chromium) 浏览器。

    ![附加到进程](../javascript/media/tutorial-nodejs-react-attach-to-process-edge.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![附加到进程](../javascript/media/tutorial-nodejs-react-attach-to-process.png)

    当 DOM 资源管理器和 JavaScript 控制台在 Visual Studio 中打开，表明已正确附加调试程序。 这些调试工具类似于 Chrome 开发人员工具和 Microsoft Edge 的 F12 工具。
    ::: moniker-end

    > [!TIP]
    > 如果未附加调试器，并且看到消息“无法启动调试适配器”或“无法附加到进程。 操作在当前状态中是非法的。”，则在调试模式中启用浏览器前，先使用 Windows 任务管理器关闭所有目标浏览器实例。 浏览器扩展可能正在运行并阻止完整的调试模式。

6. 由于可能已执行有断点的代码，因此要刷新浏览器页面。 如有必要，请采取操作来执行有断点的代码。

    在调试器中暂停时，可以通过在变量上悬停光标并使用调试器窗口，检查应用状态。 逐句通过代码（F5、F10 和 F11），推进调试器进度    。 有关基本调试功能的详细信息，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。

    你可能会在转译的 .js 文件或源文件中命中断点，具体取决于你之前按其步骤操作的应用类型以及浏览器状态等其他因素  。 无论在哪里命中，均可单步执行代码并检查变量。

   * 如果需要中断 TypeScript、JSX 或 .vue 源文件中的代码，但又无法执行此操作，请确保已正确设置环境，如[疑难解答故障排除](#troubleshooting_source_maps)部分所述  。

   * 如果需要中断转译的 JavaScript 文件中的代码（例如，“app-bundle.js”），但又无法执行此操作，请删除源映射文件“filename.js.map”   。

### <a name="troubleshooting_source_maps"></a> 断点和源映射故障排除

如果需要中断 TypeScript 或 JSX 源文件中的代码，但又无法执行此操作，请按照之前步骤中所述使用“附加到进程”来附加调试器  。 请确保已正确设置环境：

* 关闭了所有浏览器实例，包括 Chrome 扩展（使用任务管理器），以便你可以在调试模式下运行浏览器。
      
* 请确保[在调试模式下启动浏览器](#prepare_the_browser_for_debugging)。

* 请确保源映射文件包括指向源文件的正确相对路径，并确保该文件中没有不受支持的前缀（例如 webpack:///），这会阻止 Visual Studio 调试器查找源文件  。 例如，webpack:///.app.tsx 之类的引用可能会更正为 ./app.tsx   。 可在源映射文件（对测试很有用）中或通过自定义生成配置手动执行此操作。 有关详细信息，请参阅[生成用于调试的源映射](#generate_source_maps)。

或者，如果需要中断源文件中的代码（例如 app.tsx  ），但又无法执行此操作，可尝试使用源文件中的 `debugger;` 语句或改为在 Chrome 开发人员工具中设置断点（或 Microsoft Edge 的 F12 工具）。

## <a name="generate_source_maps"></a> 生成用于调试的源映射

Visual Studio 能够在 JavaScript 源文件上使用和生成源映射。 如果源由 TypeScript 或 Babel 之类的转译器创建或经过缩减，则通常需要这样做。 可用选项取决于项目类型。

* 默认情况下，Visual Studio 中的 TypeScript 项目会生成源映射。 有关详细信息，请参阅[使用 tsconfig.json 文件配置源映射](#configure_source_maps)。

* 在 JavaScript 项目中，可以使用像 webpack 这样的捆绑程序和像 TypeScript 编译器（或 Babel）这样的编译器来生成源映射，并可将其添加到项目中。 对于 TypeScript 编译器，还必须添加“tsconfig.json”文件并设置 `sourceMap` 编译器选项  。 有关如何使用基本 webpack 配置执行此操作的示例，请参阅[使用 React 创建 Node.js 应用](../javascript/tutorial-nodejs-with-react-and-jsx.md)。

> [!NOTE]
> 如果不熟悉源映射，请先阅读 [JavaScript 源映射简介](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)，然后再继续操作。 

若要配置源映射的高级设置，请使用“tsconfig.json”或 TypeScript 项目中的项目设置，但不能同时使用两者  。

若要使用 Visual Studio 启用调试，需要确保对生成的源映射中的源文件的引用正确（这可能需要进行测试）。 例如，如果使用的是 webpack，则源映射文件中的引用包括 webpack:/// 前缀，该前缀会阻止 Visual Studio 查找 TypeScript 或 JSX 源文件  。 具体而言，当你出于调试目的而更正此前缀时，必须将对源文件的引用（例如 app.tsx）从 webpack:///./app.tsx 之类的引用更改为 ./app.tsx 之类的引用，这样可启用调试（路径与源文件对应）    。 以下示例演示如何在 webpack（这是最常见的捆绑程序之一）中配置源映射，以便它们可以与 Visual Studio 配合工作。

（仅限 webpack）如果要在 TypeScript 或 JSX 文件（而不是转译的 JavaScript 文件）中设置断点，则需要更新 webpack 配置。 例如，在 webpack-config.js 中，可能需要替换以下代码  ：

```javascript
  output: {
    filename: "./app-bundle.js", // This is an example of the filename in your project
  },
```

替换为此代码：

```javascript
  output: {
    filename: "./app-bundle.js", // Replace with the filename in your project
    devtoolModuleFilenameTemplate: '[resource-path]'  // Removes the webpack:/// prefix
  },
```

此设置仅用于开发，可在 Visual Studio 中启用客户端代码调试。

对于复杂的方案，浏览器工具 (F12  ) 有时最适用于调试，因为它们不需要更改自定义前缀。

### <a name="configure_source_maps"></a> 使用 tsconfig.json 文件配置源映射

如果将“tsconfig.json”文件添加到项目中，Visual Studio 会将根目录视为 TypeScript 项目  。 若要添加文件，请在解决方案资源管理器中右键单击项目，然后选择“添加”>“新建项”>“TypeScript JSON 配置文件”  。 项目中随即添加类似于下面的“tsconfig.json”文件  。

```json
{
  "compilerOptions": {
    "noImplicitAny": false,
    "noEmitOnError": true,
    "removeComments": false,
    "sourceMap": true,
    "target": "es5"
  },
  "exclude": [
    "node_modules",
    "wwwroot"
  ]
}
```

#### <a name="compiler-options-for-tsconfigjson"></a>Tsconfig.json 的编译器选项

* **inlineSourceMap**：使用源映射发出单个文件，而不是为每个源文件创建单独的源映射。
* **inlineSources**：使用单个文件将源与源映射一起发出；需要设置“inlineSourceMap”或“sourceMap”   。
* **mapRoot**：指定调试器查找源映射 (.map) 文件的位置，不是默认位置  。 如果运行时 .map 文件需要位于与 .js 文件不同的位置，请使用此标志   。 指定的位置被嵌入到源映射中，以将调试器定向到“.map”文件的位置  。
* **sourceMap**：生成对应的“.map”文件  。
* **sourceRoot**：指定调试器查找 TypeScript 文件的位置，而不是源位置。 如果运行时源需要位于与设计时位置不同的位置，请使用此标志。 指定的位置被嵌入到源映射中，以将调试器定向到源文件所在的位置。

有关编译器选项的更多详细信息，请查看 TypeScript 手册上的[编译器选项](https://www.typescriptlang.org/docs/handbook/compiler-options.html)页。

### <a name="configure-source-maps-using-project-settings-typescript-project"></a>使用项目设置配置源映射（TypeScript 项目）

还可以使用项目属性配置源映射设置，方法是右键单击项目，然后选择“项目”>“属性”>“TypeScript 生成”>“调试”  。

以下项目设置可用。

* **生成源映射**（相当于“tsconfig.json”中的“sourceMap”）   ：生成对应的“.map”文件  。
* **指定源映射的根目录**（相当于“tsconfig.json”中的“mapRoot”）   ：指定调试器查找 map 文件的位置，而不是生成位置。 如果运行时“.map”文件需要位于与“.js”文件不同的位置，请使用此标志  。 指定的位置被嵌入到源映射中，以将调试器定向到映射文件所在的位置。
* **指定 TypeScript 文件的根目录**（相当于“tsconfig.json”中的“sourceRoot”）   ：指定调试器查找 TypeScript 文件的位置，而不是源位置。 如果运行时源文件需要位于与设计时位置不同的位置，请使用此标志。 指定的位置被嵌入到源映射中，以将调试器定向到源文件所在的位置。

## <a name="debug-javascript-in-dynamic-files-using-razor-aspnet"></a>使用 Razor (ASP.NET) 在动态文件中调试 JavaScript

::: moniker range=">=vs-2019"
从 Visual Studio 2019 开始，Visual Studio 仅为 Chrome 和 Microsoft Edge (Chromium) 提供调试支持。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 仅为 Chrome 和 Internet 资源管理器提供调试支持。
::: moniker-end

但是，不能在使用 Razor 语法（cshtml、vbhtml）生成的文件上自动命中断点。 有两种方法可用于调试此类型的文件：

* **将 `debugger;` 语句放在要中断的位置**：这会导致动态脚本在创建时停止执行并立即开始调试。
* **加载页面并在 Visual Studio 上打开动态文档**：需要在调试时打开动态文件、设置断点并刷新页面以使此方法起作用。 根据所使用的是 Chrome 还是 Internet Explorer，可以使用以下策略之一找到该文件：

   对于 Chrome，请转到“解决方案资源管理器”>“脚本文档”>“YourPageName”  。

    > [!NOTE]
    > 使用 Chrome，可能会收到一条消息：\<script> 标记之间没有可用源  。 这是正常的，只需继续调试即可。

   ::: moniker range=">=vs-2019"
   对于 Microsoft Edge (Chromium)，请使用与 Chrome 相同的进程。
   ::: moniker-end

   ::: moniker range="vs-2017"
   对于 Internet Explorer，请转至“解决方案资源管理器”>“脚本文档”>“Windows Internet Explorer”>“YourPageName”  。
   ::: moniker-end

有关详细信息，请参阅 [Google Chrome 中 ASP.NET 项目的客户端调试](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/)。
