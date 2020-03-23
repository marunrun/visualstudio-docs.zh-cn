---
title: 只是我的代码 |微软文档
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: efcabf9c7dc201f95515cd24bf3a14727f7149fe
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301391"
---
# <a name="just-my-code"></a>仅我的代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用.NET Framework 语言的开发人员熟悉“仅我的代码”调试器功能，该功能会逐过程执行系统、框架和其他非用户调用，并在调用堆栈窗口中折叠这些调用。 “仅我的代码”已扩展到 C++ 和 JavaScript 语言。 本主题介绍在 .NET Framework、本机 C++ 和 JavaScript 项目中使用“仅我的代码”的具体信息。  
  
## <a name="enable-or-disable-just-my-code"></a><a name="BKMK_Enable_or_disable_Just_My_Code"></a>启用或禁用“仅我的代码”  
 要启用或禁用"仅我的代码"，请选择 **"调试**"菜单上**的选项和设置**。 在**调试** / **常规**节点中，选择或清除**仅启用我的代码**。  
  
 ![“选项”对话框中的“启用‘仅我的代码’”](../debugger/media/dbg-justmycode-options.png "DBG_JustMyCode_Options")  
  
> [!NOTE]
> "**仅启用我的代码"** 设置是一个全局设置，应用于所有语言的所有 Visual Studio 项目。  
  
### <a name="override-call-stack-filtering"></a><a name="BKMK_Override_call_stack_filtering"></a>覆盖调用堆栈筛选  
 在调用堆栈显示中（如“调用堆栈”和“任务”窗口），“仅我的代码”会将非用户代码折叠为带有标签 `[External Code]` 的带批注帧。 要查看折叠帧，请选择调用堆栈显示的上下文菜单上显示**外部代码**。  
  
> [!NOTE]
> "**显示外部代码"** 设置将保存到当前用户的探查器中。 它会应用于所有语言中由用户打开的所有项目。  
  
## <a name="net-framework-just-my-code"></a><a name="BKMK__NET_Framework_Just_My_Code"></a>.NET 框架只是我的代码  
  
### <a name="user-and-non-user-code"></a><a name="BKMK_NET_User_and_non_user_code"></a>用户和非用户代码  
 为了区分用户代码和非用户代码，仅我的代码将查看符号 （.pdb） 文件和程序优化。 当二进制文件进行了优化时或当 .pdb 文件不可用时，调试器会将代码视为非用户代码。  
  
 还有三个特性会影响调试器视为“我的代码”的内容：  
  
- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute> 告知调试器应用它的代码不是“我的代码”。  
  
- <xref:System.Diagnostics.DebuggerHiddenAttribute> 对调试器隐藏代码，即使“仅我的代码”关闭；  
  
- <xref:System.Diagnostics.DebuggerStepThroughAttribute> 告知调试器逐句通过其所应用的代码，而不是单步执行代码。  
  
  将所有其他代码都视为用户代码。  
  
### <a name="stepping-behavior"></a><a name="BKMK_NET_Stepping_behavior"></a>步进行为  
 当您**进入**（键盘快捷方式：F11）非用户代码时，调试器将代码执行到下一个用户语句。 **当您退出**（键盘：移位 + F11）时，调试器将运行到下一行用户代码。 如果未遇到用户代码，则执行会继续，直到应用退出、命中断点或发生异常。  
  
### <a name="breakpoint-behavior"></a><a name="BKMK_NET_Breakpoint_behavior"></a>断点行为  
 启用"仅我的代码"后，您可以选择 **"全部中断**"（键盘：Ctrl + Alt = 中断），并在没有要显示的用户代码的位置停止执行。 发生这种情况时，会显示“无源”窗口。 如果随后选择“单步执行”命令，则调试器会到达下一行用户代码。  
  
### <a name="exception-behavior"></a><a name="BKMK_NET_Exception_behavior"></a>异常行为  
 如果在非用户代码中出现未经处理的异常，则调试器会在用户代码中生成异常的行上中断。  
  
 如果针对异常启用了第一机会异常，则以绿色突出显示用户代码行。 调用堆栈显示标记为 **[外部代码]** 的带标签的帧。  
  
## <a name="c-just-my-code"></a><a name="BKMK_C___Just_My_Code"></a>C++“仅我的代码”  
  
### <a name="user-and-non-user-code"></a><a name="BKMK_CPP_User_and_non_user_code"></a>用户和非用户代码  
 C++“仅我的代码”与 .NET Framework 和 JavaScript“仅我的代码”不同，因为单步执行行为独立于调用堆栈行为。  
  
 **调用堆栈**  
  
 默认情况下，调试器会将以下这些函数视为调用堆栈窗口中的非用户代码：  
  
- 在其符号文件中去除了源信息的函数。  
  
- 符号文件指示没有对应于堆栈帧的源文件的函数。  
  
- `%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers` 文件夹的 `*.natjmc` 文件中指定的函数。  
  
  **单步执行**  
  
  默认情况下，仅将 `%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers` 文件夹的 `*.natstepfilter` 文件中指定的函数视为非用户代码。  
  
  可以在 `%USERPROFILE%\My Documents\Visual Studio 2015\Visualizers` 中创建自己的 `.natstepfilter` 和 `.natjmc` 以自定义单步执行和调用堆栈窗口行为。  
  
### <a name="stepping-behavior"></a><a name="BKMK_CPP_Stepping_behavior"></a>步进行为  
 当您从用户代码**进入**（键盘快捷方式：F11）非用户代码时，调试器将执行代码到下一行用户代码。 **当您退出**（键盘：移位 + F11）时，调试器将运行到下一行用户代码。 如果未遇到用户代码，则执行会继续，直到应用退出、命中断点或发生异常。  
  
 如果调试器在非用户代码中中断（例如，如果“全部中断”命令在非用户代码中停止），则单步执行会继续在非用户代码中进行。  
  
### <a name="exception-behavior"></a><a name="BKMK_CPP_Exception_behavior"></a>异常行为  
 当调试器遇到异常时，它会异常处停止，而不考虑是处于用户还是非用户代码中。 忽略 **"例外"** 对话框中的 **"用户未处理**"选项。  
  
### <a name="customize-stepping-behavior"></a><a name="BKMK_CPP_Customize_stepping_behavior"></a>自定义步进行为  
 可以通过在 `*.natstepfilter` 文件中将函数列为非用户代码来指定要逐过程执行的函数。  
  
- 要为 Visual Studio 计算机的所有用户指定非用户代码，请将 .natstepfilter 文件`%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers`添加到文件夹中。  
  
- 要为单个用户指定非用户代码，请将 .natstep 筛选器文件添加到`%USERPROFILE%\My Documents\Visual Studio 2015\Visualizers`文件夹中。  
  
  .natstep 筛选器文件是具有此语法的 xml 文件：  
  
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
  
|元素|说明|  
|-------------|-----------------|  
|函数|必需。 将一个或多个函数指定为非用户函数。|  
|`Name`|必需。 ECMA-262 格式的正则表达式，指定要匹配的完整函数名。 例如：<br /><br /> `<Name>MyNS::MyClass.*</Name>`<br /><br /> 告知调试器将 `MyNS::MyClass` 中的所有方法都视为非用户代码。 匹配区分大小写。|  
|`Module`|可选。 ECMA-262 格式的正则表达式，指定包含函数的模块的完整路径。 匹配不区分大小写。|  
|`Action`|必需。 以下区分大小写的值之一：<br /><br /> -   `NoStepInto`• 告诉调试器踩过匹配的函数。<br />-   `StepInto`• 告诉调试器进入匹配的函数，重写匹配函数的任何其他`NoStepInto`函数。|  
  
### <a name="customize-call-stack-behavior"></a><a name="BKMK_CPP_Customize_call_stack_behavior"></a>自定义调用堆栈行为  
 可以通过在 `*.natjmc` 文件中指定模块、源文件和函数，将它们指定视为调用堆栈中的非用户代码。  
  
- 要为 Visual Studio 计算机的所有用户指定非用户代码，请将 .natjmc 文件`%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers`添加到文件夹中。  
  
- 要为单个用户指定非用户代码，请将 .natjmc 文件添加到`%USERPROFILE%\My Documents\Visual Studio 2015\Visualizers`文件夹中。  
  
  .natjmc 文件是具有此语法的 xml 文件：  
  
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
  
|Attribute|说明|  
|---------------|-----------------|  
|`Name`|必需。 模块的完整路径。 可以使用 Windows 通配符 `?`（零个或一个字符）和 `*`（零个或多个字符）。 例如，<br /><br /> `<Module Name=”?:\3rdParty\UtilLibs\*” />`<br /><br /> 告知调试器将任何驱动器上的 `\3rdParty\UtilLibs` 中的所有模块都视为外部代码。|  
|`Company`|可选。 发布在可执行文件中嵌入的模块的公司的名称。 可以使用此特性消除模块歧义。|  
  
 **文件元素特性**  
  
|Attribute|说明|  
|---------------|-----------------|  
|`Name`|必需。 要视为外部代码的源文件的完整路径。 可以在指定路径时使用 Windows 通配符 `?` 和 `*`。|  
  
 **函数元素属性**  
  
|Attribute|说明|  
|---------------|-----------------|  
|`Name`|必需。 要视为外部代码的函数的完全限定的名称。|  
|`Module`|可选。 包含函数的模块的名称或完整路径。 可以使用此特性区分具有相同名称的函数。|  
|`ExceptionImplementation`|设置为 `true` 时，调用堆栈显示的是引发异常的函数，而不是此函数。|  
  
## <a name="javascript-just-my-code"></a><a name="BKMK_JavaScript_Just_My_Code"></a>JavaScript“仅我的代码”  
  
### <a name="user-and-non-user-code"></a><a name="BKMK_JS_User_and_non_user_code"></a>用户和非用户代码  
 **代码分类**  
  
 JavaScript“仅我的代码”控件通过采用以下分类之一对代码进行分类，来控制单步执行和调用堆栈显示：  
  
|||  
|-|-|  
|**MyCode**|你拥有或控制的用户代码。|  
|**LibraryCode**|库中由你定期使用以及应用程序为正常运行而依赖的非用户代码（例如 WinJS 或 jQuery）。|  
|**UnrelatedCode**|可能在应用程序中运行的非用户代码，但您不拥有，并且应用程序不会直接依赖它正常运行（例如，显示广告的广告 SDK）。 在 Windows 应用商店项目中，从 HTTP 或 HTTPS URI 加载到应用中的任何代码也被视为 UnrelatedCode。|  
  
 JavaScript 调试器会自动对这些类型的代码进行分类：  
  
- 通过将字符串传递到主机提供的`eval`函数执行的脚本被归类为**MyCode**。  
  
- 通过将字符串传递给构造函数执行的`Function`脚本被归类为**库代码**。  
  
- 包含在框架引用中的脚本（如 WinJS 或 Azure SDK）被归类为**库代码**。  
  
- 通过将字符串传递到`setTimeout`，`setImmediate`或`setInterval`函数执行的脚本被归类为**不相关的代码**。  
  
- `%VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json` 为所有 Visual Studio JavaScript 项目指定其他用户和非用户代码。  
  
  可以通过将一个名为 `mycode.json` 的 .json 文件添加到项目的根文件夹，来修改默认分类以及对特定文件和 url 进行分类。  
  
  其他所有代码都分类为“MyCode”****。  
  
### <a name="stepping-behavior"></a><a name="BKMK_JS_Stepping_behavior"></a>步进行为  
  
- 如果函数不是用户 （**MyCode**） 代码，**则"进入**"（键盘快捷方式：F11）的行为为 **"单步执行**"（键盘：F10）。  
  
- 如果步骤从非用户 （**库代码**或不**相关的代码**） 代码中开始，则步进会暂时执行，就像未启用"仅我的代码"一样。 单步执行返回到用户代码中时，“仅我的代码”单步执行会立即重新启用。  
  
- 用户代码中的单步执行导致保留当前执行上下文（如对事件处理程序的最后一行进行单步执行）时，调试器会在执行的下一行用户代码处停止。 例如，如果在**库库代码**中执行回调，调试器将继续，直到执行下一行用户代码。  
  
- **步出**（键盘：移位 + F11）停止在下一行用户代码上。 如果未遇到用户代码，则执行会继续，直到应用退出、命中断点或发生异常。  
  
### <a name="breakpoint-behavior"></a><a name="BKMK_JS_Breakpoint_behavior"></a>断点行为  
  
- 在任何代码中设置的断点都始终会命中（无论该代码如何分类）。  
  
- 如果在以下内容中遇到 `debugger` 关键字：  
  
  - **库代码**，调试器总是中断。  

  - **不相关的代码**，调试器不会停止。  
  
### <a name="exception-behavior"></a><a name="BKMK_JS_Exception_behavior"></a>异常行为  
 如果在以下内容中出现未经处理的异常：  
  
- **MyCode**或**库代码**，调试器总是中断。  
  
- **不相关的代码**，以及**MyCode**或**库代码**位于调用堆栈上，调试器中断。  
  
  如果"例外"对话框上的异常启用了第一次机会异常，并且该异常在**库库代码**或不**相关的代码**中引发：  
  
- 如果异常经过了处理，则调试器不会中断。  
  
- 如果异常未经过处理，则调试器中断。  
  
### <a name="customize-just-my-code"></a><a name="BKMK_JS_Customize_Just_My_Code"></a>仅自定义我的代码  
 若要针对单个 Visual Studio 项目对用户和非用户代码进行分类，请将一个名为 `mycode.json` 的 .json 文件添加到该项目的根文件夹。  
  
 按以下顺序执行分类：  
  
1. 默认分类  
  
2. `%VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json` 文件中的分类  
  
3. 当前项目的 `mycode. json` 文件中的分类。  
  
   每个分类步骤都会重写前面的步骤。 .json 文件不需要列出所有键值对 **，MyCode、****库**和**不相关的**值可以是空数组。  
  
   “我的代码”.json 文件使用以下语法：  
  
```json  
{  
    "Eval" : "Classification",  
    "Function" : "Classification",  
    "ScriptBlock" : "Classification",  
    "MyCode" : [  
        "UrlOrFileSpec”,  
        . . .  
        "UrlOrFileSpec”  
    ],  
    "Libraries" : [  
        "UrlOrFileSpec”,  
        . .  
        "UrlOrFileSpec”  
    ],  
    "Unrelated" : [  
        "UrlOrFileSpec”,  
        . . .  
        "UrlOrFileSpec”  
    ]  
}  
  
```  
  
 **Eval、Function 和 ScriptBlock**  
  
 **Eval、****函数**和**脚本块**键值对确定动态生成的代码的分类方式。  
  
|||  
|-|-|  
|**Eval**|通过将字符串传递给主机提供的 `eval` 函数来执行的脚本。 默认情况下，Eval 脚本分类为“MyCode”****。|  
|**函数**|通过将字符串传递给 `Function` 构造函数来执行的脚本。 默认情况下，Function 脚本分类为“LibraryCode”****。|  
|**脚本块**|通过将字符串传递给 `setTimeout`、`setImmediate` 或 `setInterval` 函数来执行的脚本。 默认情况下，ScriptBlock 脚本分类为“UnrelatedCode”****。|  
  
 可以将值更改为以下关键字之一：  
  
- `MyCode` 将脚本分类为“MyCode”****。  
  
- `Library` 将脚本分类为“LibraryCode”****。  
  
- `Unrelated` 将脚本分类为“UnrelatedCode”****。  
  
  **MyCode、Libraries 和 Unrelated**  
  
  **MyCode、****库**和**不相关的**键值对指定要包含在分类中的 URL 或文件：  
  
|||  
|-|-|  
|**MyCode**|分类为**MyCode**的 URL 或文件数组。|  
|**库**|分类为**库代码**的 URL 或文件数组。|  
|**Unrelated**|分类为**不相关代码的**URL 或文件数组。|  
  
 url 或文件字符串可以包含一个或多个 `*` 字符，这些字符匹配零个或多个字符。 `*` 是正则表达式 `.*` 的等效项。
