---
title: 使用“仅我的代码”调试用户代码 | Microsoft Docs
ms.date: 02/13/2019
ms.topic: how-to
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 867477fd3e490f91e81fb91c8be267ede83c8d2c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536560"
---
# <a name="debug-only-user-code-with-just-my-code"></a>使用“仅我的代码”仅调试用户代码

“仅我的代码”是一项 Visual Studio 调试功能，可自动单步跳过系统、框架和其他非用户代码调用。 在“调用堆栈”窗口中，“仅我的代码”将这些调用折叠到 [External Code] 帧中 。

在 .NET、C++ 和 JavaScript 项目中，“仅我的代码”的工作方式有所不同。

## <a name="enable-or-disable-just-my-code"></a><a name="BKMK_Enable_or_disable_Just_My_Code"></a>启用或禁用“仅我的代码”

对于大多数编程语言，默认都启用“仅我的代码”。

- 要在 Visual Studio 中启用或禁用“仅我的代码”，请在“工具” > “选项”（或“调试” > “选项”）>“调试” > “常规”下，选择和取消选择“启用‘仅我的代码’”      。

![“选项”对话框中的“启用‘仅我的代码’”](../debugger/media/dbg_justmycode_options.png "启用“仅我的代码”")

> [!NOTE]
> “启用‘仅我的代码’”是全局设置，会应用于所有语言的全部 Visual Studio 项目。

## <a name="just-my-code-debugging"></a>“仅我的代码”调试

在调试会话期间，“模块”窗口会显示调试器将哪些代码模块视为“我的代码”（用户代码），以及其符号加载状态。 有关详细信息，请参阅[熟悉调试器如何附加到应用](../debugger/debugger-tips-and-tricks.md#modules_window)。

![“模块”窗口中的用户代码](../debugger/media/dbg_justmycode_module.png "“模块”窗口中的用户代码")

在“调用堆栈”或“任务”窗口中，“仅我的代码”将非用户代码折叠到标签为 `[External Code]` 的灰色带批注代码帧 。

![“调用堆栈”窗口中的 External Code 帧](../debugger/media/dbg_justmycode_externalcode.png "External Code 帧")

>[!TIP]
>必须处于调试会话才能打开“模块”、“调用堆栈”、“任务”或大多数其他调试窗口  。 调试时，在“调试” > “窗口”下，选择要打开的窗口 。

<a name="BKMK_Override_call_stack_filtering"></a> 要查看折叠的 [External Code] 帧中的代码，请在“调用堆栈”或“任务”窗口中右键单击，然后从上下文菜单中选择“显示外部代码”   。 展开的外部代码行将替换 [External Code] 帧。

![在“调用堆栈”窗口中显示外部代码](../debugger/media/dbg_justmycode_showexternalcode.png "显示外部代码")

> [!NOTE]
> “显示外部代码”是当前用户探查器设置，会应用于用户打开的所有语言的全部项目。

双击“调用堆栈”窗口中展开的外部代码行，将在源代码中以绿色突出显示调用代码行。 对于 DLL 或其他未找到或未加载的模块，可能会打开“找不到符号或源代码”页面。

## <a name="net-just-my-code"></a><a name="BKMK__NET_Framework_Just_My_Code"></a> .NET“仅我的代码”

在 .NET 项目中，“仅我的代码”使用符号 (.pdb) 文件和程序优化来区分用户和非用户代码。 .NET 调试器将优化的二进制文件和非加载的 .pdb 文件视为非用户代码。

还有三个编译器特性会影响 .NET 调试器视为用户代码的内容：

- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute> 告知调试器应用它的代码不是用户代码。
- <xref:System.Diagnostics.DebuggerHiddenAttribute> 对调试器隐藏代码，即使“仅我的代码”关闭；
- <xref:System.Diagnostics.DebuggerStepThroughAttribute> 告知调试器单步跳过而不是单步调试应用它的代码。

.NET 调试器将所有其他代码视为用户代码。

在 .NET 调试期间：

- 对非用户代码执行“调试” > “单步调试”（或 F11）会单步跳过该代码，转到下一行用户代码  。
- 对非用户代码执行“调试” > “单步跳出”（或 Shift+F11）会运行到下一行用户代码   。

如果没有更多的用户代码，调试将继续进行直到结束、命中另一个断点或者引发错误。

<a name="BKMK_NET_Breakpoint_behavior"></a> 如果调试器在非用户代码中中断（例如，使用“调试” > “全部中断”在非用户代码中暂停），则将显示“没有源代码”窗口  。 然后可以使用“调试” > “单步执行”命令来执行下一行用户代码 。

如果在非用户代码中出现未经处理的异常，则调试器会在生成异常的用户代码行处中断。

如果针对异常启用了第一机会异常，则在源代码中以绿色突出显示调用用户代码行。 “调用堆栈”窗口会显示标签为 [External Code] 的带批注帧 。

## <a name="c-just-my-code"></a><a name="BKMK_C___Just_My_Code"></a>C++“仅我的代码”

从 Visual Studio 2017 版本 15.8 开始，还支持使用“仅我的代码”来单步执行代码。 此功能还要求使用 [/JMC（仅我的代码调试）](/cpp/build/reference/jmc)编译器开关。 C++ 项目默认启用此开关。 对于“仅我的代码”中的“调用堆栈”窗口和调用堆栈支持，不需要 /JMC 开关。

<a name="BKMK_CPP_User_and_non_user_code"></a> 若要归类为用户代码，调试器必须加载包含用户代码的二进制文件的 PDB（使用“模块”窗口进行检查）。

对于调用堆栈行为，例如在“调用堆栈”窗口中，C++ 中的“仅我的代码”仅将以下函数视为非用户代码：

- 在其符号文件中去除了源信息的函数。
- 符号文件指示没有对应于堆栈帧的源文件的函数。
- %VsInstallDirectory%\Common7\Packages\Debugger\Visualizers 文件夹下 \*.natjmc 文件中指定的函数 。

对于代码单步执行行为，C++ 中的“仅我的代码”仅将以下函数视为非用户代码：

- 调试器尚未加载相应 PDB 文件的函数。
- %VsInstallDirectory%\Common7\Packages\Debugger\Visualizers 文件夹下 \*.natjmc 文件中指定的函数 。

> [!NOTE]
> 为了在“仅我的代码”中支持代码单步执行，必须在 Visual Studio 15.8 预览版 3 或更高版本中使用 MSVC 编译器来编译 C++ 代码，并且必须启用 /JMC 编译器开关（默认启用）。 有关其他详细信息，请参阅[自定义 C++ 调用堆栈和代码单步执行行为](#BKMK_CPP_Customize_call_stack_behavior)）和此[博客文章](https://devblogs.microsoft.com/cppblog/announcing-jmc-stepping-in-visual-studio/)。 对于使用较旧编译器编译的代码，.natstepfilter 文件是独立于“仅我的代码”设置自定义代码单步执行的唯一方法。 请参阅[自定义 C++ 单步执行行为](#BKMK_CPP_Customize_stepping_behavior)。

<a name="BKMK_CPP_Stepping_behavior"></a> 在 C++ 调试期间：

- 对非用户代码执行“调试” > “单步调试”（或 F11）会单步跳过该代码，转到下一行用户代码  。
- 对非用户代码执行“调试” > “单步跳出”（或 Shift+F11）会运行到下一行用户代码   。

如果没有更多的用户代码，调试将继续进行直到结束、命中另一个断点或者引发错误。

如果调试器在非用户代码中中断（例如，使用“调试” > “全部中断”在非用户代码中暂停），则会继续在非用户代码中单步执行 。

如果调试器遇到异常，它会在异常处停止，无论是处于用户还是非用户代码中。 会忽略“异常设置”对话框中的“用户未处理异常”选项 。

### <a name="customize-c-call-stack-and-code-stepping-behavior"></a><a name="BKMK_CPP_Customize_call_stack_behavior"></a> 自定义 C++ 调用堆栈和代码单步执行行为

对于 C++ 项目，可以指定“调用堆栈”窗口视为非用户代码的模块、源文件和函数，方法是在 \*.natjmc 文件中进行指定。 如果使用最新的编译器，则此自定义也适用于代码单步执行（请参阅 [C++“仅我的代码”](#BKMK_CPP_User_and_non_user_code)）。

- 要为 Visual Studio 计算机的所有用户指定非用户代码，请将 .natjmc 文件添加到 %VsInstallDirectory%\Common7\Packages\Debugger\Visualizers 文件夹 。
- 要为单个用户指定非用户代码，请将 .natjmc 文件添加到 %USERPROFILE%\My Documents\\<Visual Studio version\>\Visualizers 文件夹 。

.natjmc 文件是具有以下语法的 XML 文件：

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
|`Name`|必需。 模块的完整路径。 可以使用 Windows 通配符 `?`（零个或一个字符）和 `*`（零个或多个字符）。 例如，应用于对象的<br /><br /> `<Module Name="?:\3rdParty\UtilLibs\*" />`<br /><br /> 告知调试器中的所有模块都视为 *\3rdParty\UtilLibs* 外部代码的任何驱动器上。|
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

### <a name="customize-c-stepping-behavior-independent-of-just-my-code-settings"></a><a name="BKMK_CPP_Customize_stepping_behavior"></a> 独立于“仅我的代码”设置自定义 C++ 单步执行行为

在 C++ 项目中，可以通过在 \*.natstepfilter 文件中将函数列为非用户代码来指定要单步跳过的函数。 \*.natstepfilter 文件中列出的函数独立于“仅我的代码”设置。

- 要为所有 Visual Studio 本地用户指定非用户代码，请将 .natstepfilter 文件添加到 %VsInstallDirectory%\Common7\Packages\Debugger\Visualizers 文件夹 。
- 要为单个用户指定非用户代码，请将 .natstepfilter 文件添加到 %USERPROFILE%\My Documents\\<Visual Studio version\>\Visualizers 文件夹 。

.natstepfilter 文件是具有以下语法的 XML 文件：

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
|`Action`|必需。 以下区分大小写的值之一：<br /><br /> `NoStepInto` - 告知调试器单步跳过函数。<br /> `StepInto` - 告知调试器单步调试函数，为匹配的函数重写任何其他 `NoStepInto`。|

## <a name="javascript-just-my-code"></a><a name="BKMK_JavaScript_Just_My_Code"></a>JavaScript“仅我的代码”

<a name="BKMK_JS_User_and_non_user_code"></a>JavaScript“仅我的代码”控件通过采用以下分类之一对代码进行分类，来控制单步执行和调用堆栈显示：

|分类|描述|
|-|-|
|**MyCode**|你拥有或控制的用户代码。|
|**LibraryCode**|你定期使用的库中以及应用必需具备才能正常运行（例如 WinJS 或 jQuery）的非用户代码。|
|**UnrelatedCode**|非自有应用中或应用无需具备也能正常运行的非用户代码。 例如，显示广告的广告 SDK 可能是 UnrelatedCode。 在 UWP 项目中，从 HTTP 或 HTTPS URI 加载到应用中的任何代码也被视为 UnrelatedCode。|

JavaScript 调试器按照以下顺序归类为用户代码或非用户代码：

1. 默认分类。
   - 通过将字符串传递给主机提供的 `eval` 函数来执行的脚本为 MyCode。
   - 通过将字符串传递给 `Function` 构造函数来执行的脚本为 LibraryCode。
   - 框架引用（如 WinJS 或 Azure SDK）中的脚本为 LibraryCode。
   - 通过将字符串传递给 `setTimeout`、`setImmediate` 或 `setInterval` 函数来执行的脚本为 UnrelatedCode。

2. 为 %VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json 文件中的所有 Visual Studio JavaScript 项目指定的分类 。

3. 当前项目的 mycode.json 文件中的分类。

每个分类步骤都会重写前面的步骤。

其他所有代码都分类为“MyCode”。

可以通过将一个名为 mycode.json 的 .json 文件添加到 JavaScript 项目的根文件夹，来修改默认分类并将特定文件和 URL 分类为用户或非用户代码 。 请参阅[自定义 JavaScript“仅我的代码”](#BKMK_JS_Customize_Just_My_Code)。

<a name="BKMK_JS_Stepping_behavior"></a> 在 JavaScript 调试期间：

- 如果某个函数为非用户代码，则“调试” > “单步调试”（或 F11）的行为与“调试” > “单步跳过”（或 F10）相同     。
- 如果某个步骤在非用户（LibraryCode 或 UnrelatedCode）代码中开始，则单步执行的行为方式会暂时如同未启用“仅我的代码” 。 单步返回用户代码中时，会重启“仅我的代码”单步执行。
- 当用户代码单步执行导致退出当前的执行上下文时，调试器将在下一个已执行的用户代码行处停止。 例如，如果某个回调在“LibraryCode”代码中执行，则调试器会继续，直到执行下一行用户代码。
- 单步跳出（或 Shift+F11）会在下一行用户代码上停止  。

如果没有更多的用户代码，调试将继续进行直到结束、命中另一个断点或者引发错误。

始终命中代码中设置的断点，但会对代码进行分类。

- 如果 LibraryCode 中出现 `debugger` 关键字，调试器将始终中断。
- 如果 UnrelatedCode 中出现 `debugger` 关键字，调试器不会停止。

<a name="BKMK_JS_Exception_behavior"></a> 如果 MyCode 中发生未经处理的异常或 LibraryCode 代码，调试器将始终中断 。

如果 UnrelatedCode 中发生未经处理的异常，并且 MyCode 或 LibraryCode 位于调用堆栈上，调试器将中断  。

如果针对异常启用了第一机会异常，并且在 LibraryCode 或 UnrelatedCode 中发生异常 ：

- 如果异常已处理，则调试器不会中断。
- 如果异常未经过处理，则调试器中断。

### <a name="customize-javascript-just-my-code"></a><a name="BKMK_JS_Customize_Just_My_Code"></a> 自定义 JavaScript“仅我的代码”

要针对单个 JavaScript 项目对用户和非用户代码进行分类，可以将一个名为 mycode.json 的 .json 文件添加到该项目的根文件夹 。

此文件中的规范将替代默认分类和 mycode.default.wwa.json 文件。 mycode.json 文件不需要列出所有键值对。 MyCode、Libraries 和 Unrelated 值可为空数组  。

Mycode.json 文件使用以下语法：

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

“Eval”、“Function”和“ScriptBlock”键值对确定如何对动态生成的代码进行分类  ：

|“属性”|描述|
|-|-|
|**Eval**|通过将字符串传递给主机提供的 `eval` 函数来执行的脚本。 默认情况下，Eval 脚本分类为“MyCode”。|
|**Function**|通过将字符串传递给 `Function` 构造函数来执行的脚本。 默认情况下，Function 脚本分类为“LibraryCode”。|
|**ScriptBlock**|通过将字符串传递给 `setTimeout`、`setImmediate` 或 `setInterval` 函数来执行的脚本。 默认情况下，ScriptBlock 脚本分类为“UnrelatedCode”。|

可以将值更改为以下关键字之一：

- `MyCode` 将脚本分类为“MyCode”。
- `Library` 将脚本分类为“LibraryCode”。
- `Unrelated` 将脚本分类为“UnrelatedCode”。

**MyCode、Libraries 和 Unrelated**

“MyCode”、“Libraries”和“Unrelated”键值对指定要包含在分类中的 URL 或文件  ：

|“属性”|描述|
|-|-|
|**MyCode**|分类为“MyCode”的 URL 数组或文件数组。|
|**Libraries**|分类为“LibraryCode”的 URL 数组或文件数组。|
|**Unrelated**|分类为“UnrelatedCode”的 URL 数组或文件数组。|

URL 或文件字符串可以包含一个或多个 `*` 字符，这些字符匹配零个或多个字符。 `*` 与正则表达式 `.*` 相同。
