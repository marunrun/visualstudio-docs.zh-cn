---
title: 编码的 UI 测试的配置和平台
ms.date: 10/04/2015
ms.topic: reference
helpviewer_keywords:
- coded UI tests
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: fd44fdc7e365bd07f25318740fb2dcc04fe0ea9d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926459"
---
# <a name="supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings"></a>支持编码的 UI 测试和操作录制的配置和平台

下表针对 Visual Studio Enterprise 列出了编码的 UI 测试支持的配置和平台。 这些配置也适用于使用 [!INCLUDE[MTRlong](../test/includes/mtrlong_md.md)]创建的操作录制。

> [!NOTE]
> 编码的 UI 测试进程必须具有与受测应用程序相同的特权。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**要求**

- Visual Studio Enterprise

## <a name="supported-configurations"></a>支持的配置

| 配置 | 支持 |
|-| - |
| 操作系统 | [!INCLUDE[win7](../debugger/includes/win7_md.md)]<br /><br /> [!INCLUDE[winsvr08_r2](../debugger/includes/winsvr08_r2_md.md)]<br /><br /> [!INCLUDE[win8](../debugger/includes/win8_md.md)]<br /><br /> Windows 10 |
| 32 位/64 位支持 | 运行 32 位 [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] 的 32 位 Windows 可测试 32 位应用程序。<br /><br /> 运行 32 位 [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] 的 64 位 Windows 可测试具有 UI 同步的 32 位 WOW 应用程序。<br /><br /> 运行 32 位 [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] 的 64 位 Windows 可测试不具有 UI 同步的 64 位 Windows 窗体和 WPF 应用程序。 |
| 体系结构 | x86 和 x64**注意：** 除非在 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本下运行，否则 Internet Explorer 在 64 位模式下不受支持。 |
| .NET | .NET 2.0、3.0、3.5、4 和 4.5。 **注意：** [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] 和 Visual Studio 都需要 .NET 4 才能运行。 但是，支持使用列出的 .NET 版本开发的应用程序。 |

> [!NOTE]
> UI 同步是一种功能，该功能在每个控件的消息队列中验证播放。  如果某个控件未响应发送给它的事件，则会重新发送该事件。

## <a name="platform-support"></a>平台支持

| Platform | 支持级别 |
|-| - |
| Windows Phone 应用 | 仅支持基于 WinRT-XAML 的 Phone 应用。 |
| UWP 应用 | 仅支持基于 XAML 的 UWP 应用。 |
| 通用 Windows 应用 | 仅支持手机和桌面上基于 XAML 的通用 Windows 应用。 |
| 边缘 | 不支持录制操作步骤或借助生成器来查看对象属性。 可使用 Visual Studio 2015 Update 2 及更高版本，通过[编码的 UI 跨浏览器测试扩展](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)在 Microsoft Edge 浏览器中播放测试。 |
| Internet Explorer 8<br /><br /> Internet Explorer 9<br /><br /> Internet Explorer 10 **重要说明：** Internet Explorer 10 仅在台式机上受支持。 <br /><br /> Internet Explorer 11 **重要说明：** Internet Explorer 11 仅在台式机上受支持。 | 完全支持。<br /><br /> -   **Internet Explorer 9 和 Internet Explorer 10 支持 HTML5：** 编码的 UI 测试支持对 HTML5 控件的录制、播放和验证：音频、视频、进度条和滑块。 有关详细信息，请参阅[在编码的 UI 测试中使用 HTML5 控件](../test/using-html5-controls-in-coded-ui-tests.md)。 **警告：**    如果你在 Internet Explorer 10 中创建编码的 UI 测试，则使用 Internet Explorer 9 或 Internet Explorer 8 可能无法运行它。 这是因为 Internet Explorer 10 包含 HTML5 控件（如音频、视频、进度条和滑块）。 Internet Explorer 9 或 Internet Explorer 8 无法识别这些 HTML5 控件。 同样，使用 Internet Explorer 9 的编码的 UI 测试可能包含 Internet Explorer 8 无法识别的某些 HTML5 控件。<br />-   **Internet Explorer 10 支持拼写检查：** Internet Explorer 10 包含所有文本框的拼写检查功能。 这使你可以从建议的更正的列表中进行选择。 编码的 UI 测试将忽略选择备选的拼写建议之类的用户操作。 只会记录键入到文本框中的最终文本。<br />     针对使用拼写检查控件的编码的 UI 测试记录以下操作：添加到字典、复制、全选、添加到字典和忽略。<br />-   **Windows 8 支持运行 64 位 Internet Explorer：** 以前，64 位版本的 Internet Explorer 不支持录制和播放。 在 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 和 [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)]中，已经为 64 位版本的 Internet Explorer 启用了编码的 UI 测试。 **警告：**    仅当你运行 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本时，对 Internet Explorer 的 64 位支持才适用。<br />-   **Internet Explorer 9 支持固定网站：** Internet Explorer 9 中引入了固定网站。 利用固定网站，你可直接从 Windows 工具栏访问你喜爱的网站，而无需先打开 Internet Explorer。 编码的 UI 测试现在可以在固定网站上生成意图感知操作。 有关固定网站的详细信息，请参阅[固定网站](http://go.microsoft.com/fwlink/?LinkId=220037)。<br />-   **Internet Explorer 9 支持语义标记：** Internet Explorer 9 引入以下语义标记：section、nav、article、aside、hgroup、header、footer、figure、figcaption 和 mark。 编码的 UI 测试在录制过程中会忽略所有这些语义标记。 你可使用编码的 UI 测试生成器在这些标记上添加断言。 你可使用编码的 UI 测试生成器中的导航刻度盘来导航至任一这些元素并查看其属性。<br />-   **无缝处理 Internet Explorer 各版本之间的空白字符：** Internet Explorer 8、Internet Explorer 9 和 Internet Explorer 10 处理空白字符的方式各不相同。 编码的 UI 测试可无缝地处理这些差异。 因此，在 Internet Explorer 8（举例来说）中创建的编码的 UI 测试可在 Internet Explorer 9 和 Internet Explorer 10 中成功播放。<br />-   **现在可通过“出错时继续”属性集记录 Internet Explorer 的通知区域：** 现在可通过“出错时继续”属性集记录 Internet Explorer 的通知区域上的所有操作。 如果在播放过程中未显示通知栏，则将忽略针对它的操作，并且编码的 UI 测试将继续下一个操作。 |
| Windows 窗体和 WPF 第三方控件 | 完全支持。<br /><br /> 若要在 Windows 窗体和 WPF 应用程序中启用第三方控件，则必须添加引用和代码。 有关详细信息，请参阅[启用控件的编码的 UI 测试](../test/enable-coded-ui-testing-of-your-controls.md)。 |
| Internet Explorer 6<br /><br /> Internet Explorer 7 | 不支持。 |
| Chrome<br /><br /> Firefox | 不支持操作步骤的录制。 利用 Visual Studio 2012 Update 4 或更高版本，编码的 UI 测试可在 Chrome 和 Firefox 浏览器中播放。 有关更多详细信息，请转到 [此处](using-different-web-browsers-with-coded-ui-tests.md) 。 |
| Opera<br /><br /> Safari | 不支持。 |
| Silverlight | 不支持。<br /><br /> 对于 Visual Studo 2013，可从 Visual Studio 库下载[用于 Silverlight 的 Microsoft Visual Studio 2013 编码的 UI 测试插件](https://go.microsoft.com/fwlink/?LinkId=691026)。 |
| Flash/Java | 不支持。 |
| Windows 窗体 2.0 及更高版本 | 完全支持。 **注意：** 完全支持 NetFx 控件，但并非支持所有第三方控件。 |
| WPF 3.5 及更高版本 | 完全支持。<br /><br /> **注意** NetFx 控件完全受支持，但并非所有第三方控件都受支持。 |
| Windows Win32 | 可适用于某些已知问题，但不正式支持。 |
| MFC | 部分支持。 有关支持功能的详细信息，请参阅 [UITest 框架](https://blogs.msdn.microsoft.com/vstsqualitytools/2010/04/15/uitest-framework-mfc-support-in-vs-2010/)。 |
| SharePoint | 完全支持。 |
| Office 客户端应用程序 | 不支持。 |
| Dynamics CRM Web 客户端 | 完全支持。 |
| Dynamics (Ax) 2012 客户端 | 操作录制和播放部分受支持。 有关详细信息，请参阅[适用于 Microsoft Dynamics 的 Visual Studio 10 编码的 UI/操作录制支持](https://blogs.msdn.microsoft.com/dave_froslie/2011/09/01/visual-studio-10-coded-ui-action-recordings-support-for-microsoft-dynamics-ax-2012/)。 |
| SAP | 不支持。 |
| Citrix/终端服务 | 不建议在终端服务器上录制操作。 记录器不支持同时运行多个实例。 |
| PowerBuilder | 部分支持。<br /><br /> 支持取决于为 PowerBuilder 控件启用的可访问性。 |

有关如何创建扩展以支持其他平台的信息，请参阅[启用控件的编码的 UI 测试](../test/enable-coded-ui-testing-of-your-controls.md)和[扩展编码的 UI 测试和操作录制](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)。

## <a name="see-also"></a>请参阅

- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
