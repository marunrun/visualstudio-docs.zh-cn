---
title: 使用 DOM 资源管理器调试布局 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- box model [Windows Store apps], viewing
- debugging layout [Windows Store apps]
- layout, debugging [Windows Store apps]
ms.assetid: ded6566d-fc29-49a7-8029-dee8e50fe733
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5dd40381b8f5ba4807e95cfcf5e5b7d54afd77e2
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298385"
---
# <a name="debug-layout-using-dom-explorer"></a>使用 DOM 资源管理器调试布局
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 和 Windows Phone] （.。。将 windows_and_phone_content .png "windows_and_phone_content"）  
  
 DOM 资源管理器的“布局” 选项卡显示适用于 [应用、Windows Phone 应用商店应用或使用 Visual Studio Tools for Apache Cordova 创建的应用中的所选元素的](https://go.microsoft.com/fwlink/?LinkID=238778) CSS 方框模型 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 。 可使用此方框模型的可视表示形式来标识和修改影响元素外观的布局相关值。  
  
> [!TIP]
> 你在“布局” 选项卡中所作的更改不是永久性的。 你可以永久更改源代码，然后使用“调试”工具栏上的“刷新 Windows 应用” （仅限 Windows 应用商店和 Windows Phone 应用商店）按钮刷新应用。 这样一来，便可避免重新启动调试器。  
  
 若要使用 DOM 资源管理器修改未显示在框模型中的布局的各个方面，请参阅快速入门：[使用 DOM 资源管理器](../debugger/debug-css-styles-using-dom-explorer.md)[调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)并调试 css 样式。  
  
## <a name="example-of-fixing-a-layout-issue"></a>修复布局问题的示例  
 此示例演示了如何选择“中心/枢轴”模板中的一个列表元素、解释了 “布局”选项卡上的方框模型值，然后更改某个属性值来修复布局问题。  
  
#### <a name="to-fix-the-layout-issue"></a>修复布局问题  
  
1. 在 Visual Studio 中，创建一个使用“中心/枢轴”项目模板的新应用商店应用。  
  
2. 在共享的 pages\hub 文件夹中，打开 hub.css。  
  
3. 将下列 CSS 代码：  
  
    ```css  
    .hubpage .hub .section4 .sub-image-row img {  
        height: 95px;  
        width: 130px;  
    }  
    ```  
  
     替换为此 CSS 代码：  
  
    ```css  
    .hubpage .hub .section4 .sub-image-row img {  
        height: 95px;  
        width: 130px;  
        margin-left: 5em;  
    }  
    ```  
  
4. 在解决方案资源管理器中选择 appName.WindowsPhone 项目或 appName.Windows 项目，然后从项目的快捷菜单中选择“设为启动项目” 。  
  
5. 根据你的启动项目，在“调试”工具栏上的下拉列表中选择 “仿真程序 8.1 WVGA 4 英寸 512MB”或 “模拟器”（ “本地计算机”是默认值）。  
  
     ![选择调试目标](../debugger/media/js-dom-debug-target-emu.png "JS_DOM_Debug_Target_Emu")  
  
6. 按 F5 以在调试模式下运行应用程序。  
  
7. 通过滚动或轻弹打开第 4 部分。  
  
    > [!TIP]
    > 将 Phone 仿真程序或模拟器放置在 Visual Studio 窗口的右边，以便你能够立即看到选择结果以及你对 CSS 样式进行的更改。  
  
     加载第 4 部分时，你会发现下方的图像看起来不合适。 每个项图像显示一半（缺失左边的一半）。  
  
8. 切换到 Visual Studio，然后在 DOM 资源管理器中选择“选择元素” （或按 Ctrl+B）。 这将更改选择模式以使你可通过单击某项来选择该项，然后将应用程序置于前台。 单击后模式即恢复原样。  
  
    > [!TIP]
    > 你也可以使用箭头键或其他方法直接在 DOM 资源管理器中选择 HTML 元素。 有关选择元素的详细信息，请参阅[快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)。  
  
9. 在 Phone 仿真程序或模拟器中，在已分为两半的图像中选择右半边的灰色图像。 选定元素的周围将突出显示，如下面的 Windows Phone 仿真程序中所示：  
  
     ![选择 DOM 元素](../debugger/media/js-css-layout-select.png "JS_CSS_Layout_Select")  
  
    > [!TIP]
    > 在你选择元素之前，模拟器支持悬停在元素上以在 DOM 元素周围突出显示框。 Windows Phone 仿真程序不支持此内容。  
  
     当你选择 DOM 元素时，DOM 资源管理器将自动在 Visual Studio 中选择相应的 IMG 元素。 DOM 资源管理器中选择的元素类似于此：  
  
    ```html  
    <img src="ms-appx://guid/images/gray.png>   
    </img>  
    ```  
  
10. 单击 "**布局**" 选项卡。此选项卡显示所选元素的方框模型，如 Windows Phone 模拟器中所示。  
  
     ![DOM 资源管理器的 "布局" 选项卡](../debugger/media/js-css-layout.png "JS_CSS_Layout")  
  
     此视图提供有关元素的一些有用信息：  
  
    - 颜色与将鼠标指针悬停在元素上方时模拟器中显示的方框突出显示对应。 蓝颜色表示 \<img > 元素尺寸。 棕褐色表示边距值。  
  
    - 设置左边距 (margin-left)，它可指示问题的原因，因为它与症状匹配（图像左侧显示为黑色）。  
  
    - 显示 0 像素的值的方框（例如，“边框”和“填充”）表示可能未设置相应的 CSS 属性。  
  
11. 若要查看 margin-left 规则的应用方式，请选择“已计算” 选项卡并查看 margin-left 规则下方显示的内容。 你可以看到此规则设置为 5em 值，但是计算的值可以是 66.66px 或 146.66px，具体取决于你的目标设备。  
  
    > [!TIP]
    > "**计算**" 选项卡显示在 `..hubpage .hub. section4 .sub-image-row img` CSS 选择器中设置的左边距规则，位于 "hub" 中。 在本演示应用程序中，这是你需要执行修复的位置。  
  
     还可使用 **“布局”** 选项卡测试对布局值所做的修改。  
  
12. 在“布局” 选项卡中，选择显示在“边距” 框中左侧的“66.66”或 “146.66”。  
  
13. 键入 `0` ，然后按 Enter。 （也可使用向上键和向下键来更改此值。）  
  
14. 在 DOM 资源管理器中选择其他 \<img > 元素，并将其左边距值更改为0。  
  
15. 切换至 Phone 仿真程序或模拟器。 更新后的 margin-left 值已应用到第 4 部分的图像。 这些值还会在 margin-left 规则下的“已计算” 选项卡中更新。  
  
## <a name="see-also"></a>请参阅  
 [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)   
 [使用 DOM 资源管理器调试 CSS 样式](../debugger/debug-css-styles-using-dom-explorer.md)   
 [查看 DOM 事件侦听器](../debugger/view-dom-event-listeners.md)
