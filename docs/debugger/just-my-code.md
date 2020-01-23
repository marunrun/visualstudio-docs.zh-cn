---
title: 用仅我的代码调试用户代码 |Microsoft Docs
ms.date: 02/13/2019
ms.topic: conceptual
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c1d474b388dd8f116eb53febb8a472d4c5b8150
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535995"
---
# <a name="debug-only-user-code-with-just-my-code"></a>仅调试具有仅我的代码的用户代码

*仅我的代码*是一种 Visual Studio 调试功能，可自动执行对系统、框架和其他非用户代码的调用。 在 "**调用堆栈**" 窗口中，仅我的代码将这些调用折叠到 **[外部代码]** 帧中。

在 .NET、 C++和 JavaScript 项目中，仅我的代码的工作方式有所不同。

## <a name="BKMK_Enable_or_disable_Just_My_Code"></a>启用或禁用“仅我的代码”

对于大多数编程语言，默认情况下启用仅我的代码。

- 若要在 Visual Studio 中启用或禁用仅我的代码，请在 "**工具**"  > **选项**"（或"**调试** > **选项**"） >**调试** > **常规**"，选择或取消选择 "**启用仅我的代码**"。

![在 "选项" 对话框中启用仅我的代码](../debugger/media/dbg_justmycode_options.png "启用“仅我的代码”")

> [!NOTE]
> **启用仅我的代码**是一项全局设置，适用于所有语言的所有 Visual Studio 项目。

## <a name="just-my-code-debugging"></a>“仅我的代码”调试

在调试会话期间，"**模块**" 窗口显示调试器将哪个代码模块视为我的代码（用户代码）以及其符号加载状态。 有关详细信息，请参阅[更熟悉调试器如何附加到你的应用程序](../debugger/debugger-tips-and-tricks.md#modules_window)。

!["模块" 窗口中的用户代码](../debugger/media/dbg_justmycode_module.png "\"模块\" 窗口中的用户代码")

在 "**调用堆栈**" 或 "**任务**" 窗口中，仅我的代码将非用户代码折叠成标记为 `[External Code]` 的灰色批注代码框架。

!["调用堆栈" 窗口中的外部代码帧](../debugger/media/dbg_justmycode_externalcode.png "外部代码框架")

>[!TIP]
>若要打开**模块**、**调用堆栈**、**任务**或大多数其他调试窗口，必须在调试会话中。 调试时，在 "**调试**"  > **窗口**下，选择要打开的窗口。

<a name="BKMK_Override_call_stack_filtering"></a>若要查看折叠的 **[外部代码]** 帧中的代码，请在 "**调用堆栈**" 或 "**任务**" 窗口中单击右键，然后从上下文菜单中选择 "**显示外部代码**"。 展开的外部代码行替换 **[外部代码**] 框架。

![在 "调用堆栈" 窗口中显示外部代码](../debugger/media/dbg_justmycode_showexternalcode.png "显示外部代码")

> [!NOTE]
> **显示外部代码**是当前用户探查器设置，适用于用户打开的所有语言的所有项目。

在 "**调用堆栈**" 窗口中双击展开的外部代码行会在源代码中突出显示以绿色显示的调用代码行。 对于 Dll 或未找到或加载的其他模块，可能会打开 "符号或源找不到" 页。

## <a name="BKMK__NET_Framework_Just_My_Code"></a>.NET 仅我的代码

在 .NET 项目中，仅我的代码使用符号（ *.pdb*）文件和程序优化来对用户和非用户代码进行分类。 .NET 调试器将优化的二进制文件和非加载 *.pdb*文件视为非用户代码。

这三个编译器属性还会影响 .NET 调试器认为是用户代码：

- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute> 通知调试器，它应用到的代码不是用户代码。
- <xref:System.Diagnostics.DebuggerHiddenAttribute> 对调试器隐藏代码，即使“仅我的代码”关闭；
- <xref:System.Diagnostics.DebuggerStepThroughAttribute> 通知调试器遍历应用到的代码，而不是单步执行代码。

.NET 调试器将所有其他代码视为用户代码。

在 .NET 调试期间：

- **调试** > **单步执行**（或按**F11**）在非用户代码上逐过程执行代码，并将代码移到用户代码的下一行。
- **调试** >  非用户代码上的 "**跳出**" （或**Shift** +**F11**）运行到用户代码的下一行。

如果没有更多的用户代码，调试将继续，直到它结束、到达另一个断点或引发错误。

<a name="BKMK_NET_Breakpoint_behavior"></a>如果调试器在非用户代码中中断（例如，在非用户代码中使用 "**调试**"  >  "**全部中断**" 和 "暂停"），则不会显示 "**无源**" 窗口。 然后，你可以使用 "**调试** > **步骤**" 命令来执行用户代码的下一行。

如果非用户代码中出现未经处理的异常，调试器将在生成异常的用户代码行处中断。

如果对异常启用了第一次机会异常，则调用用户代码行在源代码中以绿色突出显示。 "**调用堆栈**" 窗口显示标记为 **[外部代码]** 的带批注的帧。

## <a name="BKMK_C___Just_My_Code"></a>C++“仅我的代码”

从 Visual Studio 2017 15.8 版开始，还支持代码单仅我的代码。 此功能还要求使用[/JMC （仅我的代码调试）](/cpp/build/reference/jmc)编译器开关。 默认情况下，在项目中C++启用此开关。 对于 "**调用堆栈**" 窗口和仅我的代码中的调用堆栈支持，不需要/JMC 开关。

<a name="BKMK_CPP_User_and_non_user_code"></a>若要归类为用户代码，必须由调试器加载包含用户代码的二进制文件的 PDB （使用 "**模块**" 窗口进行检查）。

对于调用堆栈行为（如 "**调用堆栈**" 窗口中的）， C++中的仅我的代码仅将这些函数视为*非用户代码*：

- 在其符号文件中去除了源信息的函数。
- 符号文件指示没有对应于堆栈帧的源文件的函数。
- *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹中 *\* natjmc*文件中指定的函数。

对于代码单步执行行为， C++仅我的代码仅将这些函数视为*非用户代码*：

- 调试器中尚未加载相应的 PDB 文件的函数。
- *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹中 *\* natjmc*文件中指定的函数。

> [!NOTE]
> 为了仅我的代码中的代码步进支持C++ ，必须在 Visual Studio 15.8 Preview 3 或更高版本中使用 MSVC 编译器来编译代码，并且必须启用/JMC 编译器开关（默认情况下启用）。 有关更多详细信息[， C++请参阅此](#BKMK_CPP_Customize_call_stack_behavior)[博客文章](https://devblogs.microsoft.com/cppblog/announcing-jmc-stepping-in-visual-studio/)。 对于使用较旧的编译器编译的代码， *. natstepfilter* files 是自定义代码单步执行的唯一方法，该方法与仅我的代码无关。 请[参阅C++自定义单步执行行为](#BKMK_CPP_Customize_stepping_behavior)。

<a name="BKMK_CPP_Stepping_behavior"></a>调试C++期间：

- **调试** > **单步执行**（或按**F11**）在非用户代码上逐过程执行代码，并将代码移到用户代码的下一行。
- **调试** >  非用户代码上的 "**跳出**" （或**Shift** +**F11**）运行到用户代码的下一行。

如果没有更多的用户代码，调试将继续，直到它结束、到达另一个断点或引发错误。

如果调试器在非用户代码中中断（例如，在非用户代码中使用 "**调试**"  >  "**全部中断**" 和 "暂停"），则在非用户代码中继续执行。

如果调试器遇到异常，则它会在异常上停止，无论它是在用户代码还是非用户代码中。 "**异常设置**" 对话框中的**用户未处理**的选项将被忽略。

### <a name="BKMK_CPP_Customize_call_stack_behavior"></a>自C++定义调用堆栈和代码单步执行行为

对于C++项目，可以指定模块、源文件和函数，"**调用堆栈**" 窗口将其视为非用户代码，方法是在 *\* natjmc*文件中指定它们。 如果使用的是最新的编译器，此自定义也适用于代码单步执行（请参阅[ C++仅我的代码](#BKMK_CPP_User_and_non_user_code)）。

- 若要为 Visual Studio 计算机的所有用户指定非用户代码，请将*natjmc*文件添加到 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹。
- 若要为单个用户指定非用户代码，请将*natjmc*文件添加到 *%USERPROFILE%\My 文档 \\ < Visual Studio 版本 \> \visualizers*文件夹中。

*Natjmc*文件是具有以下语法的 XML 文件：

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
|`Name`|必须的。 模块的完整路径。 可以使用 Windows 通配符 `?` （零个或一个字符）和 `*` （零个或多个字符）。 例如，应用于对象的<br /><br /> `<Module Name="?:\3rdParty\UtilLibs\*" />`<br /><br /> 告知调试器中的所有模块都视为 *\3rdParty\UtilLibs* 外部代码的任何驱动器上。|
|`Company`|可选。 发布在可执行文件中嵌入的模块的公司的名称。 可以使用此特性消除模块歧义。|

 **文件元素属性**

|特性|描述|
|---------------|-----------------|
|`Name`|必须的。 要视为外部代码的源文件的完整路径。 可以在指定路径时使用 Windows 通配符 `?` 和 `*`。|

 **函数元素属性**

|特性|描述|
|---------------|-----------------|
|`Name`|必须的。 要视为外部代码的函数的完全限定的名称。|
|`Module`|可选。 包含函数的模块的名称或完整路径。 可以使用此特性区分具有相同名称的函数。|
|`ExceptionImplementation`|设置为 `true` 时，调用堆栈显示的是引发异常的函数，而不是此函数。|

### <a name="BKMK_CPP_Customize_stepping_behavior"></a>自C++定义独立于仅我的代码设置的单步执行行为

在C++项目中，可以通过将函数作为 *\** 文件中的非用户代码列出来指定要逐过程执行的函数。 *@No__t_1*文件中列出的函数不依赖于仅我的代码设置。

- 若要为所有本地 Visual Studio 用户指定非用户代码，请将*natstepfilter*文件添加到 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*文件夹。
- 若要为单个用户指定非用户代码，请将*natstepfilter*文件添加到 *%USERPROFILE%\My 文档 \\ < Visual Studio 版本 \> \visualizers*文件夹中。

*Natstepfilter*文件是具有以下语法的 XML 文件：

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
|`Function`|必须的。 将一个或多个函数指定为非用户函数。|
|`Name`|必须的。 ECMA-262 格式的正则表达式，指定要匹配的完整函数名。 例如:<br /><br /> `<Name>MyNS::MyClass.*</Name>`<br /><br /> 告知调试器将 `MyNS::MyClass` 中的所有方法都视为非用户代码。 匹配区分大小写。|
|`Module`|可选。 ECMA-262 格式的正则表达式，指定包含函数的模块的完整路径。 匹配不区分大小写。|
|`Action`|必须的。 以下区分大小写的值之一：<br /><br /> `NoStepInto`-通知调试器逐过程执行该函数。<br /> `StepInto`-通知调试器单步执行函数，并重写匹配函数的任何其他 `NoStepInto`。|

## <a name="BKMK_JavaScript_Just_My_Code"></a>JavaScript“仅我的代码”

<a name="BKMK_JS_User_and_non_user_code"></a>JavaScript“仅我的代码”控件通过采用以下分类之一对代码进行分类，来控制单步执行和调用堆栈显示：

|||
|-|-|
|**MyCode**|你拥有或控制的用户代码。|
|**LibraryCode**|你经常使用的库中的非用户代码，你的应用程序依赖于正常工作（例如 WinJS 或 jQuery）。|
|**UnrelatedCode**|应用中不具备的非用户代码，你的应用程序不依赖于正常运行。 例如，显示广告的广告 SDK 可能会 UnrelatedCode。 在 UWP 项目中，从 HTTP 或 HTTPS URI 加载到应用中的任何代码也被视为 UnrelatedCode。|

JavaScript 调试器按照此顺序将代码归类为 "用户" 或 "非用户"：

1. 默认分类。
   - 通过将字符串传递给宿主提供的 `eval` 函数执行的脚本为**MyCode**。
   - 通过将字符串传递给 `Function` 构造函数来执行的脚本为**LibraryCode**。
   - 框架引用中的脚本（如 WinJS 或 Azure SDK）为**LibraryCode**。
   - 通过将字符串传递到 `setTimeout`、`setImmediate` 或 `setInterval` 函数来执行的脚本为**UnrelatedCode**。

2. 为 *%VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json*文件中的所有 Visual Studio JavaScript 项目指定的分类。

3. 当前项目的*mycode*文件中的分类。

每个分类步骤都会重写前面的步骤。

其他所有代码都分类为“MyCode”。

通过将名为*mycode*的*json*文件添加到 JavaScript 项目的根文件夹，可以修改默认分类，并将特定文件和 url 作为用户或非用户代码进行分类。 请参阅[自定义 JavaScript 仅我的代码](#BKMK_JS_Customize_Just_My_Code)。

<a name="BKMK_JS_Stepping_behavior"></a>在 JavaScript 调试期间：

- 如果某个函数为非用户代码，则**debug**  > **单步执行**（或按**F11**）的行为与**Debug**  > **逐过程**（或按**F10**）相同。
- 如果某个步骤以非用户（**LibraryCode**或**UnrelatedCode**）代码开始，则单步执行会暂时表现为不启用仅我的代码。 当你返回到用户代码时，仅我的代码单步执行将重新启用。
- 当用户代码步骤导致保留当前的执行上下文时，调试器将在下一个已执行的用户代码行处停止。 例如，如果某个回调在“LibraryCode”代码中执行，则调试器会继续，直到执行下一行用户代码。
- **跳出**（或**Shift** +**F11**）将在用户代码的下一行停止。

如果没有更多的用户代码，调试将继续，直到它结束、到达另一个断点或引发错误。

始终命中代码中设置的断点，但会对代码进行分类。

- 如果 `debugger` 关键字出现在**LibraryCode**中，则调试器始终中断。
- 如果 `debugger` 关键字出现在**UnrelatedCode**中，则调试器不会停止。

<a name="BKMK_JS_Exception_behavior"></a>如果**MyCode**或**LibraryCode**代码中出现未经处理的异常，调试器将始终中断。

如果**UnrelatedCode**中发生未处理的异常，并且**MyCode**或**LibraryCode**在调用堆栈上，则调试器中断。

如果对异常启用了第一次异常，则会在**LibraryCode**或**UnrelatedCode**中出现异常：

- 如果异常已处理，则调试器不会中断。
- 如果异常未经过处理，则调试器中断。

### <a name="BKMK_JS_Customize_Just_My_Code"></a>自定义 JavaScript 仅我的代码

若要对单个 JavaScript 项目的用户和非用户代码进行分类，可以将名为*mycode*的*json*文件添加到项目的根文件夹中。

此文件中的规范将覆盖默认的分类和*wwa*文件。 *Mycode*文件不需要列出所有键值对。 **MyCode**、**库**和**无关**的值可以为空数组。

*Mycode*文件使用以下语法：

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

URL 或文件字符串可以包含一个或多个 `*` 字符，这些字符与零个或多个字符匹配。 `*` 与正则表达式 `.*` 相同。
