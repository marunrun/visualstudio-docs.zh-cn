---
title: 调试 JavaScript 或 TypeScript 应用
description: Visual Studio 支持在 Visual Studio 中调试 JavaScript 和 TypeScript 应用
ms.date: 12/03/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 47f709ae086a32c0680fca060744898251a76afd
ms.sourcegitcommit: 8a96a65676fd7a2a03b0803d7eceae65f3fa142b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72589135"
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

Visual Studio 仅为 Chrome 和 Internet 资源管理器提供调试支持。 在某些情况下，调试器会自动命中 JavaScript 和 TypeScript 代码中以及 HTML 文件的嵌入脚本中的断点。

如果源是由 TypeScript 或 Babel 之类的转译器创建或经过其缩减，则需要使用[源映射](#generate_sourcemaps)以获得最佳调试体验。 如果没有源映射，仍可以将调试器附加到正在运行的客户端脚本。 但是，可能只能在缩减或转译的文件中设置和命中断点，而不能在原始源文件中设置和命中断点。 例如，在 Vue.js 应用中，缩减的脚本被作为字符串传递给 `eval` 语句，除非使用源映射，否则无法使用 Visual Studio 调试器有效地单步执行此代码。 在某些复杂的调试方案中，还可以使用 Chrome 开发人员工具或 Microsoft Edge 的 F12 工具。

若要从 Visual Studio 附加调试器并在客户端代码中命中断点，调试器通常需要协助标识正确的进程。 以下是使用 Chrome 实现此目的的一种方法。

### <a name="attach-the-debugger-to-client-side-script-using-chrome"></a>使用 Chrome 将调试器附加到客户端脚本

1. 关闭所有 Chrome 窗口。

    在调试模式下运行 Chrome 之前，必须执行此操作。

2. 从 Windows“启动”按钮打开“运行”命令（右键单击并选择“运行”），然后输入以下命令    ：

    `chrome.exe --remote-debugging-port=9222`

    此命令在启动 Chrome 时会同时启用调试。

    ::: moniker range=">=vs-2019"

    > [!NOTE]
    > 还可以在浏览器启动时设置 `--remote-debugging-port` 标志，方法是从“调试”工具栏选择“浏览方式...”，然后选择“添加”，并在“参数”字段中设置标志     。 为浏览器使用其他易记名称，如“带有调试功能的 Chrome”  。 有关详细信息，请参阅[发行说明](https://docs.microsoft.com/visualstudio/releases/2019/release-notes-preview)。

    ::: moniker-end

3. 切换到 Visual Studio 并在源代码中设置断点。 （在允许断点的代码行中设置断点，例如 `return` 语句或 `var` 声明）。

    ![设置断点](../javascript/media/tutorial-nodejs-react-set-breakpoint-client-code.png)

    如果需要在生成的大型文件中查找特定代码，请使用“Ctrl”+“F”（“编辑” > “查找和替换” > “快速查找”）      。

4. 在选择 Chrome 作为 Visual Studio 中调试目标的情况下，按 Ctrl+F5（“调试” > “启动时不调试”）在浏览器中运行应用     。

    应用随即在新的浏览器选项卡中打开。

    如果计算机上有 Chrome，但未显示为选项，请从调试目标下拉列表中选择  “浏览方式”，然后选择 Chrome 作为默认浏览器目标（选择“设为默认值”  ）。

5. 选择“调试” > “附加到进程”   。

6. 在“附加到进程”对话框中，选择“附加到”字段中的“WebKit 代码”，在筛选框中键入“chrome”以筛选搜索结果     。

    “WebKit 代码”是 Chrome 的必需值，Chrome 是一个基于 WebKit 的浏览器  。

7. 使用正确的主机端口（此图中为 1337）选择 Chrome 进程，然后选择“附加”  。

    ![附加到进程](../javascript/media/tutorial-nodejs-react-attach-to-process.png)

    ::: moniker range="vs-2017"
    当 DOM 资源管理器和 JavaScript 控制台在 Visual Studio 中打开，表明已正确附加调试程序。 这些调试工具类似于 Chrome 开发人员工具和 Microsoft Edge 的 F12 工具。
    ::: moniker-end

    > [!NOTE]
    > 如果未附加调试程序，则会看到消息“无法附加到进程。 操作在当前状态中是非法的。在调试模式中启用 Chrome 前，先使用任务管理器关闭所有 Chrome 实例。 Chrome 扩展可能正在运行并阻止完整的调试模式。

8. 如果已执行有断点的代码，刷新浏览器页面以命中断点。

    在调试器中暂停时，可以通过在变量上悬停光标并使用调试器窗口，检查应用状态。 逐句通过代码（F5、F10 和 F11），推进调试器进度    。

    对于缩减或转译的 JavaScript，可以在转译的 JavaScript 中或 TypeScript 文件中断点的映射位置（使用源映射）处命中断点，具体取决于环境和浏览器状态。 无论在哪里命中，均可单步执行代码并检查变量。

    * 如果需要中断 TypeScript 文件中的代码但又无法执行此操作，请按照之前所述的步骤，使用“附加到进程”来附加调试程序  。 然后通过打开“脚本文档” > “filename.tsx”，从解决方案资源管理器打开动态生成“TypeScript”文件，设置断点并刷新浏览器中的页面（在允许断点的代码行中设置断点，如 `return` 语句或 `var` 声明）   。

        或者，如果需要中断 TypeScript 文件中的代码但又无法执行此操作，可尝试使用 TypeScript 文件中的 `debugger;` 语句或改为在 Chrome 开发人员工具中设置断点。

    * 如果需要中断转译的 JavaScript 文件中的代码（例如，“app-bundle.js”），但又无法执行此操作，请删除源映射文件“filename.js.map”   。

     > [!TIP]
     > 首次通过这些步骤附加到进程后，可选择“调试” > “重新附加到进程”，快速重新附加到同一进程   。

## <a name="generate_sourcemaps"></a> 生成用于调试的源映射

Visual Studio 能够在 JavaScript 源文件上使用和生成源映射。 如果源由 TypeScript 或 Babel 之类的转译器创建或经过缩减，则通常需要这样做。 可用选项取决于项目类型。

* 默认情况下，Visual Studio 中的 TypeScript 项目会生成源映射。

* 在 JavaScript 项目中，需要使用像 webpack 这样的捆绑程序和像 TypeScript 编译器（或 Babel）这样的编译器来生成源映射，并可将其添加到项目中。 对于 TypeScript 编译器，还必须添加“tsconfig.json”文件  。 有关如何使用基本 webpack 配置执行此操作的示例，请参阅[使用 React 创建 Node.js 应用](../javascript/tutorial-nodejs-with-react-and-jsx.md)。

> [!NOTE]
> 如果不熟悉源映射，请先阅读 [JavaScript 源映射简介](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)，然后再继续操作。

若要配置源映射的高级设置，请使用“tsconfig.json”或 TypeScript 项目中的项目设置，但不能同时使用两者  。

### <a name="configure-source-maps-using-a-tsconfigjson-file"></a>使用 tsconfig.json 文件配置源映射

如果将“tsconfig.json”文件添加到项目中，Visual Studio 会将根目录视为 TypeScript 项目  。 若要添加文件，请在解决方案资源管理器中右键单击项目，然后选择“添加”>“新建项”>“Web”>“脚本”>“TypeScript JSON 配置文件”  。 项目中随即添加类似于下面的“tsconfig.json”文件  。

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

### <a name="configure-source-maps-using-project-settings"></a>使用项目设置配置源映射

还可以使用项目属性配置源映射设置，方法是右键单击项目，然后选择“项目”>“属性”>“TypeScript 生成”>“调试”  。

以下项目设置可用。

* **生成源映射**（相当于“tsconfig.json”中的“sourceMap”）   ：生成对应的“.map”文件  。
* **指定源映射的根目录**（相当于“tsconfig.json”中的“mapRoot”）   ：指定调试器查找 map 文件的位置，而不是生成位置。 如果运行时“.map”文件需要位于与“.js”文件不同的位置，请使用此标志  。 指定的位置被嵌入到源映射中，以将调试器定向到映射文件所在的位置。
* **指定 TypeScript 文件的根目录**（相当于“tsconfig.json”中的“sourceRoot”）   ：指定调试器查找 TypeScript 文件的位置，而不是源位置。 如果运行时源文件需要位于与设计时位置不同的位置，请使用此标志。 指定的位置被嵌入到源映射中，以将调试器定向到源文件所在的位置。

## <a name="debug-javascript-in-dynamic-files-using-razor-aspnet"></a>使用 Razor (ASP.NET) 在动态文件中调试 JavaScript

Visual Studio 仅为 Chrome 和 Internet 资源管理器提供调试支持。 它会自动将断点附加到 HTML 文件上的 JavaScript/TypeScript 和嵌入的脚本中。

不会自动调试动态生成的文件。 不能在使用 Razor 语法（cshtml、vbhtml）生成的文件上自动命中断点。 有两种方法可用于调试此类型的文件：

* **将 `debugger;` 语句放在要中断的位置**：这会导致动态脚本在创建时停止执行并立即开始调试。
* **加载页面并在 Visual Studio 上打开动态文档**：需要在调试时打开动态文件、设置断点并刷新页面以使此方法起作用。 根据所使用的是 Chrome 还是 Internet Explorer，可以使用以下策略之一找到该文件：

   对于 Chrome，请转到“解决方案资源管理器”>“脚本文档”>“YourPageName”  。

    > [!NOTE]
    > 使用 Chrome，可能会收到一条消息：\<script> 标记之间没有可用源  。 这是正常的，只需继续调试即可。

   对于 Internet Explorer，请转至“解决方案资源管理器”>“脚本文档”>“Windows Internet Explorer”>“YourPageName”  。

有关详细信息，请参阅 [Google Chrome 中 ASP.NET 项目的客户端调试](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/)。