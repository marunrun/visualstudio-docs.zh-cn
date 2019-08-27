---
title: JavaScript 控制台命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/28/2019
ms.topic: reference
helpviewer_keywords:
- JavaScript Console commands [UWP apps]
- JavaScript debugging, console [UWP apps]
- debugging JavaScript, console [UWP apps]
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
- cordova
ms.openlocfilehash: 40e32250378d92ac63e4a057a59ee847de6af810
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905669"
---
# <a name="javascript-console-commands-in-visual-studio"></a>Visual Studio 中的 JavaScript 控制台命令

::: moniker range=">=vs-2019"
你可以在 Visual Studio 的“JavaScript 控制台”窗口中使用命令发送消息和执行其他任务。 本主题中的信息适用于使用 Visual Studio 中使用创建的 Node.js 应用**Node.js 开发**安装工作负载。
::: moniker-end
::: moniker range="vs-2017"
你可以在 Visual Studio 的“JavaScript 控制台”窗口中使用命令发送消息和执行其他任务。 有关演示如何使用此窗口的示例，请参阅[快速入门：调试 JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md?view=vs-2017)。 本主题中的信息适用于 Node.js 应用，UWP 应用和使用 Visual Studio Tools for Apache Cordova 创建的应用。 有关 Cordova 应用中受支持控制台命令的信息，请参阅 [Debug Your App](https://taco.visualstudio.com/en-us/docs/debug-using-visual-studio/)。
::: moniker-end

如果 JavaScript 控制台窗口已关闭，则可以打开它通过选择 Visual Studio 中调试时，**调试** > **Windows** > **JavaScript控制台**。

> [!NOTE]
> 如果该窗口在调试会话期间不可用，请确保在项目的“调试”属性中将调试器类型设置为 **“脚本”** 。

在 Microsoft Edge 开发人员工具中使用控制台的信息，请参阅[本主题](/microsoft-edge/devtools-guide)。

## <a name="console-object-commands"></a>控制台对象命令
下表显示 `console` 对象命令的语法，这些命令可用在“JavaScript 控制台”窗口中或者可用于从代码中向控制台发送消息。 此对象提供多种形式，以使你可区分信息性消息和错误消息（如果要区分）。

如果需要避免可能与由局部对象命名的控制台产生混淆，可使用较长的命令形式 `window.console.[command]` 。

> [!TIP]
> 较旧版本的 Visual Studio 不支持完整的命令集。 使用控制台对象上的 IntelliSense 快速获取有关支持命令的信息。

|命令|描述|示例|
|-------------|-----------------|-------------|
|`assert(expression, message)`|如果 `expression` 计算结果为 **false**，则发送消息。|`console.assert((x == 1), "assert message: x != 1");`|
|`clear()`|清除控制台窗口中的消息（包括脚本错误消息）以及控制台窗口中显示的脚本。 不清除你在控制台输入提示中输入的脚本。|`console.clear();`|
|`count(title)`|将计数命令的调用次数发送到控制台窗口。 对计数的每次调用由可选的 `title`唯一标识。<br /><br /> 控制台窗口中的现有项由 `title` 参数（如果有）标识，并由计数命令更新。 不创建新项。|`console.count();`<br /><br /> `console.count("inner loop");`|
|`debug(message)`|向控制台窗口发送 `message` 。<br /><br /> 此命令与 console.log 相同。<br /><br /> 使用此命令传递的对象将转换为字符串值。|`console.debug("logging message");`|
|`dir(object)`|将指定的对象发送到控制台窗口并在对象可视化工具中显示它。 可使用该可视化工具在控制台窗口中检查属性。|`console.dir(obj);`|
|`dirxml(object)`|将指定的 XML 节点 `object` 发送到控制台窗口并使其显示为 XML 节点树。|`console.dirxaml(xmlNode);`|
|`error(message)`|向控制台窗口发送 `message` 。 消息文本为红色，并以错误符号开头。<br /><br /> 使用此命令传递的对象将转换为字符串值。|`console.error("error message");`|
|`group(title)`|对发送到控制台窗口的消息开始分组，并发送可选的 `title` 作为组标签。 在控制台窗口中，组可以嵌套并显示在树视图中。<br /><br /> 在某些情况下，例如使用一个组件模型时，通过 group* 命令可以更轻松地查看控制台窗口输出。|`console.group("Level 2 Header");` <br /> `console.log("Level 2");` <br /> `console.group();` <br /> `console.log("Level 3");` <br /> `console.warn("More of level 3");` <br /> `console.groupEnd();` <br /> `console.log("Back to level 2");` <br /> `console.groupEnd();` <br /> `console.debug("Back to the outer level");`|
|`groupCollapsed(title)`|对发送到控制台窗口的消息开始分组，并发送可选的 `title` 作为组标签。 使用 `groupCollapsed` 发送的组默认显示在折叠视图中。 在控制台窗口中，组可以嵌套并显示在树视图中。|用法与 `group` 命令相同。<br /><br /> 请参见 `group` 命令的示例。|
|`groupEnd()`|当前组结束。<br /><br /> 要求：<br /><br /> Visual Studio 2013|请参见 `group` 命令的示例。|
|`info(message)`|向控制台窗口发送 `message` 。 消息以信息符号开头。|`console.info("info message");`<br /><br /> 有关更多示例，请参阅本主题后面部分的 [Formatting console.log output](#ConsoleLog) 。|
|`log(message)`|向控制台窗口发送 `message` 。<br /><br /> 若传递某个对象，则该命令将该对象发送到控制台窗口并在对象可视化工具中显示它。 可使用该可视化工具在控制台窗口中检查属性。|`console.log("logging message");`|
|`msIsIndependentlyComposed(element)`|在 Web 应用中使用。 不支持在使用 JavaScript 的 UWP 应用中。|不支持。|
|`profile(reportName)`|在 Web 应用中使用。 不支持在使用 JavaScript 的 UWP 应用中。|不支持。|
|`profileEnd()`|在 Web 应用中使用。 不支持在使用 JavaScript 的 UWP 应用中。|不支持。|
|`select(element)`|在 `element` DOM 资源管理器 [中选择指定的 HTML](../debugger/quickstart-debug-html-and-css.md)。|console.select(element);|
|`time (name)`|启动由可选的 `name` 参数标识的计时器。 配合 `console.timeEnd`使用时，计算 `time` 和 `timeEnd`之间经历的时间，并使用 `name` 字符串作为前缀将结果（以 ms 为测量单位）发送到控制台。 用于启用应用程序代码的检测以衡量性能。|`console.time("app start");  app.start();  console.timeEnd("app start");`|
|`timeEnd(name)`|停止由可选的 `name` 参数标识的计时器。 请参见 `time` 控制台命令。|`console.time("app start"); app.start(); console.timeEnd("app start");`|
|`trace()`|将堆栈跟踪发送到控制台窗口。 跟踪包括完整的调用堆栈以及文件名、行号和列号等信息。|`console.trace();`|
|`warn(message)`|向控制台窗口发送 `message` ，并以警告符号开头。<br /><br /> 使用此命令传递的对象将转换为字符串值。|`console.warn("warning message");`|

## <a name="miscellaneous-commands"></a>杂项命令
JavaScript 控制台窗口中也提供这些命令（它们不能通过代码启用）。

|命令|描述|示例|
|-------------|-----------------|-------------|
|`$0`, `$1`, `$2`, `$3`, `$4`|将指定元素返回到控制台窗口。 `$0` 返回当前在 DOM 资源管理器中选择的元素，`$1` 返回以前在 DOM 资源管理器中选择的元素，依此类推，最多可返回第四个以前选择的元素。|$3|
|`$(id)`|按 ID 返回元素。 这是 `document.getElementById(id)`的快捷方式命令，其中 `id` 是一个表示元素 ID 的字符串。|`$("contenthost")`|
|`$$(selector)`|使用 CSS 选择器语法返回与指定选择器匹配的元素的数组。 这是 `document.querySelectorAll()`的快捷方式命令。|`$$(".itemlist")`|
|`cd()`<br /><br /> `cd(window)`|用于将表达式计算的上下文从页面的默认顶级窗口改为指定框架的窗口。 无参数调用 `cd()` 可使上下文返回顶级窗口。|`cd();`<br /><br /> `cd(myframe);`|
|`select(element)`|在 [DOM 资源管理器](../debugger/quickstart-debug-html-and-css.md)中选择指定元素。|`select(document.getElementById("element"));`<br /><br /> `select($("element"));`<br /><br /> `select($1);`|
|`dir(object)`|为指定的对象返回一个可视化工具。 可使用该可视化工具在控制台窗口中检查属性。|`dir(obj);`|

## <a name="checking-whether-a-console-command-exists"></a>检查控制台命令是否存在
在尝试使用特定命令前，可以检查其是否存在。 此示例检查 `console.log` 命令是否存在。 如果 `console.log` 存在，代码将调用它。

```javascript
if (console && console.log) {
    console.log("msg");
}

```

## <a name="examining-objects-in-the-javascript-console-window"></a>检查“JavaScript 控制台”窗口中的对象
使用“JavaScript 控制台”窗口时，你可以与范围内的任何对象进行交互。 若要检查控制台窗口中超出范围的对象，请在代码中使用 `console.log` 、 `console.dir`或其他命令。 当对象在范围内时，你还可以在代码中设置断点（**“断点”** > **Insert “断点”**），从控制台窗口与对象进行交互。

## <a name="ConsoleLog"></a>格式化 console.log 输出
若将多个参数传递给 `console.log`，则控制台将这些参数视为数组并连接输出。

```javascript
var user = new Object();
user.first = "Fred";
user.last = "Smith";

console.log(user.first, user.last);
// Output:
// Fred Smith

```

`console.log` 还支持“printf”替换模式以格式化输出。 若在第一个参数中使用替换模式，则将使用其他参数来按使用的顺序对指定模式进行替换。

 支持以下替换模式：

- %s - 字符串 %i - 整数 %d - 整数 %f - 浮点数 %o - 对象 %b - 二进制 %x - 十六进制 %e - 指数

  下面是在 `console.log`中使用替换模式的一些示例：

```javascript
var user = new Object();
user.first = "Fred";
user.last = "Smith";
user.age = 10.01;
console.log("Hi, %s %s!", user.first, user.last);
console.log("%s is %i years old!", user.first, user.age);
console.log("%s is %f years old!", user.first, user.age);

// Output:
// Hi, Fred Smith!
// Fred is 10 years old!
// Fred is 10.01 years old!
```

## <a name="see-also"></a>请参阅
- [快速入门：调试 JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md?view=vs-2017)
- [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md?view=vs-2017)
