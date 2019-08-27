---
title: 查看 DOM 事件侦听器 |Microsoft Docs
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
- DOM events, viewing [Windows Store apps]
- event listeners, viewing [Windows Store apps]
ms.assetid: d5b679e7-87dd-4cec-9176-883db6ff0781
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 64d4892080aaf0cf04e4b208b1a0bdb7a7a4480d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65693578"
---
# <a name="view-dom-event-listeners"></a>查看 DOM 事件侦听器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 和 Windows Phone] (../Image/windows_and_phone_content.png"windows_and_phone_content")

 **事件**DOM 资源管理器的选项卡显示与 DOM 元素关联的事件。 在每个顶部节点**事件**选项卡表示一个具有活动订户的事件。 顶部节点包含若干子节点，表示为特定事件注册的事件侦听器。 使用此选项卡除了可查看事件侦听器之外，还可导航至事件侦听器在 JavaScript 代码中的位置。 本主题中的信息适用于使用 HTML 和 JavaScript 的应用商店应用。

 上的列表**事件**是动态的选项卡。 如果在应用运行时添加事件侦听器，则列表中将显示该新事件侦听器。 有关添加和删除事件侦听器的信息，请参阅[解决问题的事件侦听器的提示](#Tips)本主题中。

> [!NOTE]
> 如非 DOM 元素的代码元素的事件侦听器`xhr`，不会显示**事件**选项卡。

## <a name="view-event-listeners-for-dom-elements"></a>查看 DOM 元素的事件侦听器
 本示例展示了一个 Windows Phone 应用商店应用。 Windows 应用商店应用也支持此处描述的 DOM 资源管理器功能。

#### <a name="to-view-event-listeners"></a>若要查看事件侦听器，请执行以下操作

1. 在 Visual Studio 中，创建一个使用“Windows Phone 枢轴应用程序”项目模板的 JavaScript 应用。

2. 在 Visual Studio 中打开该模板中，选择**仿真程序 8.1 WVGA 4 英寸 512MB**在调试器中的调试工具栏上的下拉列表中：

     ![选择调试目标](../debugger/media/js-dom-debug-target-emu.png "JS_DOM_Debug_Target_Emu")

3. 按 F5 以在调试模式下运行应用程序。

4. 在正在运行的应用，请转至**第 3 部分**枢轴项。

5. 切换到 Visual Studio（Alt+Tab 或 F12）。

6. 在 DOM 资源管理器中，选择右上角的 `Find`。

7. 键入 `ListView`，然后按 Enter。

8. 如有必要，选择**下一步**按钮以查找`DIV`元素，它表示`ListView`控件 (此元素具有`data-win-control`的值`WinJS.UI.ListView`)。

     此时，应在 DOM 资源管理器中选择 `DIV` 元素。

9. 选择**事件**在 DOM 资源管理器右侧窗格中的选项卡。

     现在可看到具有 `DIV` 元素的活动订户的事件，如下所示。

     ![DOM 资源管理器的事件选项卡](../debugger/media/js-dom-events.png "JS_DOM_Events")

10. 若要查找这些事件的事件侦听器，请选择关联的 JavaScript 文件链接。

11. 要快速地识别 DOM 层次结构中的父元素的事件侦听器，请在 DOM 资源管理器底部的层次结构列表中选择一个父元素。

     ![选择 DOM 层次结构中的父元素](../debugger/media/js-dom-breadcrumbs.png "JS_DOM_Breadcrumbs")

     **事件**选项卡显示在层次结构列表中选择任何元素的事件侦听器。

### <a name="Tips"></a> 解决问题的事件侦听器的提示
 在某些应用方案，事件侦听器必须显式删除使用[removeEventListener](https://msdn.microsoft.com/library/ie/ff975250\(v=vs.85\).aspx)。 使用**事件**在 DOM 资源管理器来测试是否运行代码时从 DOM 元素删除事件侦听器的选项卡。 下面是一些提示，用来帮助解决以下类型的问题：

- 使用单页导航模型的应用程序在 Visual Studio 中实现[项目模板](https://msdn.microsoft.com/library/windows/apps/hh758331.aspx)，它不是通常需要删除对对象，例如，属于页面的 DOM 元素注册的事件侦听器。 在此方案中，DOM 元素及其关联事件侦听器具有相同的生存期并且它们可以作为垃圾回收。

- 如果 DOM 元素的生存期与关联的事件侦听器不同，你可能必须调用 `removeEventListener` 方法。 例如，如果你使用 `window.onresize` 事件，当你从处理事件的页面离开时，你可能必须移除事件侦听器。

- 如果 `removeEventListener` 无法删除指定的侦听器，它可能已由对象的另一个实例调用。 可以使用[bind 方法 (Function)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)方法来解决此问题时添加侦听器。

- 若要删除的事件侦听器，通过使用已添加[bind 方法 (Function)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)或通过使用匿名函数中, 添加侦听器时存储该函数的实例。 下面是安全使用此模式的一种方法：

    ```javascript
    // You could use the following code within the constructor function of an object, or
    // in the ready function of a PageControl object (Store app).
    this.storedHandler = this._handlerFunc.bind(this);
    elem.addEventListener('mouseup', this.storedHandler);

    // In this example, add the following code in the PageControl object's unload function.
    elem.removeEventListener('mouseup', this.storedHandler);

    ```

     如果你使用以下代码而不是存储对绑定函数的引用，你可能无法显式删除事件侦听器：

    ```javascript
    // Avoid this pattern. No reference to the bound function is available.
    elem.addEventListener('mouseup', this._handlerFunc.bind(this));
    ```

- 如果事件侦听器是使用 `removeEventListener` 属性（例如，`obj.on<eventname>`）添加的，你可能无法使用 `window.onresize = handlerFunc` 删除事件侦听器。

- 使用 JavaScript 内存分析器[JavaScript 内存](../profiling/javascript-memory.md)应用程序中。 必须显式删除的事件侦听器可能会显示为内存泄露。

## <a name="see-also"></a>请参阅

- [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)
- [使用 DOM 资源管理器调试 CSS 样式](../debugger/debug-css-styles-using-dom-explorer.md)
- [使用 DOM 资源管理器调试布局](../debugger/debug-layout-using-dom-explorer.md)