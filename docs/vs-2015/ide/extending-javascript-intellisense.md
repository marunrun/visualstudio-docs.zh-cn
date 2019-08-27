---
title: 扩展 JavaScript IntelliSense |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- JavaScript, intellisense object
- extending JavaScript IntelliSense
- customizing JavaScript IntelliSense
- JavaScript, extending IntelliSense
- IntelliSense [JavaScript], extending
ms.assetid: 004e1ab6-bd7a-4327-9e01-89b9be96ba2f
caps.latest.revision: 43
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: eea71ffe2b449e0ee5aff893efd05e12e4ecae73
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824928"
---
# <a name="extending-javascript-intellisense"></a>扩展 JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript IntelliSense 扩展性功能，可自定义在第三方库的 JavaScript 编辑器中 IntelliSense 结果。 这可以提高使用这些库的开发人员的体验。  
  
 JavaScript 语言服务添加到项目的第三方 JavaScript 库提供 IntelliSense 功能。 对于大多数的库，语句完成自动由提供的语言服务。 下图显示语句完成的示例：  
  
 ![示例语句结束](../ide/media/js-intellisense-completion.png "js_intellisense_completion")  
  
 如果你的库包括变量、 函数和对象的说明可以在标准 JavaScript 注释标记 (/ /)，您会自动得到好处，默认情况下，从 IntelliSense 扩展性功能，提供一个弹出框中的描述性信息将出现在完成列表中，或在函数调用键入左括号时元素的右侧。 弹出框中的注释包含成员的说明。 下面的示例演示一个完成列表的弹出框。  
  
 ![示例中的快速信息弹出窗口的&#45;弹出框](../ide/media/js-intellisense-quickinfo.png "js_intellisense_quickinfo")  
  
 若要进一步提高开发人员体验，可能想要向开发人员在弹出框中提供类型信息。 可以通过使用 JavaScript 提供类型信息[XML 文档注释](../ide/xml-documentation-comments-javascript.md)而不是标准的注释标记。 使用三斜杠注释标记 （/ /） 和一组定义的 XML 元素添加 XML 文档注释。  
  
 或者，您可以通过使用 JavaScript IntelliSense 扩展性提供类型信息。 此功能，可通过创建 JavaScript 扩展并将其添加到脚本上下文自定义 IntelliSense 结果。 在扩展中，它是一个 JavaScript 文件，你订阅的事件公开的`intellisense`语言服务的对象。 JavaScript IntelliSense 扩展性是库的首选的解决方案，如果库中的行为模式，使 JavaScript 语言服务无法提供所需的级别的 IntelliSense 支持，并且如果声明性 XML 的替代方法文档注释，也需要。 通过自定义 IntelliSense 结果，可以创建一流的 IntelliSense 体验，而不考虑任何可能会限制语言服务的默认功能的行为模式。 有关详细信息，请参阅[标识符的语句完成](../ide/statement-completion-for-identifiers.md)。  
  
## <a name="adding-an-extension-to-the-script-context"></a>将扩展添加到脚本上下文  
 若要执行的 IntelliSense 扩展，它需要添加到当前脚本上下文。 扩展可以自动添加到脚本上下文的自动发现机制，或者你可以将扩展添加到脚本上下文手动使用引用组或引用指令。  
  
 自动发现机制，以自动查找遵循文件命名约定的扩展语言服务*libraryname*。 intellisense.js，和的中到库所在的目录的位置该应用扩展。 例如，jQuery 库的有效扩展名将 jQuery.intellisense.js。 对于限制性更强的 jQuery 扩展，可以使用文件的名称，例如 jQuery 1.7.1.intellisense.js （特定于版本的扩展） 或 jQuery.ui.intellisense.js （作用域内的 jQuery 库的扩展）。 如果给定库中找到多个扩展，则使用限制性最高版本的扩展。  
  
 如果你想要使用适用于所有 JavaScript 项目文件扩展，则可能会选择将扩展添加到引用组。 有几种类型的引用组，包含隐式引用的是那些和那些包含专用辅助角色的引用。 若要添加扩展，通常需要将文件添加为隐式引用组，或者**隐式 (Windows)** ，**隐式 (Web)** 。 在代码编辑器中打开每个.js 文件的作用域中是隐式引用。 当使用此方法时，您需要添加扩展插件和补充该扩展的文件。  
  
 使用**智能感知**页**选项**对话框可以将扩展添加为引用组。 您可以访问**智能感知**页上通过选择**工具**，**选项**菜单栏上，然后选择**文本编辑器**， **JavaScript**， **IntelliSense**，**引用**。 有关引用组的详细信息，请参阅[JavaScript IntelliSense](../ide/javascript-intellisense.md)并[选项，文本编辑器、 JavaScript、 IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md)。  
  
 如果你想要使用扩展名以特定的文件集，使用引用指令。 当使用此方法时，需要引用该扩展并补充了扩展的文件。 有关使用引用指令的信息，请参阅[JavaScript IntelliSense](../ide/javascript-intellisense.md)。  
  
## <a name="handling-intellisense-events"></a>处理 IntelliSense 事件  
 可扩展性功能，可通过订阅的事件，如自定义 IntelliSense 结果`statementcompletion`事件的语言服务`intellisense`对象。 下面的示例演示一个简单的扩展语言服务用于隐藏语句完成后以下划线开头的成员。 此代码包含在 underscorefilter.js 并且处于\\ \\ *Visual Studio 安装路径*\JavaScript\References 文件夹。  
  
```javascript  
intellisense.addEventListener('statementcompletion', function (event) {  
    if (event.targetName === "this") return;  
  
    var filterRegex;  
  
    if (event.target === undefined || event.target === window)  
        filterRegex = /^_.*\d{2,}/;  
    else  
        filterRegex = /^_.*/;  
  
    event.items = event.items.filter(function (item) {  
        return !filterRegex.test(item.name);  
    });  
});  
```  
  
 在前面的代码中，扩展将检查[targetName 属性](#TargetName)并[属性为目标](#Target)的属性`statementcompletion`事件对象，如排除对象`this`和`window`，并确保可以标识有效的语句完成列表。 如果无法确定完成列表，该扩展更新语句结束[项属性](#Items)通过筛选出以下划线开头的成员的集合。  
  
 对于其他示例，请查看\\ \\ *Visual Studio 安装路径*\JavaScript\References 文件夹。 此文件夹中的 showPlainComments.js 文件提供了示例的使用其他事件提供默认的 IntelliSense 支持的标准 JavaScript 注释标记 (/ /)。 如 underscorefilter.js，showPlainComments.js 已可用作工作扩展，并且注释标记在代码中使用的变量、 函数和对象时，可以看到生成的 IntelliSense 信息。 有关其他示例，请参阅[代码示例](#CodeExamples)。  
  
> [!WARNING]
> 如果您修改 Visual Studio 附带的扩展文件，可能会禁用 JavaScript IntelliSense 或扩展所支持的功能。  
  
 在扩展代码中，可以创建以下事件类型的处理程序，通过使用`addEventListener`:  
  
- `statementcompletion`这会增加语句完成事件的处理程序。 键入一个特殊字符，例如句点 （.） 后，将显示为特定类型的成员的列表或键入时或当您按 CTRL + j。 将显示标识符的列表，提供了语句完成该处理程序接收类型的事件对象`CompletionEvent`，它支持以下成员：[项属性](#Items)，[属性为目标](#Target)， [targetName 属性](#TargetName)，并[作用域属性](#Scope)。  
  
- `signaturehelp`其中添加处理程序的参数的 IntelliSense 信息。 参数信息提供了数、 名称和类型的函数所需参数的信息。 该处理程序接收类型的事件对象`SignatureHelpEvent`，它支持以下成员：[属性为目标](#Target)， [parentObject 属性](#ParentObject)， [functionComments 属性](#FunctionComments)， [functionHelp 属性](#FunctionHelp)。  
  
- `statementcompletionhint`其中添加处理程序的 IntelliSense 快速信息。 快速信息弹出框在代码中显示了标识符的完整声明。 该处理程序接收类型的事件对象`CompletionHintEvent`，它支持以下成员： [completionItem 属性](#CompletionItem)，和[symbolHelp 属性](#SymbolHelp)。  
  
  显示 IntelliSense 功能，如语句完成、 参数信息和快速信息的示例，请参阅[使用 IntelliSense](../ide/using-intellisense.md)。  
  
> [!NOTE]
> 在 JavaScript 中，快速信息是指将出现完成列表右侧的弹出框。 不能手动调用快速信息。  
  
## <a name="intellisenseObject"></a> intellisense 对象  
 下表显示了可用于函数`intellisense`对象。 `intellisense`对象是只能在设计时可用。  
  
|函数|描述|  
|--------------|-----------------|  
|`addEventListener(type, handler);`|添加 IntelliSense 事件的事件处理程序。<br /><br /> `type` 是一个字符串值。 有效值包括 `statementcompletion`、`signaturehelp` 和 `statementcompletionhint`。<br /><br /> `handler` 是接收到以下类型之一的事件对象的事件处理程序函数：<br /><br /> -   `CompletionEvent`用于`statementcompletion`事件。<br />-   `SignatureHelpEvent`用于`signaturehelp`事件。<br />-   `CompletionHintEvent`用于`statementcompletionhint`事件。<br /><br /> 有关使用此函数的示例，请参阅[代码示例](#CodeExamples)。|  
|`annotate(obj, doc);`|通过将文档注释从一个对象复制到另一个对象中指定的对象的文档。<br /><br /> `obj` 指定要将文档复制到的对象。<br /><br /> `doc` 指定要从其中复制文档的对象。<br /><br /> 有关演示如何使用此函数的示例，请参阅[添加 IntelliSense 批注](#Annotations)。|  
|`getFunctionComments(func);`|返回指定的函数的注释。<br /><br /> `func` 指定为其返回注释的函数。<br /><br /> 可以设置`func`参数使用`completionItem.value`。<br /><br /> 返回`functionComments`对象包含以下成员： `above`， `inside`，和`paramComment`。 有关详细信息，请参阅[functionComments 属性](#FunctionComments)属性。<br /><br /> `getFunctionComments` 可以仅从某个注册的事件处理程序内调用`addEventListener`。<br /><br /> 有关演示如何使用此函数的示例，请参阅\\ \\ *Visual Studio 安装路径*\JavaScript\References\showPlainComments.js。|  
|`logMessage(msg);`|将诊断消息发送到输出窗口。<br /><br /> `msg` 是一个字符串，包含的消息。<br /><br /> 有关演示如何使用此函数的示例，请参阅[将消息发送到输出窗口](#Logging)。|  
|`nullWithCompletionsOf(value);`|返回为其完成列表由传入的对象的特殊的 null 值`value`参数。<br /><br /> `value` 确定返回值的完成列表。 `value` 可以是任何类型。<br /><br /> Null 返回值被视为在设计时为 null，但返回的值的完成列表是相同的完成列表`value`参数。<br /><br /> 此函数的一个用途是返回类型是在运行时，可预测，但返回的值是用于保存返回值提供 IntelliSense`null`在设计时。|  
|`redirectDefinition(func, definition);`|指示智能感知时要使用提供的定义函数而不是原始的 func 函数参数帮助或**转到定义**请求。<br /><br /> `func` 指定的目标函数。<br /><br /> `definition` 指定要用于参数的信息的而不是目标函数的函数和**转到定义**。|  
|`setCallContext(func, thisArg);`|设置调用上下文或范围，对于指定的函数。<br /><br /> `func` 指定要为其设置的作用域的函数。<br /><br /> `thisArg` 是一个对象文字到`this`关键字可引用，它指定新的作用域的成员。 例如，则可以使用此参数中传递的参数 `intellisense.setCallContext(func, { thisArg: "", args: [23,2] });`<br /><br /> `setCallContext` 提供行为类似于`Function.prototype.bind`，只不过它仅用于设计时 IntelliSense 支持。 可以使用`setCallContext`若要设置函数范围，如果你需要模拟调用是不否则为可访问，以便当您调用该函数的代码，函数调用将包括的正确作用域和参数。|  
|`undefinedWithCompletionsOf(value);`|返回为其完成列表由传入的对象的特殊未定义的值`value`参数。<br /><br /> `value` 确定返回值的完成列表。 `value` 可以是任何类型。<br /><br /> 未定义返回值将被处理为未定义在设计时，但完成的返回值的列表是相同的完成列表`value`参数。<br /><br /> 此函数的一个用途是返回类型是在运行时，可预测，但在设计时返回的值未定义时，用于保存返回值提供 IntelliSense。|  
|`version()`|返回 Visual Studio 版本。|  
  
## <a name="event-members"></a>事件成员  
 以下部分介绍在以下事件的事件对象中公开的成员： `statementcompletion`， `signaturehelp`，和`statementcompletionhint`。  
  
### <a name="CompletionItem"></a> completionItem 属性  
 返回的标识符，称为完成项，为其请求快速信息弹出框。 此属性是可用于`statementcompletionhint`事件对象以及[项属性](#Items)属性的`statementcompletion`事件对象。  
  
 返回值：`completionItem`对象  
  
 以下是的成员`completionItem`对象：  
  
- `name`。 在中使用时读/写`items`集合; 否则为只读的。 返回一个字符串，标识完成项。  
  
- `kind`。 在中使用时读/写`items`集合; 否则为只读的。 返回一个字符串，表示完成项的类型。 可能的值为方法、 字段、 属性、 参数、 变量，并保留。  
  
- `glyph`。 在中使用时读/写`items`集合; 否则为只读的。 返回一个字符串，表示在完成列表中显示的图标。 可能的值`glyph`使用以下格式： vs:*glyphType*，其中*glyphType*对应于在独立于语言的成员<xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup>枚举。 例如，`vs:GlyphGroupMethod`是一个可能的值`glyph`。 当`glyph`未设置，则`kind`属性确定的默认图标。  
  
- `parentObject`。 只读。 返回父对象。  
  
- `value`。 只读。 返回一个对象，表示完成项的值。  
  
- `comments`。 只读。 返回一个字符串，包含超过了字段或变量的注释。  
  
- `scope`。 只读。 返回完成项的范围。 可能的值为全局、 本地、 参数和成员。  
  
### <a name="Items"></a> 项属性  
 获取或设置完成项的语句的数组。 数组中的每个元素均[completionItem 属性](#CompletionItem)对象。 `items`属性是可用于`statementcompletion`事件对象。  
  
 返回值： 数组  
  
### <a name="FunctionComments"></a> functionComments 属性  
 返回该函数的注释。 此属性是可用于`signaturehelp`事件对象。  
  
 返回值：`comments`对象  
  
 以下是的成员`comments`对象：  
  
- `above`。 返回的函数上方的注释。  
  
- `inside`。 VSDoc 格式通常返回在函数内的注释。  
  
- `paramComments`。 返回一个数组，表示函数中的每个参数的注释。 数组的成员包括：  
  
  - `name`。 返回一个表示参数名称的字符串。  

  - `comment`。 返回一个字符串，包含注释的参数。  
  
### <a name="FunctionHelp"></a> functionHelp 属性  
 返回有关函数的帮助。 此属性是可用于`signaturehelp`事件对象。  
  
 返回值：`functionHelp`对象  
  
 以下是的成员`functionHelp`对象：  
  
- `functionName`。 读/写。 返回包含函数名称的字符串。  
  
- `signatures`。 读/写。 获取或设置数组的函数签名。 数组中的每个元素均`signature`对象。 某些`signature`属性，如`locid`，对应于常见[XML 文档注释](../ide/xml-documentation-comments-javascript.md)属性。  
  
  成员`signature`对象包括：  

  - `description`。 读/写。 返回一个字符串，描述该函数。  

  - `locid`。 读/写。 返回包含有关该函数的本地化信息的字符串标识符。  

  - `helpKeyword`。 读/写。 返回一个字符串，包含帮助关键字。  

  - `externalFile`。 读/写。 返回一个字符串，表示文件，其中包含成员 id。  

  - `externalid`。 读/写。 返回一个字符串，表示该函数的成员 ID。  

  - `params`。 读/写。 获取或设置函数的参数数组。 参数数组中的每个元素均`parameter`具有对应的以下特性的属性的对象[ \<param >](../ide/param-javascript.md)元素：  

    - `name`。 读/写。 返回一个字符串，表示参数名称。  

    - `type`。 读/写。 返回一个字符串，表示参数类型。  

    - `elementType`。 读/写。 如果类型为`Array`，返回一个字符串，表示数组中元素的类型。  

    - `description`。 读/写。 返回一个字符串，描述的参数。  

    - `locid`。 读/写。 返回包含有关该函数的本地化信息的字符串标识符。  

    - `optional`。 读/写。 返回一个字符串，指示参数是否可选。 `true` 指示参数是可选的;`false`指示它不是。  

  - `returnValue`。 读/写。 获取或设置一个具有相对应的属性的返回值对象的以下特性[\<返回 >](../ide/returns-javascript.md)元素：  

    - `type`。 读/写。 返回一个字符串，表示返回类型。  

    - `elementType`。 读/写。 如果类型为`Array`，返回一个字符串，表示数组中元素的类型。  

    - `description`。 读/写。 返回一个字符串，描述返回值。  

    - `locid`。 读/写。 返回包含有关该函数的本地化信息的字符串标识符。  

    - `helpKeyword`。 读/写。 返回一个字符串，包含帮助关键字。  

    - `externalFile`。 读/写。 返回一个字符串，表示文件，其中包含成员 id。  

    - `externalid`。 读/写。 返回一个字符串，表示该函数的成员 ID。  
  
### <a name="ParentObject"></a> parentObject 属性  
 返回父对象的成员函数。 例如，对于`document.getElementByID`，`parentObject`返回`document`对象。 此属性是可用于`signaturehelp`事件对象。  
  
 返回值： 对象  
  
### <a name="Target"></a> 目标属性  
 返回一个对象，表示触发器字符，它是一个句点 （.） 左侧的项。 对于函数，`target`返回为其请求的参数信息的函数。 此属性是可用于`statementcompletion`和`signaturehelp`事件对象。  
  
 返回值： 对象  
  
### <a name="TargetName"></a> targetName 属性  
 返回一个字符串，表示目标。 例如，对于"this"，`targetName`返回"this"。 对于"A.B"（当光标位于"B"），`targetName`返回"B"。 此属性是可用于`statementcompletion`事件对象。  
  
 返回值： 字符串  
  
### <a name="SymbolHelp"></a> symbolHelp 属性  
 返回为其请求快速信息弹出框完成项。 此属性是可用于`statementcompletionhint`事件对象。  
  
 返回值：`symbolHelp`对象。  
  
 某些属性`symbolHelp`对象，例如`locid`，对应于常见[XML 文档注释](../ide/xml-documentation-comments-javascript.md)属性。  
  
 以下是的成员`symbolHelp`对象：  
  
- `name`。 读/写。 返回一个字符串，包含标识符名称。  
  
- `symbolType`。 读/写。 返回一个字符串，表示符号类型。 可能值包括未知、 布尔值、 数字、 字符串、 对象、 函数、 数组、 日期和正则表达式。  
  
- `symbolDisplayType`。 读/写。 返回一个字符串，包含要显示的类型名称。 如果`symbolDisplayType`未设置，`symbolType`使用。  
  
- `elementType`。 读/写。 如果`symbolType`是`Array`，返回一个字符串，表示数组中元素的类型。  
  
- `scope`。 读/写。 返回一个字符串，表示符号的作用域。 可能值包括全局、 本地、 参数和成员。  
  
- `description`。 读/写。 返回一个字符串，包含符号的说明。  
  
- `locid`。 读/写。 返回包含符号的本地化信息的字符串标识符。  
  
- `helpKeyword`。 读/写。 返回一个字符串，包含帮助关键字。  
  
- `externalFile`。 读/写。 返回一个字符串，表示文件，其中包含成员 id。  
  
- `externalid`。 读/写。 返回一个字符串，表示符号的成员 ID。  
  
- `functionHelp`。 读/写。 返回[functionHelp 属性](#FunctionHelp)，其中可能包含的信息时`symbolType`是函数。  
  
### <a name="Scope"></a> 作用域属性  
 返回该事件的完成作用域。 完成的可能值的范围是全局和成员。 此属性是可用于`statementcompletion`事件对象。  
  
 返回值： 字符串  
  
## <a name="debugging-intellisense-extensions"></a>调试 IntelliSense 扩展  
 不能调试扩展，但你可以使用[intellisense 对象](#intellisenseObject)函数将信息发送到 Visual Studio 输出窗口。 有关演示如何使用此函数的示例，请参阅[将消息发送到输出窗口](#Logging)本主题中更高版本。 有关`logMessage`要起作用，必须在至少一个事件处理程序注册的扩展中。  
  
## <a name="CodeExamples"></a> 代码示例  
 本节包含演示如何使用 IntelliSense 扩展性 Api 的代码示例。 还有其他方法来使用这些 Api。 有关其他示例，请参阅中的以下文件\\ \\ *Visual Studio 安装路径*\JavaScript\References 文件夹。 这些工作的 JavaScript 语言服务所使用的示例。  
  
- underscoreFilter.js。 此代码将隐藏从 IntelliSense 的私有成员。 它包括的事件处理程序`statementcompletion`事件。  
  
- showPlainComments.js。 此代码的标准注释提供 IntelliSense 支持。 它包括的事件处理程序`signaturehelp`和`statementcompletionhint`事件。  
  
### <a name="Annotations"></a> 添加 IntelliSense 批注  
 以下过程说明如何为第三方库提供 IntelliSense 文档支持，而无需直接修改库。 若要执行此操作，可以使用`intellisense.annotate`扩展中。  
  
 为使此示例正常工作，您需要项目中有以下 JavaScript 文件:  
  
- demoLib.js 是表示第三方库的项目文件。  
  
- demoLib.intellisense.js 是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。  
  
- appCode.js，是表示应用程序代码的项目文件。  
  
##### <a name="to-add-an-intellisense-annotation"></a>若要添加 IntelliSense 批注  
  
1. 将以下代码添加到 demoLib.js。  
  
    ```javascript  
    function someFunc(a) { };  
    var rectangle;  
  
    ```  
  
2. 将以下代码添加到 demoLib.intellisense.js。  
  
    ```javascript  
    intellisense.annotate(someFunc, function (a) {  
        /// <signature>  
        /// <summary>Description of someFunc</summary>  
        /// <param name="a">Param a</param>  
        /// </signature>  
    });  
  
    intellisense.annotate(window, {  
        // This is a comment on a global variable named rectangle.  
        rectangle: undefined  
    });  
    ```  
  
3. 将下列引用指令添加为 appCode.js 的第一行。 此处使用的路径指示 JavaScript 文件位于同一文件夹中。  
  
    ```javascript  
    /// <reference path="demoLib.js" />  
  
    ```  
  
4. 在 appCode.js，键入以下代码。 你将看到显示为 IntelliSense 参数信息的扩展中的 XML 文档注释。  
  
     ![显示 intellisense.annotate 使用情况的示例](../ide/media/js-intellisense-annotate-paraminfo.png "js_intellisense_annotate_paraminfo")  
  
5. 在 appCode.js，键入以下代码。 键入时，你将看到显示为 IntelliSense 快速信息的扩展中的标准注释。  
  
     ![显示 intellisense.annotate 使用情况的示例](../ide/media/js-intellisense-annotations.png "js_intellisense_annotations")  
  
### <a name="Logging"></a> 将消息发送到输出窗口  
 以下过程说明如何将消息发送到输出窗口。 您可以发送消息来帮助调试 IntelliSense 扩展。  
  
 为使此示例正常工作，您需要项目中有以下 JavaScript 文件:  
  
- exampleLib.js 是表示第三方库的项目文件。  
  
- exampleLib.intellisense.js 是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。  
  
- appCode.js，是表示应用程序代码的项目文件。  
  
##### <a name="to-send-a-message-to-the-output-window"></a>若要将消息发送到输出窗口  
  
1. 将以下代码添加到 exampleLib.js。  
  
    ```javascript  
    var someVar = {  
        a: 1,  
        b: 'hello'  
    };  
    ```  
  
2. 将以下代码添加到 exampleLib.intellisense.js。  
  
    ```javascript  
    intellisense.addEventListener('statementcompletion', function (e) {  
        // Prints out statement completion info: Either (1) the member   
        // list, if the trigger character was typed, or (2) the   
        // statement completion identifiers.  
        // e.target represents the object left of the trigger character.  
        intellisense.logMessage(  
            e.target ? 'member list requested, target: ' + e.targetName : 'statement completion for current scope requested');  
  
        // Prints out all statement completion items.  
        e.items.forEach(function (item) {  
            intellisense.logMessage('[completion item] ' + item.name + ', kind:' + item.kind + ', scope:' + item.scope + ', value:' + item.value);  
        });  
    });  
    ```  
  
3. 将下列引用指令添加为 appCode.js 的第一行。 此处使用的路径指示 JavaScript 文件位于同一文件夹中。  
  
    ```javascript  
    /// <reference path="exampleLib.js" />  
  
    ```  
  
4. 在输出窗口中，选择**JavaScript Language Service**中**显示输出来源**列表。 (若要查看输出窗口，请选择**输出**从视图菜单。)  
  
5. 在 appCode.js，键入以下代码。 键入时，输出窗口显示了来自语言服务的消息。 在输出窗口中的第一个消息指示已请求适用于当前作用域语句结束。  
  
    ```javascript  
    some  
    ```  
  
     下面是分部视图应看到的输出。  
  
    ```scr  
    03:16:14.3113: statement completion for current scope requested  
    03:16:14.3113: [completion item] break, kind:reserved, scope:undefined, value:undefined  
    03:16:14.3113: [completion item] case, kind:reserved, scope:undefined, value:undefined  
    03:16:14.3113: [completion item] catch, kind:reserved, scope:undefined, value:undefined  
  
    …  
    ```  
  
6. 选择**全部清除**输出窗口中的按钮。  
  
7. 键入以下代码。 在输出窗口中的第一个消息指示已请求成员列表。  
  
    ```javascript  
    someVar.  
    ```  
  
     下面是分部视图应看到的输出：  
  
    ```scr  
    03:17:43.4032: member list requested, target: someVar  
    03:17:43.4032: [completion item] a, kind:field, scope:member, value:1  
    03:17:43.4032: [completion item] b, kind:field, scope:member, value:hello  
    03:17:43.4032: [completion item] constructor, kind:method, scope:member, value:  
  
    …  
    ```  
  
### <a name="Icons"></a> 更改 IntelliSense 图标  
 以下过程说明如何更改默认情况下显示 intellisense 的图标。 提供有关特定于库的概念，如命名空间、 类、 接口和枚举的 IntelliSense 信息时，这可能很有用。  
  
 有关可用图标值，请参阅<xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup>。  
  
 为使此示例正常工作，您需要项目中有以下 JavaScript 文件:  
  
- exampleLib.js，这是一个项目文件的 represens 第三方库。  
  
- exampleLib.intellisense.js 是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。  
  
- appCode.js，是表示应用程序代码的项目文件。  
  
##### <a name="to-change-the-icons"></a>若要更改的图标  
  
1. 将以下代码添加到 exampleLib.js。  
  
    ```javascript  
    function Namespace(name) {  
        this._isNamespace = true;  
        window[name] = this;  
    };  
  
    function Enum(values) {  
        var e = Object.create(values);  
        e._isEnum = true;  
        return e;  
    };  
  
    var SomeNamespace = new Namespace('SomeNamespace');  
    // A constructor function is considered a class.  
    SomeNamespace.SomeClass1 = function () { }  
    SomeNamespace.Enum1 = new Enum({ VALUE1: 0, VALUE2: 1 });  
    ```  
  
2. 将以下代码添加到 exampleLib.intellisense.js。  
  
    ```javascript  
    intellisense.addEventListener('statementcompletion', function (e) {  
        e.items.forEach(function (item) {  
            // Detect a namespace by using the _isNamespace flag.  
            if (item.value && item.value._isNamespace) {  
                item.glyph = 'vs:GlyphGroupNamespace';  
                }  
  
            if (item.parentObject && item.parentObject._isNamespace) {  
                // The item is a member of a namespace.   
  
                // All constructor functions that are part of a namespace   
                // are considered classes.   
                // A constructor function starts with  
                // an uppercase letter by convention.    
                if (typeof item.value == 'function' && (item.name[0].toUpperCase()   
                    == item.name[0])) {  
                    item.glyph = 'vs:GlyphGroupClass';  
                }  
  
                // Detect an enumeration by using the _isEnum flag.  
                if (item.value && item.value._isEnum) {  
                    item.glyph = 'vs:GlyphGroupEnum';  
                }  
            }  
        });  
    });  
  
    intellisense.addEventListener('statementcompletionhint', function (e) {  
        if (e.completionItem.value) {  
            if (e.completionItem.value._isNamespace) {  
                e.symbolHelp.symbolDisplayType = 'Namespace';  
            }  
            if (e.completionItem.value._isEnum) {  
                e.symbolHelp.symbolDisplayType = 'Enum';  
            }  
        }  
    });  
    ```  
  
3. 将下列引用指令添加为 appCode.js 的第一行。 此处使用的路径指示 JavaScript 文件位于同一文件夹中。  
  
    ```javascript  
    /// <reference path="exampleLib.js" />  
  
    ```  
  
4. 在 appCode.js，键入以下代码。 键入时，您将看到的图标的命名空间已更改为"{}"，因为在 C# 中使用。  
  
     ![显示标志符号属性使用示例](../ide/media/js-intellisense-glyph-namespace.png "js_intellisense_glyph_namespace")  
  
5. 在 appCode.js，键入以下代码。 键入时，你将看到一个新的枚举图标 1> 成员和 SomeClass1 成员的新类图标。  
  
     ![显示标志符号属性使用情况的示例](../ide/media/js-intellisense-glyph-class-enum.png "js_intellisense_glyph_class_enum")  
  
### <a name="Overriding"></a> 避免对 IntelliSense 结果的运行时影响  
 JavaScript 语言服务在运行代码来动态提供 IntelliSense 信息。 因此，想要的结果可能偶尔会影响运行时行为。 以下过程演示如何重写 IntelliSense 结果时的运行时行为会导致不正确的 IntelliSense。  
  
 为使此示例正常工作，您需要项目中有以下 JavaScript 文件:  
  
- exampleLib.js 是表示第三方库的项目文件。  
  
- exampleLib.intellisense.js 是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。  
  
- appCode.js，是表示应用程序代码的项目文件。  
  
##### <a name="to-avoid-run-time-effects-on-intellisense-results"></a>若要避免运行时对 IntelliSense 结果的影响  
  
1. 将以下代码添加到 exampleLib.js。  
  
    ```javascript  
    function after(count, func) {  
        return function () {  
            if (--times < 1) {  
                return func.apply(this, arguments);  
            }  
        };  
    };  
    ```  
  
     在前面的代码中，已包装的函数将忽略值的基础的初始调用`count`，也不会返回结果。  
  
2. 将下列引用指令添加为 appCode.js 的第一行。 此处使用的路径指示 JavaScript 文件位于同一文件夹中。  
  
    ```javascript  
    /// <reference path="exampleLib.js" />  
  
    ```  
  
3. 在 appCode.js，键入以下代码。 因为已包装的函数永远不会调用时，这意味着，而不是 IntelliSense 显示标识符列表`throttled`函数没有返回任何结果。  
  
     ![覆盖 intellisense 结果的示例](../ide/media/js-intellisense-override.png "js_intellisense_override")  
  
4. 将以下代码添加到 exampleLib.intellisense.js。 这将更改设计时行为，以便智能感知显示对于包装函数，按预期方式。  
  
    ```javascript  
    window.after = function (count, func) {  
        // Just return func.   
        return func;  
    };  
    ```  
  
5. 在 appCode.js，键入以前类型化的同一代码测试的结果。 这一次，IntelliSense 提供了所需的信息。  
  
     ![覆盖 IntelliSense 结果的示例](../ide/media/js-intellisense-override-fixed.png "js_intellisense_override_fixed")  
  
## <a name="see-also"></a>请参阅  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)   
 [适用于标识符的语句结束](../ide/statement-completion-for-identifiers.md)
