---
title: 在不同的 Web 浏览器中运行编码的 UI 测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: a859595f-6517-43f2-9d61-c706cb55a388
caps.latest.revision: 25
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d9c86125d934c5165e3e8111fdd06631844ad1a6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297963"
---
# <a name="using-different-web-browsers-with-coded-ui-tests"></a>对编码的 UI 测试使用不同的 Web 浏览器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编码的 UI 测试可通过使用 Internet Explorer 记录你的测试来自动化 Web 应用程序的测试。 然后，你可以自定义你的测试并使用 Internet Explorer 或其他适用于这些 Web 应用程序的浏览器类型来播放测试。

 **惠?**

- Visual Studio Enterprise

- 操作系统：

  - Microsoft Windows 7

  - Microsoft Windows 8

  - Microsoft Windows Server 2008 R2 SP1

- Web 浏览器版本：

  - Windows Internet Explorer 9

  - Windows Internet Explorer 10

  - 有关 Mozilla Firefox 和 Google Chrome 的受支持版本，请转到[此处](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)

- 安装[用于编码的 UI 跨浏览器测试的 Selenium 组件](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)。

  **哪些是所有 Web 浏览器都支持的功能？**

- [添加用于控制功能（如属性、搜索和播放等待应用）的自定义代码](https://devblogs.microsoft.com/devops/coded-ui-test-configuring-search-properties-while-recording-on-internet-explorer/)。

- 弹出窗口和对话框

- [执行不含返回类型的基本 JavaScript](https://devblogs.microsoft.com/devops/introducing-javascript-execution-on-internetexplorer-and-crossbrowser-in-coded-ui-test/)

- 搜索恢复能力（使用智能匹配）和[性能提升](https://devblogs.microsoft.com/devops/guidelines-on-improving-performance-of-coded-ui-test-playback/)

## <a name="why-should-i-use-coded-ui-tests-across-multiple-web-browser-types"></a>为什么应在多个 Web 浏览器类型中使用编码的 UI 测试?
 通过使用各种 Web 浏览器类型测试你的 Web 应用程序，你可以更好地模拟可能运行不同浏览器的用户的 UI 体验。 例如，你的应用程序可能包含 Internet Explorer 中与其他 Web 浏览器不兼容的控件或代码。 通过在其他浏览器中运行编码的 UI 测试，你可以在任何问题对客户产生影响前发现并更正它。

## <a name="how-do-i-record-and-play-back-coded-ui-tests-on-web-applications-using-the-supported-web-browsers"></a>如何使用支持的 Web 浏览器在 Web 应用程序上记录和播放编码的 UI 测试?
 **录制：** 必须使用编码的 UI 测试生成器来录制在 Internet Explorer 中运行的 Web 应用测试。 你可以选择使用一组预定义的属性为已测试的控件添加验证和自定义代码，这与你通常对编码的 UI 测试所做的一样。 有关详细信息，请参阅[使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)。

> [!NOTE]
> 你无法使用 Google Chrome 或 Mozilla Firefox 浏览器记录编码的 UI 测试。

 **使用 Internet Explorer 播放：** 如果未显式指定浏览器，默认将在 Internet Explorer 中运行测试。 可以在测试代码中设置 **BrowserWindow.CurrentBrowser** 属性来显式声明要使用的浏览器。 对于 Internet Explorer，应将此属性设为“IE”或“Internet Explorer”。

 **使用非 Internet Explorer Web 浏览器播放：** 若要在非 Internet Explorer Web 浏览器中播放，请将测试代码中的 BrowserWindow.CurrentBrowser 属性更改为“Firefox”或“Chrome”。

 必须**用于编码的 UI 跨浏览器测试的 Selenium 组件**，才能在非 IE 浏览器上播放测试。

#### <a name="installing-selenium-components"></a>安装 Selenium 组件

1. 在“工具” 菜单上，选择“扩展和更新”。

2. 在“扩展和更新”对话框中，搜索“`Selenium components for Cross Browser Testing`”。

3. 依次选择扩展和“下载”。

   > [!TIP]
   > 还可以从[此处](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)下载用于编码的 UI 跨浏览器测试的 Selenium 组件。

   若要详细了解如何创建和使用编码的 UI 测试，请参阅[创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)。

### <a name="enable-debugging"></a>启用调试
 若要能够调试 Web 应用程序，则必须完成以下配置选项：

1. 启用“仅我的代码”：

    1. 在“工具”菜单上，依次选择“选项”和“调试”。

    2. 选择“启用‘仅我的代码’”。

2. 禁用 CLR 异常：

    1. 选择“调试”菜单上的“异常”。

    2. 对于“公共语言运行时异常”，请取消选中“用户未处理的”。

## <a name="generate"></a>*在编码的 UI 测试中我看不到用于更改 BrowserWindow.CurrentBrowser 的选项。*
 你使用的 [!INCLUDE[vs2011_first](../includes/vs2011-first-md.md)] 版本可能不支持使用各种 Web 浏览器的编码的 UI 测试。 若要使用此类编码的 UI 测试，你必须使用 Visual Studio Enterprise。

 *我还应该知道什么？*
 **注意**

- ![Prerequsite](../test/media/prereq.png "Prereq") Apple Safari web browser is not supported.

- ![Prerequsite](../test/media/prereq.png "Prereq") The action of starting the web browser must be part of the coded UI test.

   如果你已打开 Web 浏览器并想在其中运行步骤，则播放将失败，除非你使用 Internet Explorer。 因此，最佳做法是将 Web 浏览器的启动操作作为编码的 UI 测试的一部分。

- ![Prerequsite](../test/media/prereq.png "Prereq") Automating browser specific based UI actions such as maximize, minimize and restore is not supported.

  **提示**

- ![Tip](../test/media/tip.png "提示") You can configure the output to include screenshots in the coded UI logs. 为此，你需要在 QTAgent32.exe.config 文件中设置某些配置设置。 默认情况下，该文件安装在以下位置：

   **C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE**

   设置下列值：

  - `EqtTraceLevel` 部分中的 `system.diagnostics`。

  - `<add name="EqtTraceLevel" value="4" />`

     通过将值设置为 3 或更大，可为每个操作拍摄屏幕快照。 当该值设置为 1 或 2 时，仅为错误操作拍摄屏幕快照。

    有关详细信息，请参阅[使用编码的 UI 测试日志分析编码的 UI 测试](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)。

## <a name="external-resources"></a>外部资源

### <a name="videos"></a>视频
 [在 IE 上录制并在所有位置上播放](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!183&authkey=!ANqaLtCZbtJrImU)

 [使用编码的 UI 测试生成器创作跨浏览器测试](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!184&authkey=!AKG8CSow_qmeTq8)

 [使用不含 UI 映射的纯手工编码创作跨浏览器测试](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!186&authkey=!AJaEvxJnsefyAT4)

 [在多个浏览器上依序运行跨浏览器测试](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!187&authkey=!ADI8eCQkxHnpOR8)

 [跨浏览器测试问题排查](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!182&authkey=!AEpS48i295B49FI)

### <a name="guidance"></a>指导
 [使用 Visual Studio 2012 对连续交付进行测试 - 第 2 章：单元测试：测试内部](https://go.microsoft.com/fwlink/?LinkID=255188)

 [使用 Visual Studio 2012 测试持续交付 - 第 5 章：实现系统测试的自动化](https://go.microsoft.com/fwlink/?LinkID=255196)

### <a name="faq"></a>FAQ
 [编码的 UI 测试常见问题 - 1](https://go.microsoft.com/fwlink/?LinkID=230576)

 [编码的 UI 测试常见问题 - 2](https://go.microsoft.com/fwlink/?LinkID=230578)

### <a name="forum"></a>论坛
 [Visual Studio UI 自动测试（包括编码的 UI）](https://go.microsoft.com/fwlink/?LinkID=224497)

## <a name="see-also"></a>请参阅
 [Use UI Automation To Test Your Code](../test/use-ui-automation-to-test-your-code.md) [Supported Configurations and Platforms for Coded UI Tests and Action Recordings](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md) [Analyzing Coded UI Tests Using Coded UI Test Logs](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)
