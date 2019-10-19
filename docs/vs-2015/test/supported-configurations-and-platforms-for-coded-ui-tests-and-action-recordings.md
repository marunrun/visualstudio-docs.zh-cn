---
title: 支持编码的 UI 测试和操作录制的配置和平台 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests
ms.assetid: 544742b5-4ec1-4d51-b941-72b2f6ff17bc
caps.latest.revision: 108
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 147c15baf8f089bf41262e04694bce8b5b44f31e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660413"
---
# <a name="supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings"></a>支持编码的 UI 测试和操作录制的配置和平台
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下表针对 Visual Studio Enterprise 列出了编码的 UI 测试支持的配置和平台。 这些配置也适用于使用 [!INCLUDE[MTRlong](../includes/mtrlong-md.md)]创建的操作录制。

> [!NOTE]
> 编码的 UI 测试进程必须具有与受测应用程序相同的特权。

 **惠?**

- Visual Studio Enterprise

## <a name="supported-configurations"></a>支持的配置

|配置|支持|
|-------------------|---------------|
|操作系统|[!INCLUDE[win7](../includes/win7-md.md)]<br /><br /> [!INCLUDE[winsvr08_r2](../includes/winsvr08-r2-md.md)]<br /><br /> [!INCLUDE[win8](../includes/win8-md.md)]<br /><br /> Windows 10|
|32 位/64 位支持|运行 32 位 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 的 32 位 Windows 可测试 32 位应用程序。<br /><br /> 运行 32 位 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 的 64 位 Windows 可测试具有 UI 同步的 32 位 WOW 应用程序。<br /><br /> 运行 32 位 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 的 64 位 Windows 可测试不具有 UI 同步的 64 位 Windows 窗体和 WPF 应用程序。|
|体系结构|x86 和 x64 **注意：** 除非在 [!INCLUDE[win8](../includes/win8-md.md)] 或更高版本下运行，否则 Internet Explorer 在 64 位模式下不受支持。|
|.NET|.NET 2.0、3.0、3.5、4 和 4.5。 **注意：** [!INCLUDE[TCMext](../includes/tcmext-md.md)] 和 Visual Studio 都需要 .NET 4 才能运行。 但是，支持使用列出的 .NET 版本开发的应用程序。|

> [!NOTE]
> UI 同步是一种功能，该功能在每个控件的消息队列中验证播放。 如果某个控件未响应发送给它的事件，则会重新发送该事件。

## <a name="platform-support"></a>平台支持

|Platform|支持级别|
|--------------|----------------------|
|Windows Phone 应用|仅支持基于 WinRT-XAML 的 Phone 应用。|
|Windows 应用商店应用|仅支持基于 XAML 的应用商店应用。|
|通用 Windows 应用|仅支持手机和桌面上基于 XAML 的通用 Windows 应用。|
|边缘|在 Visual Studio 2015 Update 2 以及更高版本中，使用[跨浏览器测试扩展的编码的 UI](https://visualstudiogallery.msdn.microsoft.com/11cfc881-f8c9-4f96-b303-a2780156628d)|
|Internet Explorer 8<br /><br /> Internet Explorer 9<br /><br /> Internet Explorer 10 **重要提示：** Internet Explorer 10 仅在台式机上受支持。 <br /><br /> Internet Explorer 11 **重要提示：** Internet Explorer 11 仅在台式机上受支持。|完全支持。<br /><br /> -   **对 Internet Explorer 9 和 Internet Explorer 10 中的 HTML5 的支持：** 编码的 UI 测试支持 HTML5 控件（音频、视频、进度条和滑块）的录制、播放和验证。 有关详细信息，请参阅[在编码的 UI 测试中使用 HTML5 控件](../test/using-html5-controls-in-coded-ui-tests.md)。 **警告：** 如果你在 Internet Explorer 10 中创建编码的 UI 测试，则使用 Internet Explorer 9 或 Internet Explorer 8 可能无法运行它。 这是因为 Internet Explorer 10 包含 HTML5 控件（如音频、视频、进度条和滑块）。 Internet Explorer 9 或 Internet Explorer 8 无法识别这些 HTML5 控件。 同样，使用 Internet Explorer 9 的编码的 UI 测试可能包含 Internet Explorer 8 无法识别的某些 HTML5 控件。<br />-   **对 Internet Explorer 10 拼写检查的支持：** Internet Explorer 10 包含对所有文本框的拼写检查功能。 这使你可以从建议的更正的列表中进行选择。 编码的 UI 测试将忽略选择备选的拼写建议之类的用户操作。 只会记录键入到文本框中的最终文本。<br />     将为使用拼写检查控件的编码的 UI 测试记录以下操作：“添加到字典”、“复制”、“全选”和“忽略”。<br />-   **对在 Windows 8 下运行的 64 位 Internet Explorer 的支持：** 以前，64 位版本的 Internet Explorer 不支持录制和播放。 在 [!INCLUDE[win8](../includes/win8-md.md)] 和 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 中，已经为 64 位版本的 Internet Explorer 启用了编码的 UI 测试。 **警告：** 仅当你运行 [!INCLUDE[win8](../includes/win8-md.md)] 或更高版本时，对 Internet Explorer 的 64 位支持才适用。<br />-   **对 Internet Explorer 9 中的固定网站的支持：** Internet Explorer 9 中引入了固定网站。 利用固定网站，你可直接从 Windows 工具栏访问你喜爱的网站，而无需先打开 Internet Explorer。 编码的 UI 测试现在可以在固定网站上生成意图感知操作。 有关固定网站的详细信息，请参阅 [固定网站](http://go.microsoft.com/fwlink/?LinkId=220037)。<br />-   **对 Internet Explorer 9 语义标记的支持：** Internet Explorer 9 引入以下语义标记：section、nav、article、aside、hgroup、header、footer、figure、figcaption 和 mark。 编码的 UI 测试在录制过程中会忽略所有这些语义标记。 你可使用编码的 UI 测试生成器在这些标记上添加断言。 你可使用编码的 UI 测试生成器中的导航刻度盘来导航至任一这些元素并查看其属性。<br />-   **各个版本的 Internet Explorer 之间的空白字符的无缝处理：** Internet Explorer 8、Internet Explorer 9 和 Internet Explorer 10 的空白字符的处理方式各不相同。 编码的 UI 测试可无缝地处理这些差异。 因此，在 Internet Explorer 8（举例来说）中创建的编码的 UI 测试可在 Internet Explorer 9 和 Internet Explorer 10 中成功播放。<br />-   **Internet Explorer 的通知区域现在在进行录制时会设置“出错时继续”特性：** Internet Explorer 的通知区域中的所有操作现在在进行录制时会设置“出错时继续”特性。 如果在播放过程中未显示通知栏，则将忽略针对它的操作，并且编码的 UI 测试将继续下一个操作。|
|Windows 窗体和 WPF 第三方控件|完全支持。<br /><br /> 若要在 Windows 窗体和 WPF 应用程序中启用第三方控件，则必须添加引用和代码。 有关详细信息，请参阅[启用控件的编码的 UI 测试](../test/enable-coded-ui-testing-of-your-controls.md)。|
|Internet Explorer 6<br /><br /> Internet Explorer 7|不支持。|
|Chrome<br /><br /> Firefox|不支持操作步骤的录制。 利用 Visual Studio 2012 Update 4 或更高版本，编码的 UI 测试可在 Chrome 和 Firefox 浏览器中播放。 有关更多详细信息，请转到 [此处](https://msdn.microsoft.com/library/jj835758.aspx) 。|
|Opera<br /><br /> Safari|不支持。|
|Silverlight|不支持。<br /><br /> 对于 Visual Studo 2013，你可从 Visual Studio 库下载 [用于 Silverlight 的 Microsoft Visual Studio 2013 编码 UI 测试插件](https://go.microsoft.com/fwlink/?LinkId=691026) 。|
|Flash/Java|不支持。|
|Windows 窗体 2.0 及更高版本|完全支持。 **注意：** NetFx 控件完全受支持，但并非所有第三方控件都受支持。|
|WPF 3.5 及更高版本|完全支持。<br /><br /> **注意** NetFx 控件完全受支持，但并非所有第三方控件都受支持。|
|Windows Win32|可适用于某些已知问题，但不正式支持。|
|MFC|部分支持。 有关受支持的功能的详细信息，请参阅以下 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkId=206511) 。|
|SharePoint|完全支持。|
|Office 客户端应用程序|不支持。|
|Dynamics CRM Web 客户端|完全支持。|
|Dynamics (Ax) 2012 客户端|操作录制和播放部分受支持。 有关详细信息，请参阅以下 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkId=232677) 。|
|SAP|不支持。|
|Citrix/终端服务|我们不建议在终端服务器上录制操作。 记录器不支持同时运行多个实例。|
|PowerBuilder|部分支持。<br /><br /> 支持取决于为 PowerBuilder 控件启用的可访问性。|

 有关如何创建扩展以支持其他平台的信息，请参阅[启用控件的编码的 UI 测试](../test/enable-coded-ui-testing-of-your-controls.md)和[扩展编码的 UI 测试和操作录制以支持 Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)。

## <a name="see-also"></a>请参阅
 [使用 UI 自动化来测试代码，](../test/use-ui-automation-to-test-your-code.md) [从现有操作录制生成编码的 UI 测试](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)
