---
title: 调试用户代码与仅我的代码 |Microsoft Docs
ms.date: 02/13/2019
ms.topic: conceptual
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: edb78ed49add85b35f3fb89b4ba424d44f52bf8b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905741"
---
# <a name="debug-only-user-code-with-just-my-code"></a>调试用户代码仅使用仅我的代码

*仅我的代码*Visual Studio 调试功能的自动步骤是通过对系统、 框架和其他非用户代码的调用。 在中**调用堆栈**窗口中，仅我的代码折叠这些调用 **[外部代码]** 帧。

仅我的代码的工作方式在.NET Framework 中， C++，和 JavaScript 项目。

## <a name="BKMK_Enable_or_disable_Just_My_Code"></a>启用或禁用“仅我的代码”

对于大多数编程语言，默认情况下启用仅我的代码。

- 若要启用或禁用在 Visual Studio 中，仅我的代码下**工具** > **选项**(或**调试** > **选项**) >**调试** > **常规**中，选择或取消选中**启用 ' 仅我的代码**。

![启用仅我的代码选项对话框中](../debugger/media/dbg_justmycode_options.png "启用 ' 仅我的代码")

> [!NOTE]
> **启用仅我的代码**是适用于所有语言中的所有 Visual Studio 项目的全局设置。

## <a name="just-my-code-debugging"></a>“仅我的代码”调试

调试会话期间**模块**窗口显示了其符号加载状态以及代码调试器视为我的代码 （用户代码） 的模块。 有关详细信息，请参阅[更深入了解如何将调试器附加到您的应用程序](../debugger/debugger-tips-and-tricks.md#modules_window)。

![模块窗口中的用户代码](../debugger/media/dbg_justmycode_module.png "模块窗口中的用户代码")

在中**调用堆栈**或**任务**窗口中，仅我的代码将非用户代码折叠到标记为灰显批注的代码帧`[External Code]`。

![在调用堆栈窗口中的外部代码帧](../debugger/media/dbg_justmycode_externalcode.png "外部代码帧")

>[!TIP]
>若要打开**模块**，**调用堆栈**，**任务**，或者必须是在调试会话中的其他大多数的调试窗口。 在调试时下,**调试** > **Windows**，选择你想要打开的窗口。

<a name="BKMK_Override_call_stack_filtering"></a> 若要查看一个折叠中的代码 **[外部代码]** 框架中，右键单击**调用堆栈**或**任务**窗口中，然后选择**显示外部代码**从上下文菜单。 展开的外部代码行替换 **[外部代码**] 帧。

![在调用堆栈窗口中显示外部代码](../debugger/media/dbg_justmycode_showexternalcode.png "显示外部代码")

> [!NOTE]
> **显示外部代码**是当前用户探查器设置，适用于在用户打开的所有语言中的所有项目。

双击在展开的外部代码行**调用堆栈**窗口突出显示绿色的源代码中调用的代码行。 对于 Dll 或未找到或加载其他模块，符号或源文件未找到页可能会打开。

## <a name="BKMK__NET_Framework_Just_My_Code"></a>.NET Framework“仅我的代码”

在.NET Framework 项目中，仅我的代码使用符号 (*.pdb*) 文件和程序优化，以对用户和非用户代码进行分类。 .NET Framework 调试程序会将优化的二进制文件，而非加载 *.pdb*文件视为非用户代码。

三个编译器属性也会影响.NET 调试器视为用户代码：

- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute> 告知调试器应用于的代码不是用户代码。
- <xref:System.Diagnostics.DebuggerHiddenAttribute> 对调试器隐藏代码，即使“仅我的代码”关闭；
- <xref:System.Diagnostics.DebuggerStepThroughAttribute> 告知调试器逐句通过代码应用到的、 而不是单步执行代码。

.NET Framework 调试器就会将所有其他代码，用户代码。

在.NET Framework 调试：

- **调试** > **单步执行**(或**F11**) 非用户代码的步骤的代码到下一行用户代码。
- **调试** > **单步跳出**(或**Shift**+**F11**) 非用户代码运行到下一行用户代码。

如果没有更多的用户代码，调试继续，直到它结束，到达另一个断点，或将引发错误。

<a name="BKMK_NET_Breakpoint_behavior"></a> 如果调试器在非用户代码中中断 (例如，使用**调试** > **全部中断**和在非用户代码中的暂停)，则**无源**窗口会显示。 然后，可以使用**调试** > **步骤**命令可以转到下一行用户代码。

如果在非用户代码中发生未经处理的异常，调试器将中断在用户代码行生成异常的位置。

如果异常启用了第一机会异常，调用用户代码行以在源代码中的绿色突出显示。 **调用堆栈**窗口将显示标记为在带批注的帧 **[外部代码]**。

## <a name="BKMK_C___Just_My_Code"></a>C++“仅我的代码”

启动 Visual Studio 2017 版本 15.8，代码仅我的代码中也支持单步执行。 此功能还需要使用[/JMC （仅我的代码的调试）](/cpp/build/reference/jmc)编译器开关。 默认情况下启用了开关C++项目。 有关**调用堆栈**窗口和调用堆栈的支持仅我的代码，在不需要 /JMC 开关。

<a name="BKMK_CPP_User_and_non_user_code"></a> 被归类为用户代码，其中包含用户代码二进制文件的 PDB 必须加载由调试器 (使用**模块**窗口要检查此项)。

对于调用堆栈行为，如在**调用堆栈**窗口中，仅在我的代码C++将仅为这些函数视为*非用户代码*:

- 在其符号文件中去除了源信息的函数。
- 符号文件指示没有对应于堆栈帧的源文件的函数。
- 中指定的函数 *\*.natjmc*中的文件 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹。

有关代码单步执行行为，仅在我的代码C++会考虑仅为这些函数*非用户代码*:

- 为其相应的 PDB 文件尚未加载在调试器中的函数。
- 中指定的函数 *\*.natjmc*中的文件 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹。

> [!NOTE]
> 代码单步执行中的支持仅我的代码，C++必须使用在 Visual Studio 15.8 Preview 3 或更高版本的 MSVC 编译器编译代码，必须启用 /JMC 编译器开关 （默认情况下已启用）。 有关其他详细信息，请参阅[自定义C++调用堆栈和代码单步执行行为](#BKMK_CPP_Customize_call_stack_behavior))，这[博客文章](https://devblogs.microsoft.com/cppblog/announcing-jmc-stepping-in-visual-studio/)。 对于使用较旧的编译器编译的代码 *.natstepfilter*文件是唯一的方法自定义代码单步执行，这是独立于仅我的代码。 请参阅[自定义C++单步执行行为](#BKMK_CPP_Customize_stepping_behavior)。

<a name="BKMK_CPP_Stepping_behavior"></a> 在C++调试：

- **调试** > **单步执行**(或**F11**) 非用户代码的步骤的代码到下一行用户代码。
- **调试** > **单步跳出**(或**Shift**+**F11**) 非用户代码运行到下一行用户代码。

如果没有更多的用户代码，调试继续，直到它结束，到达另一个断点，或将引发错误。

如果调试器在非用户代码中中断 (例如，使用**调试** > **全部中断**和暂停在非用户代码中)，在非用户代码中继续单步执行。

如果调试器遇到异常时，它将停止的异常，不管它们是在用户或非用户代码。 **用户未处理**中的选项**异常设置**对话框将被忽略。

### <a name="BKMK_CPP_Customize_call_stack_behavior"></a> 自定义C++调用堆栈和代码单步执行行为

有关C++项目中，可以指定模块、 源文件和函数**调用堆栈**窗口将视为非用户代码通过指定其 *\*.natjmc*文件。 此自定义也适用于单步执行，如果您使用的最新编译器的代码 (请参阅[C++仅我的代码](#BKMK_CPP_User_and_non_user_code))。

- 若要指定非用户代码的 Visual Studio 计算机所有用户，请添加 *.natjmc*的文件 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹。
- 若要指定为单个用户的非用户代码，请添加 *.natjmc*的文件 *%USERPROFILE%\My Documents\\< Visual Studio 版本\>\Visualizers*文件夹。

一个 *.natjmc*文件是 XML 文件使用以下语法：

```xml
<?xml version="1.0" encoding="utf-8"?>
<NonUserCode xmlns="http://schemas.microsoft.com/vstudio/debugger/jmc/2015">

  <!-- Modules -->
  <Module Name="ModuleSpec" />
  <Module Name="ModuleSpec" Company="CompanyName" />

  <!-- Files -->
  <File Name="FileSpec"/>

  <!-- Functions -->
  <Function Name="FunctionSpec" />
  <Function Name="FunctionSpec" Module ="ModuleSpec" />
  <Function Name="FunctionSpec" Module ="ModuleSpec" ExceptionImplementation="true" />

</NonUserCode>

```

 **模块元素属性**

|特性|描述|
|---------------|-----------------|
|`Name`|必需。 模块的完整路径。 可以使用 Windows 通配符`?`（零个或一个字符） 和`*`（零个或多个字符）。 例如，应用于对象的<br /><br /> `<Module Name="?:\3rdParty\UtilLibs\*" />`<br /><br /> 告知调试器中的所有模块都视为 *\3rdParty\UtilLibs* 外部代码的任何驱动器上。|
|`Company`|可选。 发布在可执行文件中嵌入的模块的公司的名称。 可以使用此特性消除模块歧义。|

 **文件元素属性**

|特性|描述|
|---------------|-----------------|
|`Name`|必需。 要视为外部代码的源文件的完整路径。 可以在指定路径时使用 Windows 通配符 `?` 和 `*`。|

 **函数元素属性**

|特性|描述|
|---------------|-----------------|
|`Name`|必需。 要视为外部代码的函数的完全限定的名称。|
|`Module`|可选。 包含函数的模块的名称或完整路径。 可以使用此特性区分具有相同名称的函数。|
|`ExceptionImplementation`|设置为 `true` 时，调用堆栈显示的是引发异常的函数，而不是此函数。|

### <a name="BKMK_CPP_Customize_stepping_behavior"></a> 自定义C++单步执行行为独立于仅我的代码设置

在C++项目中，可以指定要通过为非用户代码中单步函数 *\*.natstepfilter*文件。 中列出的函数 *\*.natstepfilter*文件不是依赖于仅我的代码设置。

- 若要指定非用户代码的所有本地 Visual Studio 用户，请添加 *.natstepfilter*的文件 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹。
- 若要指定为单个用户的非用户代码，请添加 *.natstepfilter*的文件 *%USERPROFILE%\My Documents\\< Visual Studio 版本\>\Visualizers*文件夹。

一个 *.natstepfilter*文件是 XML 文件使用以下语法：

```xml
<?xml version="1.0" encoding="utf-8"?>
<StepFilter xmlns="http://schemas.microsoft.com/vstudio/debugger/natstepfilter/2010">
    <Function>
        <Name>FunctionSpec</Name>
        <Action>StepAction</Action>
    </Function>
    <Function>
        <Name>FunctionSpec</Name>
        <Module>ModuleSpec</Module>
        <Action>StepAction</Action>
    </Function>
</StepFilter>

```

|元素|描述|
|-------------|-----------------|
|`Function`|必需。 将一个或多个函数指定为非用户函数。|
|`Name`|必需。 ECMA-262 格式的正则表达式，指定要匹配的完整函数名。 例如：<br /><br /> `<Name>MyNS::MyClass.*</Name>`<br /><br /> 告知调试器将 `MyNS::MyClass` 中的所有方法都视为非用户代码。 匹配区分大小写。|
|`Module`|可选。 ECMA-262 格式的正则表达式，指定包含函数的模块的完整路径。 匹配不区分大小写。|
|`Action`|必需。 以下区分大小写的值之一：<br /><br /> `NoStepInto`  -告知调试器单步执行函数。<br /> `StepInto`  -告知调试器单步执行函数，重写任何其他`NoStepInto`为匹配的函数。|

## <a name="BKMK_JavaScript_Just_My_Code"></a>JavaScript“仅我的代码”

<a name="BKMK_JS_User_and_non_user_code"></a>JavaScript“仅我的代码”控件通过采用以下分类之一对代码进行分类，来控制单步执行和调用堆栈显示：

|||
|-|-|
|**MyCode**|你拥有或控制的用户代码。|
|**LibraryCode**|定期使用的库和您的应用程序中的非用户代码依赖于能够正确 （例如 WinJS 或 jQuery）。|
|**UnrelatedCode**|您不拥有的应用程序和应用程序中的非用户代码不依赖才能正常工作。 例如，广告可以显示广告 SDK 可能是 UnrelatedCode。 在 UWP 项目中，加载到你的应用的 HTTP 或 HTTPS URI 的任何代码也被视为 UnrelatedCode。|

JavaScript 调试器将作为用户或按此顺序的非用户代码分为两类：

1. 默认分类中。
   - 通过将字符串传递给主机提供执行脚本`eval`技术支持部门**MyCode**。
   - 通过将字符串传递到执行脚本`Function`构造函数是**LibraryCode**。
   - 框架引用，如 WinJS 或 Azure SDK 中的脚本已**LibraryCode**。
   - 通过将字符串传递到执行脚本`setTimeout`， `setImmediate`，或`setInterval`functions 是**UnrelatedCode**。

2. 指定的所有 Visual Studio JavaScript 项目中的分类 *%VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json*文件。

3. 中的分类*mycode.json*当前项目的文件。

每个分类步骤都会重写前面的步骤。

其他所有代码都分类为“MyCode”。

您可以修改默认分类，并对其分类的特定文件和 Url 为用户或非用户代码，通过添加 *.json*名为的文件*mycode.json* JavaScript 项目的根文件夹。 请参阅[自定义 JavaScript 仅我的代码](#BKMK_JS_Customize_Just_My_Code)。

<a name="BKMK_JS_Stepping_behavior"></a> 在 JavaScript 调试：

- 如果函数为非用户代码**调试** > **单步执行**(或**F11**) 的行为与相同**调试** > **单步跳过**(或**F10**)。
- 如果某个步骤开始在非用户 (**LibraryCode**或**UnrelatedCode**) 代码中，暂时单步执行行为将如同未启用仅我的代码。 当返回到用户代码，仅我的代码单步单步执行是重新启用。
- 当用户代码步骤导致保留当前执行上下文时，调试器将停止在下一步执行的用户代码行。 例如，如果某个回调在“LibraryCode”代码中执行，则调试器会继续，直到执行下一行用户代码。
- **单步跳出**(或**Shift**+**F11**) 将在下一行用户代码处停止。

如果没有更多的用户代码，调试继续，直到它结束，到达另一个断点，或将引发错误。

始终命中在代码中设置断点，但代码进行分类。

- 如果`debugger`关键字出现在**LibraryCode**，调试器始终中断。
- 如果`debugger`关键字出现在**UnrelatedCode**，调试器不会停止。

<a name="BKMK_JS_Exception_behavior"></a> 如果在发生未经处理的异常**MyCode**或**LibraryCode**代码，调试器始终中断。

如果在发生未经处理的异常**UnrelatedCode**，并**MyCode**或**LibraryCode**位于调用堆栈，调试器中断。

如果异常，启用了第一机会异常，并且中发生的异常**LibraryCode**或**UnrelatedCode**:

- 如果异常已处理，则调试器不会中断。
- 如果异常未经过处理，则调试器中断。

### <a name="BKMK_JS_Customize_Just_My_Code"></a> 自定义 JavaScript 仅我的代码

若要将用户和非用户代码的单个 JavaScript 项目分类，可以添加 *.json*名为的文件*mycode.json*项目的根文件夹。

此文件中的说明重写默认分类和*mycode.default.wwa.json*文件。 *Mycode.json*文件不需要列出所有键/值对。 **MyCode**，**库**，并**Unrelated**值可以是空数组。

*Mycode.json*文件使用以下语法：

```json
{
    "Eval" : "Classification",
    "Function" : "Classification",
    "ScriptBlock" : "Classification",
    "MyCode" : [
        "UrlOrFileSpec",
        . . .
        "UrlOrFileSpec"
    ],
    "Libraries" : [
        "UrlOrFileSpec",
        . .
        "UrlOrFileSpec"
    ],
    "Unrelated" : [
        "UrlOrFileSpec",
        . . .
        "UrlOrFileSpec"
    ]
}

```

**Eval、Function 和 ScriptBlock**

“Eval”、“Function”和“ScriptBlock”键值对确定如何对动态生成的代码进行分类：

|||
|-|-|
|**Eval**|通过将字符串传递给主机提供的 `eval` 函数来执行的脚本。 默认情况下，Eval 脚本分类为“MyCode”。|
|**Function**|通过将字符串传递给 `Function` 构造函数来执行的脚本。 默认情况下，Function 脚本分类为“LibraryCode”。|
|**ScriptBlock**|通过将字符串传递给 `setTimeout`、`setImmediate` 或 `setInterval` 函数来执行的脚本。 默认情况下，ScriptBlock 脚本分类为“UnrelatedCode”。|

可以将值更改为以下关键字之一：

- `MyCode` 将脚本分类为“MyCode”。
- `Library` 将脚本分类为“LibraryCode”。
- `Unrelated` 将脚本分类为“UnrelatedCode”。

**MyCode、Libraries 和 Unrelated**

“MyCode”、“Libraries”和“Unrelated”键值对指定要包含在分类中的 URL 或文件：

|||
|-|-|
|**MyCode**|分类为“MyCode”的 URL 数组或文件数组。|
|**Libraries**|分类为“LibraryCode”的 URL 数组或文件数组。|
|**Unrelated**|分类为“UnrelatedCode”的 URL 数组或文件数组。|

URL 或文件字符串可以具有一个或多`*`匹配零个或多个字符的字符。 `*` 与正则表达式相同`.*`。
