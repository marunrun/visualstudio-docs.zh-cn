---
title: 调试 WebView 控件 (UWP) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 7d105907-8b39-4d07-8762-5c5ed74c7f21
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: 43d545a52cbe066e4bb5002b57e9539b9a1b303c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402631"
---
# <a name="debug-a-webview-control-in-a-uwp-app"></a>调试 UWP 应用中的 WebView 控件

 若要检查并调试 Windows 运行时应用中的 `WebView` 控件，可以配置 Visual Studio，使其在你启动应用时附加脚本调试器。 使用调试器与 `WebView` 控件交互的方式有两种：

- 打开 `WebView` 实例的 [DOM 资源管理器](../debugger/quickstart-debug-html-and-css.md)，然后检查 DOM 元素、调查 CSS 样式问题并测试动态呈现的样式的更改。

- 选择网页或`iFrame`中显示`WebView`实例中的目标作为[JavaScript 控制台](../debugger/javascript-console-commands.md)窗口中，然后与使用控制台命令的网页进行交互。 控制台提供对当前脚本执行上下文的访问。

### <a name="attach-the-debugger-c-visual-basic-c"></a>附加调试器（C#、Visual Basic、C++）

1. 在 Visual Studio 中，向 Windows 运行时应用添加 `WebView` 控件。

2. 在解决方案资源管理器中，通过从项目的快捷菜单中选择“属性”来打开项目的属性。

3. 选择“调试”。 在“应用程序进程”列表中，选择“脚本”。

     ![附加脚本调试器](../debugger/media/js_dom_webview_script_debugger.png "JS_DOM_WebView_Script_Debugger")

4. （可选）对于不是 Express 版本的 Visual Studio，可通过选择“工具”>“选项”>“调试”>“实时”，然后禁用脚本的 JIT 调试，来禁用实时 (JIT) 调试。

    > [!NOTE]
    > 对于某些网页上发生的无法处理的异常，你可以通过禁用 JIT 调试来隐藏对话框。 在 Visual Studio Express 中，JIT 调试始终处于禁用状态。

5. 按 F5 开始调试。

### <a name="use-the-dom-explorer-to-inspect-and-debug-a-webview-control"></a>使用 DOM 资源管理器以检查并调试 WebView 控件

1. （C#、Visual Basic、C++）向你的应用附加脚本调试器。 请参见第一部分以获取说明。

2. 若没有 `WebView` 控件，请向应用添加该控件并按 F5 启动调试。

3. 导航到包含 `Webview` 控件的页面。

4. 打开的 DOM 资源管理器窗口`WebView`通过选择控件**调试**， **Windows**， **DOM 资源管理器**，然后选择的 URL`WebView`你想要检查。

     ![打开 DOM 资源管理器](../debugger/media/js_dom_webview.png "JS_DOM_WebView")

     与 `WebView` 关联的 DOM 资源管理器将在 Visual Studio 中显示为新选项卡。

5. 查看和修改实时 DOM 元素和 CSS 样式，如中所述[使用 DOM 资源管理器调试 CSS 样式](/visualstudio/debugger/quickstart-debug-html-and-css)。

### <a name="use-the-javascript-console-window-to-inspect-and-debug-a-webview-control"></a>使用 JavaScript 控制台窗口以检查并调试 WebView 控件

1. （C#、Visual Basic、C++）向你的应用附加脚本调试器。 请参见第一部分以获取说明。

2. 若没有 `WebView` 控件，请向应用添加该控件并按 F5 启动调试。

3. 打开的 JavaScript 控制台窗口`WebView`通过选择控件**调试**， **Windows**， **JavaScript 控制台**。

     将显示“JavaScript 控制台”窗口。

4. 导航到包含 `Webview` 控件的页面。

5. 在控制台窗口中，选择网页或`iFrame`情况下显示`WebView`控制**目标**列表。

     ![面向 JavaScript 控制台窗口中的选择](../debugger/media/js_console_target.png "JS_Console_Target")

    > [!NOTE]
    > 通过使用控制台，可以与单个 `WebView`、`iFrame` 交互，每次还可以共享协定或 Web Worker。 每个元素都需要单独的 Web 平台主机 (WWAHost.exe) 的实例。 一次可与一个主机交互。

6. 查看和修改应用程序中的变量或使用控制台命令，如中所述[快速入门：调试 JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md)并[JavaScript 控制台命令](../debugger/javascript-console-commands.md)。

## <a name="see-also"></a>请参阅

- [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)