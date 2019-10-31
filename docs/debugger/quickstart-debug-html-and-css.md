---
title: 调试 UWP 应用中的 HTML 和 CSS |Microsoft Docs
ms.date: 07/17/2018
ms.topic: conceptual
f1_keywords:
- VS.WebClient.DomExplorer
dev_langs:
- JavaScript
helpviewer_keywords:
- debugging, CSS
- debugging, HTML
- debugging, JavaScript [UWP apps]
- DOM Explorer [UWP apps]
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: 12f66658cd8069f58355a96b2c3b3031a4cb6808
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187568"
---
# <a name="debug-html-and-css-in-uwp-apps-in-visual-studio"></a>在 Visual Studio 中调试 UWP 应用中的 HTML 和 CSS

Visual Studio 针对 JavaScript 应用提供全面的调试体验，其中包括 Internet Explorer 和 Visual Studio 开发人员熟悉的多项功能。 UWP 应用和使用 Visual Studio Tools Apache Cordova 创建的应用支持这些功能。

通过使用 DOM 检查工具所提供的交互式调试模型，你可以查看并修改所呈现的 HTML 和 CSS 代码。 你可以在不停止并重新启动调试器的情况下执行这一切操作。

有关其他 JavaScript 调试功能（如使用 JavaScript 控制台窗口和设置断点）的信息，请参阅[快速入门：](../debugger/quickstart-debug-javascript-using-the-console.md) [在 Visual Studio 中](debugging-windows-store-and-windows-universal-apps.md)调试 JavaScript 和调试应用。

## <a name="InspectingDOM"></a> 检查实时 DOM
DOM 资源管理器展示所呈现的页面的视图，还可使用 DOM 资源管理器更改值并立即看到结果。 这使你可以在无需停止和重新启动调试器的情况下测试更改。 使用此方法与页面进行交互时不更改项目中的源代码，因此当发现代码中要更正的内容时，请对源代码作出更改。

> [!TIP]
> 若要在更改源代码时避免停止和重新启动调试器，你可以使用“调试”工具栏上的 **“刷新 Windows 应用”** 按钮（或按 F4）刷新应用。 有关详细信息，请参阅[刷新应用（JavaScript）](../debugger/refresh-an-app-javascript.md)。

可使用 DOM 资源管理器：

- 在 DOM 元素子树中导航并检查所呈现的 HTML、CSS 和 JavaScript 代码。

- 动态编辑所呈现元素的特性和 CSS 样式，并立即看到结果。

- 检查如何将 CSS 样式应用到页元素，并跟踪已应用的规则。

  调试应用程序时，通常需要在 DOM 资源管理器中选择元素。 选择某个元素后，DOM 资源管理器右侧选项卡上显示的值将自动更新，以反映 DOM 资源管理器中的选定元素。 这些选项卡是：“样式”、“计算”、“布局”。 UWP 应用还支持 "**事件**" 和 "**更改**" 选项卡。 有关选择元素的详细信息，请参见 [Selecting elements](#SelectingElements)。

> [!TIP]
> 如果“DOM 资源管理器”窗口已关闭，请依次选择“调试”> >  以重新打开它。 仅在脚本调试会话期间显示该窗口。

在后续过程中，我们将通过使用 DOM 资源管理器完成以交互方式调试应用程序的过程。 我们将创建一个使用 `FlipView` 控件的应用程序，然后调试它。 此应用程序包含若干错误。

> [!WARNING]
> 下面的示例应用是 UWP 应用。 Cordova 支持以上相同的功能，但应用会有所不同。

#### <a name="to-debug-by-inspecting-the-live-dom"></a>通过检查实时 DOM 进行调试

1. 通过选择 **“文件”**  >  **“新建项目”** 。

2. 选择 " **JavaScript**  > **Windows 通用**"，然后选择 " **WinJS 应用**"。

3. 为项目输入名称（如 `FlipViewApp`），然后选择“确定” 以创建应用。

4. 在 index 的 BODY 元素中，添加以下代码：

    ```html
    <div id="flipTemplate" data-win-control="WinJS.Binding.Template"
            style="display:none">
        <div class="fixedItem" >
            <img src="#" data-win-bind="src: flipImg" />
        </div>
    </div>
    <div id="fView" style="width:100px;height:100px"
        data-win-control="WinJS.UI.FlipView" data-win-options="{
        itemDataSource: Data.items.dataSource, itemTemplate: flipTemplate }">
    </div>
    ```

5. 打开 default.css，然后添加以下 CSS：

    ```css
    #fView {
        background-color:#0094ff;
        height: 100%;
        width: 100%;
        margin: 25%;
    }
    ```

6. 将 default.js 中的代码替换为以下这段代码：

    ```javascript
    (function () {
        "use strict";

        var app = WinJS.Application;
        var activation = Windows.ApplicationModel.Activation;

        var myData = [];
        for (var x = 0; x < 4; x++) {
            myData[x] = { flipImg: "/images/logo.png" }
        };

        var pages = new WinJS.Binding.List(myData, { proxy: true });

        app.onactivated = function (args) {
            if (args.detail.kind === activation.ActivationKind.launch) {
                if (args.detail.previousExecutionState !==
                activation.ApplicationExecutionState.terminated) {
                    // TODO: . . .
                } else {
                    // TODO: . . .
                }
                args.setPromise(WinJS.UI.processAll());

                updateImages();
            }
        };

        function updateImages() {

            pages.setAt(0, { flipImg: "http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-76.jpg" });
            pages.setAt(1, { flipImg: "http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-77.jpg" });
            pages.setAt(2, { flipImg: "http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-78.jpg" });
        };

        app.oncheckpoint = function (args) {
        };

        app.start();

        var publicMembers = {
            items: pages
        };

        WinJS.Namespace.define("Data", publicMembers);

    })();
    ```

    下图显示了在运行此应用程序时需要了解的内容。 但是，若要让应用程序进入此状态，我们必须先修复大量 Bug。

    ![显示预期结果的 FlipView 应用](../debugger/media/js_dom_appfixed.png "JS_DOM_AppFixed")

7. 从 "**调试**" 工具栏上的 "**启动调试**" 按钮旁的下拉列表中选择 "**本地计算机**"：

    ![选择调试目标列表](../debugger/media/js_select_target.png "JS_Select_Target")

8. 选择 **“仿真程序 8.1 WVGA 4 英寸 512MB”**  >  **“模拟器”** 或按 F5，以调试模式运行应用。

    这会运行应用程序，但你将看到大多数空白屏幕，因为样式中有几个 bug。 第一个 `FlipView` 图像显示在屏幕中间附近的小正方形中。

9. 切换到 Visual Studio 并选择 **“DOM 资源管理器”** 选项卡。

    > [!TIP]
    > 可按 Alt+Tab 或 F12，在 Visual Studio 和正在运行的应用程序之间切换。

10. 在“DOM 资源管理器”窗口中，选择 ID 为 `"fView"`的部分的 DIV 元素。 使用箭头键可以查看并选择正确的 DIV 元素。 （使用向右键可以查看元素的子元素。）

    ![DOM 资源管理器](../debugger/media/js_dom_explorer.png "JS_DOM_Explorer")

    > [!TIP]
    > 也可通过在 >> 输入提示符下键入 `select(fView)`，然后按 Enter，在“JavaScript 控制台”窗口的左下角选择此 DIV 元素。

    “DOM 资源管理器”窗口的右侧选项卡上显示的值将自动更新，以反映 DOM 资源管理器中的当前元素。

11. 选择右侧的 **“计算”** 选项卡。

    此选项卡显示选定 DOM 元素的每个属性的计算值或最终值。

12. 打开高度 CSS 规则。 请注意，有一个级联样式设置为 100px，似乎与为 `#fView` CSS 选择器设置的 100% 的高度值不一致。 `#fView` 选择器的带有删除线的文本指示内联样式优先于该样式。

    下图显示了 **“已计算”** 选项卡。

    ![DOM 资源管理器计算选项卡](../debugger/media/js_dom_explorer_computed.png "JS_DOM_Explorer_Computed")

13. 在“DOM 资源管理器”主窗口中，双击 `fView` DIV 元素的高度和宽度的级联样式。 现在可以在此处编辑这些值。 在此方案中，我们需要完全移除它们。

14. 在主窗口中，双击 "`width: 100px;height: 100px;`"，按**Delete**键，然后按**enter**。 按 Enter 后，新值会立即反映在应用中，但你尚未停止调试会话。

    > [!IMPORTANT]
    > 你不但可以在“DOM 资源管理器”窗口中更新特性，还可更新 **“样式”** 、 **“已计算”** 和 **“布局”** 选项卡上显示的值。 有关详细信息，请参阅[使用 Dom 资源管理器调试 CSS 样式](../debugger/debug-css-styles-using-dom-explorer.md)和[使用 Dom 资源管理器调试布局](quickstart-debug-html-and-css.md)。

15. 通过选择该应用程序或通过使用 Alt + Tab 切换到该应用程序。

    现在， `FlipView` 控件的外观大于模拟器或 Phone 仿真程序的屏幕大小。 这并不是预期的结果。 若要进行调查，请切回到 Visual Studio。

16. 在 DOM 资源管理器中，再次选择 **“计算”** 选项卡并打开高度规则。 FView 元素仍按预期从 CSS 中显示值100%，但计算值等于应用的屏幕高度（例如，800px、667.67 p px 或其他值），这不是我们想要用于此应用的值。 若要进行调查，请在后续步骤中，删除 `fView` DIV 元素的高度和宽度。

17. 在 **“样式”** 选项卡中，取消选中 `#fView` CSS 选择器的高度和宽度属性。

    **“计算”** 选项卡现在显示高度 400px。 信息指示此值来自平台 CSS 文件 ui-dark.css 中指定的 .win-flipview 选择器。

18. 切回到此应用程序。

    情况有所好转。 然而，还有一个问题有待解决，那就是边距看上去太大。

19. 要进行调查，请切换到 Visual Studio 并选择“布局”选项卡查看元素的框模型。

    在 "**布局**" 选项卡中，你将看到以下内容：

    - 255px （偏移量）和255px （边距）或类似值（取决于设备分辨率）。

      下图显示了在使用具有100px 偏移量和边距的模拟器时 "**布局**" 选项卡的外观。

      ![DOM 资源管理器布局选项卡](../debugger/media/js_dom_explorer_layout.png "JS_DOM_Explorer_Layout")

      这似乎并不合适。 **“计算”** 选项卡也显示相同的边距值。

20. 选择 **“样式”** 选项卡，并找到 `#fView` CSS 选择器。 在这里，你将看到 **“边距”** 属性的值为 25%。

21. 选择 25% 并将其更改为 25px，然后按 Enter。

22. 同样，在 **“样式”** 选项卡中，选择 .win-flipview 选择器的高度规则并将 400px 更改为 500px，然后按 Enter。

23. 切回到应用程序，你会发现元素的位置显示正确。 若要修复源并刷新应用程序，而不停止并重新启动调试器，请参见以下过程。

#### <a name="to-refresh-your-app-while-debugging"></a>若要在调试期间刷新应用程序，请执行以下操作

1. 在应用程序仍在运行时，切换至 Visual Studio。

2. 打开 default.html，然后通过将 `"fView"` DIV 元素的 height 和 width 均设置为 100%，对源代码进行修改。

3. 选择“调试”工具栏上的 **“刷新 Windows 应用程序”** 按钮（或按 F4）。 按钮如下所示： "![刷新 Windows 应用程序" 按钮](../debugger/media/js_refresh.png "JS_Refresh")。

    随后将重新加载应用程序页面，并且模拟器或 Phone 仿真程序将返回前台。

    有关刷新功能的详细信息，请参阅[刷新应用（JavaScript）](../debugger/refresh-an-app-javascript.md)。

## <a name="SelectingElements"></a> Selecting elements
在调试应用程序时，可以通过三种方式选择 DOM 元素：

- 通过在“DOM 资源管理器”窗口中直接单击元素（或通过使用箭头键）。

- 通过使用 **“选择元素”** 按钮 (Ctrl+B)。

- 通过使用 `select` 命令（该命令是 [JavaScript Console commands](../debugger/javascript-console-commands.md?view=vs-2017)。

  在使用“DOM 资源管理器”窗口选择元素并将鼠标指针置于一个元素上时，正在运行的应用程序中会突出显示相应的元素。 必须在 DOM 资源管理器中单击该元素以将其选定，也可以使用箭头键突出显示并选择元素。此外，还可以使用 **“选择元素”** 按钮在 DOM 资源管理器中选择元素。 下图显示 **“选择元素”** 按钮。

  ![DOM 资源管理器中的 "选择元素" 按钮](../debugger/media/js_dom_select_element_button.png "JS_DOM_Select_Element_Button")

  单击 **“选择元素”** （或按 Ctrl+B）将更改选择模式，以使你在正在运行的应用程序中单击某项，即可在 DOM 资源管理器中选择该项。 单击之后，模式将变回正常选择模式。 单击 **“选择元素”** 后，应用程序转入前台，而光标发生变化以反映新的选择模式。 单击有轮廓包围的元素后，DOM 资源管理器将返回前台，并选中了指定的元素。

  在选择 **“选择元素”** 之前，可通过切换 **“显示网页突出显示”** 按钮来指定是否在正在运行的应用中突出显示元素。 下图显示了该按钮。 默认情况下，将显示突出显示的元素。

  ![显示网页突出显示按钮](../debugger/media/js_dom_display_highlights_button.png "JS_DOM_Display_Highlights_Button")

  在选择突出显示元素时，将突出显示模拟器中指针悬停在其上方的元素。 突出显示的元素的颜色与 DOM 资源管理器的 **“布局”** 选项卡中显示的方框模型匹配。

> [!NOTE]
> 指针悬停在元素上方时突出显示的元素在 Windows Phone 模拟器中仅部分受支持。

## <a name="see-also"></a>请参阅
- [在 Visual Studio 中调试应用](debugging-windows-store-and-windows-universal-apps.md)
- [刷新应用 (JavaScript)](../debugger/refresh-an-app-javascript.md)
- [调试 WebView 控件](../debugger/debug-a-webview-control.md)
- [键盘快捷键](../debugger/keyboard-shortcuts-html-and-javascript.md?view=vs-2017)
- [JavaScript Console commands](../debugger/javascript-console-commands.md?view=vs-2017)
- [调试 HTML、CSS 和 JavaScript 示例代码](../debugger/debug-html-css-and-javascript-sample-code.md)
- [产品支持和辅助功能](https://msdn.microsoft.com/library/tzbxw1af(VS.120).aspx)
