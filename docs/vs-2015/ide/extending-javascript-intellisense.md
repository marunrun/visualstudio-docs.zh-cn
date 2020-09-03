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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bf16b6fdc307e11875f30cfad6e4bb35580b0b04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665756"
---
# <a name="extending-javascript-intellisense"></a>扩展 JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript IntelliSense 扩展性功能使你能够在 JavaScript 编辑器中为第三方库自定义 IntelliSense 结果。 这可以提高使用这些库的开发人员的体验。

 JavaScript 语言服务为添加到项目中的第三方 JavaScript 库提供 IntelliSense 功能。 对于大多数库，语句完成由语言服务自动提供。 下图显示了语句完成的示例：

 ![语句结束示例](../ide/media/js-intellisense-completion.png "js_intellisense_completion")

 如果你的库在标准 JavaScript 注释标记 (//) 中包含变量、函数和对象的说明，则默认情况下，你会自动从 IntelliSense 扩展性功能中受益，这些功能在显示在完成列表中的元素右侧的弹出框中提供描述性信息，或在函数调用中键入左括号。 弹出框中的注释包含成员的说明。 下面的示例演示完成列表的弹出框。

 !["快速信息" 弹出窗口&#45;的示例](../ide/media/js-intellisense-quickinfo.png "js_intellisense_quickinfo")

 为了进一步提高开发人员体验，您可能需要在弹出框中向开发人员提供类型信息。 您可以使用 JavaScript [XML 文档注释](../ide/xml-documentation-comments-javascript.md) 而不是标准注释标记来提供类型信息。 使用三斜杠注释标记添加 XML 文档注释 (///) 和一组已定义的 XML 元素。

 或者，可以使用 JavaScript IntelliSense 扩展性提供类型信息。 此功能使你能够通过创建 JavaScript 扩展并将其添加到脚本上下文来自定义 IntelliSense 结果。 在扩展（即 JavaScript 文件）中，你可以订阅由语言服务的对象公开的事件 `intellisense` 。 如果库中的行为模式阻止 JavaScript 语言服务提供所需的 IntelliSense 支持级别，并且还需要声明性 XML 文档注释的替代方法，JavaScript IntelliSense 扩展性是库的首选解决方案。 通过自定义 IntelliSense 结果，你可以创建一流的 IntelliSense 体验，而不考虑可能限制语言服务默认功能的任何行为模式。 有关详细信息，请参阅[标识符的语句完成](../ide/statement-completion-for-identifiers.md)。

## <a name="adding-an-extension-to-the-script-context"></a>向脚本上下文添加扩展
 对于要执行的 IntelliSense 扩展，需要将其添加到当前脚本上下文。 可以通过自动发现机制自动将扩展添加到脚本上下文，也可以通过使用引用组或引用指令，手动将扩展添加到脚本上下文。

 自动发现机制使语言服务能够自动查找遵循文件命名约定 *libraryname*.intellisense.js 的扩展，并与扩展所应用到的库位于同一个目录中。 例如，jQuery 库的有效扩展名将 jQuery.intellisense.js。 对于限制性更强的 jQuery extensions，你可以使用文件名称（如 jQuery-1.7.1.intellisense.js (特定于版本的扩展) 或 jQuery.ui.intellisense.js (范围的 jQuery library) 的扩展。 如果找到一个给定库的多个扩展，则使用该扩展的最严格的版本。

 如果要对所有 JavaScript 项目文件使用扩展，则可以改为选择将扩展添加到引用组。 有多种类型的引用组，其中包括隐式引用和包含专用辅助角色引用的引用组。 若要添加扩展，通常需要将文件添加为隐式引用组，隐式 ** (Windows) **， **隐式 (Web) **。 在代码编辑器中打开的每个 .js 文件的范围内，隐式引用都在范围内。 使用此方法时，需要添加扩展和扩展所补充的文件。

 使用 "**选项**" 对话框的 " **IntelliSense** " 页可将扩展添加为引用组。 可以通过选择菜单栏上的 "**工具**"、"**选项**"，然后选择 "**文本编辑器**"、" **JavaScript**"、" **IntelliSense**"、"**引用**" 来访问 " **IntelliSense** " 页。 有关引用组的详细信息，请参阅 [JavaScript IntelliSense](../ide/javascript-intellisense.md) 和 [选项、文本编辑器、JavaScript、IntelliSense](../ide/reference/options-text-editor-javascript-intellisense.md)。

 如果要将扩展用于特定的一组文件，请使用 reference 指令。 使用此方法时，需要同时引用扩展和扩展所补充的文件。 有关使用 reference 指令的信息，请参阅 [JavaScript IntelliSense](../ide/javascript-intellisense.md)。

## <a name="handling-intellisense-events"></a>处理 IntelliSense 事件
 利用该扩展性功能，您可以通过订阅事件（例如 language service 对象的事件）来自定义 IntelliSense 结果 `statementcompletion` `intellisense` 。 下面的示例演示了一个简单的扩展，它由语言服务用于隐藏从语句完成中以下划线开头的成员。 此代码包含在 underscorefilter.js 中，位于 \\ \\ *Visual Studio 安装路径*\JavaScript\References 文件夹中。

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

 在前面的代码中，扩展检查事件对象的 [TargetName 属性](#TargetName) 和 [target 属性](#Target) 属性 `statementcompletion` 以排除对象（如 `this` 和）， `window` 并确保可以标识有效的语句完成列表。 如果可以确定完成列表，扩展将通过筛选以下划线开头的成员来更新语句完成 [项属性](#Items) 集合。

 有关其他示例，请查看 \\ \\ *Visual Studio 安装路径*\JavaScript\References 文件夹。 此文件夹中的 showPlainComments.js 文件提供了使用其他事件为标准 JavaScript 注释标记 (//) 提供默认 IntelliSense 支持的示例。 与 underscorefilter.js 一样，showPlainComments.js 已作为工作扩展提供，当在代码中为变量、函数和对象使用注释标记时，可以看到生成的 IntelliSense 信息。 有关其他示例，请参阅 [代码示例](#CodeExamples)。

> [!WARNING]
> 如果修改 Visual Studio 随附的扩展文件，则可以禁用 JavaScript IntelliSense 或扩展所支持的功能。

 在扩展代码中，可以通过使用为以下事件类型创建处理程序 `addEventListener` ：

- `statementcompletion`，它为语句完成事件添加处理程序。 语句完成功能提供特定类型的成员列表，该列表在您键入特殊字符（例如句点 )  (）后出现，或在您键入或按下 CTRL + J 时显示的标识符列表。处理程序接收类型的事件对象 `CompletionEvent` ，该对象支持以下成员： [items 属性](#Items)、 [Target 属性](#Target)、 [targetName 属性](#TargetName)和 [作用域属性](#Scope)。

- `signaturehelp`，它为 IntelliSense 参数信息添加处理程序。 参数信息提供有关函数所需的参数数目、名称和参数类型的信息。 处理程序接收类型的事件对象 `SignatureHelpEvent` ，该对象支持以下成员： [target 属性](#Target)、 [ParentObject 属性](#ParentObject)、 [functionComments 属性](#FunctionComments)、 [functionHelp 属性](#FunctionHelp)。

- `statementcompletionhint`，它可为 IntelliSense 快速信息添加处理程序。 "快速信息" 弹出框显示代码中的标识符的完整声明。 处理程序接收类型的事件对象 `CompletionHintEvent` ，该对象支持以下成员： [completionItem 属性](#CompletionItem)和 [symbolHelp 属性](#SymbolHelp)。

  有关显示 IntelliSense 功能（如语句完成、参数信息和快速信息）的示例，请参阅 [使用 intellisense](../ide/using-intellisense.md)。

> [!NOTE]
> 在 JavaScript 中，"快速信息" 是指显示在完成列表右侧的弹出框。 不能手动调用 "快速信息"。

## <a name="intellisense-object"></a><a name="intellisenseObject"></a> intellisense 对象
 下表显示了可用于对象的函数 `intellisense` 。 `intellisense`对象仅在设计时可用。

|函数|说明|
|--------------|-----------------|
|`addEventListener(type, handler);`|添加 IntelliSense 事件的事件处理程序。<br /><br /> `type` 是一个字符串值。 有效值包括 `statementcompletion`、`signaturehelp` 和 `statementcompletionhint`。<br /><br /> `handler` 是一个事件处理程序函数，该函数接收以下类型之一的事件对象：<br /><br /> -   `CompletionEvent`，用于 `statementcompletion` 事件。<br />-   `SignatureHelpEvent`，用于 `signaturehelp` 事件。<br />-   `CompletionHintEvent`，用于 `statementcompletionhint` 事件。<br /><br /> 有关使用此函数的示例，请参阅 [代码示例](#CodeExamples)。|
|`annotate(obj, doc);`|通过将文档注释从一个对象复制到另一个对象来指定对象的文档。<br /><br /> `obj` 指定要向其复制文档的对象。<br /><br /> `doc` 指定要从中复制文档的对象。<br /><br /> 有关演示如何使用此函数的示例，请参阅 [添加 IntelliSense 批注](#Annotations)。|
|`getFunctionComments(func);`|返回指定函数的注释。<br /><br /> `func` 指定为其返回注释的函数。<br /><br /> 可以 `func` 使用设置参数 `completionItem.value` 。<br /><br /> 返回的 `functionComments` 对象包含以下成员： `above` 、 `inside` 和 `paramComment` 。 有关详细信息，请参阅 [FunctionComments 属性](#FunctionComments) 。<br /><br /> `getFunctionComments` 只能从注册的某个事件处理程序中调用 `addEventListener` 。<br /><br /> 有关演示如何使用此函数的示例，请参阅 \\ \\ *Visual Studio 安装路径*\JavaScript\References\showPlainComments.js。|
|`logMessage(msg);`|将诊断消息发送到 "输出" 窗口。<br /><br /> `msg` 包含消息的字符串。<br /><br /> 有关演示如何使用此函数的示例，请参阅将 [消息发送到输出窗口](#Logging)。|
|`nullWithCompletionsOf(value);`|返回一个特殊的 null 值，完成列表由参数中传递的对象确定 `value` 。<br /><br /> `value` 确定返回值的完成列表。 `value` 可以是任何类型。<br /><br /> 在设计时将 null 返回值视为 null，但返回值的完成列表与参数的完成列表相同 `value` 。<br /><br /> 此函数的一个用途是，当返回类型在运行时是可预测的，但返回值在设计时，为返回值提供 IntelliSense `null` 。|
|`redirectDefinition(func, definition);`|当请求参数 "帮助" 或 " **转到定义** " 时，指示 IntelliSense 使用提供的定义函数而不是原始 func 函数。<br /><br /> `func` 指定目标函数。<br /><br /> `definition` 指定要使用的函数，而不是参数信息的目标函数以及 " **转到定义**"。|
|`setCallContext(func, thisArg);`|为指定的函数设置调用上下文或范围。<br /><br /> `func` 指定要为其设置作用域的函数。<br /><br /> `thisArg``this`关键字可引用的对象文本，它指定成员的新范围。 可以包含要传入此参数的参数，例如 `intellisense.setCallContext(func, { thisArg: "", args: [23,2] });`<br /><br /> `setCallContext` 提供类似于的行为 `Function.prototype.bind` ，只不过它仅用于设计时 IntelliSense 支持。 `setCallContext`如果需要模拟对不能访问的代码的调用，则可以使用设置函数作用域，以便在调用函数时，函数调用将包含正确的作用域和参数。|
|`undefinedWithCompletionsOf(value);`|返回一个特殊的未定义值，完成列表由参数中传递的对象确定 `value` 。<br /><br /> `value` 确定返回值的完成列表。 `value` 可以是任何类型。<br /><br /> 在设计时将未定义的返回值视为未定义，但返回值的完成列表与参数的完成列表相同 `value` 。<br /><br /> 此函数的一个用途是在运行时可预测返回类型时为返回值提供 IntelliSense，但在设计时不定义返回值。|
|`version()`|返回 Visual Studio 版本。|

## <a name="event-members"></a>事件成员
 以下各节描述了在事件对象中为以下事件公开的成员： `statementcompletion` 、 `signaturehelp` 和 `statementcompletionhint` 。

### <a name="completionitem-property"></a><a name="CompletionItem"></a> completionItem 属性
 返回为其请求 "快速信息" 弹出框的标识符（称为 "完成项"）。 此属性可用于事件 `statementcompletionhint` 对象和事件对象的 [items 属性](#Items) 属性 `statementcompletion` 。

 返回值： `completionItem` 对象

 以下是对象的成员 `completionItem` ：

- `name`. 读/写，在集合中使用时 `items` ; 否则为只读。 返回标识完成项的字符串。

- `kind`. 读/写，在集合中使用时 `items` ; 否则为只读。 返回一个字符串，该字符串表示完成项的类型。 可能的值为方法、字段、属性、参数、变量和保留值。

- `glyph`. 读/写，在集合中使用时 `items` ; 否则为只读。 返回一个字符串，该字符串表示在完成列表中显示的图标。 的可能值 `glyph` 使用以下格式： vs：*glyphType*，其中 *glyphType* 对应于枚举中与语言无关的成员 <xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup> 。 例如， `vs:GlyphGroupMethod` 是的一个可能的值 `glyph` 。 如果 `glyph` 未设置，属性将 `kind` 确定默认图标。

- `parentObject`. 只读。 返回父对象。

- `value`. 只读。 返回一个对象，该对象表示完成项的值。

- `comments`. 只读。 返回一个字符串，该字符串包含字段或变量上方的注释。

- `scope`. 只读。 返回完成项的作用域。 可能的值为 global、local、parameter 和 member。

### <a name="items-property"></a><a name="Items"></a> items 属性
 获取或设置语句完成项的数组。 数组中的每个元素都是一个 [CompletionItem 属性](#CompletionItem) 对象。 `items`属性可用于 `statementcompletion` 事件对象。

 返回值：数组

### <a name="functioncomments-property"></a><a name="FunctionComments"></a> functionComments 属性
 返回函数的注释。 此属性可用于 `signaturehelp` 事件对象。

 返回值： `comments` 对象

 以下是对象的成员 `comments` ：

- `above`. 返回函数上方的注释。

- `inside`. 返回函数内的注释，通常为 VSDoc 格式。

- `paramComments`. 返回一个数组，该数组表示函数中每个参数的注释。 数组的成员包括：

  - `name`. 返回表示参数名称的字符串。

  - `comment`. 返回一个包含参数注释的字符串。

### <a name="functionhelp-property"></a><a name="FunctionHelp"></a> functionHelp 属性
 返回该函数的帮助。 此属性可用于 `signaturehelp` 事件对象。

 返回值： `functionHelp` 对象

 以下是对象的成员 `functionHelp` ：

- `functionName`. 读/写。 返回一个包含函数名称的字符串。

- `signatures`. 读/写。 获取或设置函数签名的数组。 数组中的每个元素都是一个 `signature` 对象。 某些 `signature` 属性（如 `locid` ）对应于常见的 [XML 文档注释](../ide/xml-documentation-comments-javascript.md) 特性。

  对象的成员 `signature` 包括：

  - `description`. 读/写。 返回描述函数的字符串。

  - `locid`. 读/写。 返回一个字符串标识符，其中包含有关函数的本地化信息。

  - `helpKeyword`. 读/写。 返回一个字符串，其中包含 Help 关键字。

  - `externalFile`. 读/写。 返回一个字符串，该字符串表示包含成员 ID 的文件。

  - `externalid`. 读/写。 返回一个字符串，该字符串表示函数的成员 ID。

  - `params`. 读/写。 获取或设置函数的参数数组。 参数数组中的每个元素都是一个 `parameter` 对象，该对象的属性与元素的以下特性相对应 [\<param>](../ide/param-javascript.md) ：

    - `name`. 读/写。 返回表示参数名称的字符串。

    - `type`. 读/写。 返回一个字符串，该字符串表示参数类型。

    - `elementType`. 读/写。 如果类型为 `Array` ，则返回一个字符串，该字符串表示数组中元素的类型。

    - `description`. 读/写。 返回一个描述参数的字符串。

    - `locid`. 读/写。 返回一个字符串标识符，其中包含有关函数的本地化信息。

    - `optional`. 读/写。 返回一个字符串，该字符串指示参数是否为可选的。 `true` 指示参数是可选的; `false` 指示它不是。

  - `returnValue`. 读/写。 获取或设置一个返回值对象，其属性与元素的以下特性相对应 [\<returns>](../ide/returns-javascript.md) ：

    - `type`. 读/写。 返回表示返回类型的字符串。

    - `elementType`. 读/写。 如果类型为 `Array` ，则返回一个字符串，该字符串表示数组中元素的类型。

    - `description`. 读/写。 返回描述返回值的字符串。

    - `locid`. 读/写。 返回一个字符串标识符，其中包含有关函数的本地化信息。

    - `helpKeyword`. 读/写。 返回一个字符串，其中包含 Help 关键字。

    - `externalFile`. 读/写。 返回一个字符串，该字符串表示包含成员 ID 的文件。

    - `externalid`. 读/写。 返回一个字符串，该字符串表示函数的成员 ID。

### <a name="parentobject-property"></a><a name="ParentObject"></a> parentObject 属性
 返回成员函数的父对象。 例如，对于 `document.getElementByID` ， `parentObject` 返回 `document` 对象。 此属性可用于 `signaturehelp` 事件对象。

 返回值：对象

### <a name="target-property"></a><a name="Target"></a> 目标属性
 返回一个对象，该对象表示触发器字符左侧的项，这是一个句点 (。 ) 。 对于函数， `target` 返回为其请求参数信息的函数。 此属性可用于 `statementcompletion` 和 `signaturehelp` 事件对象。

 返回值：对象

### <a name="targetname-property"></a><a name="TargetName"></a> targetName 属性
 返回表示目标的字符串。 例如，对于 "this."， `targetName` 返回 "this"。 对于 "A B" (当光标位于 "B" ) 后， `targetName` 返回 "b"。 此属性可用于 `statementcompletion` 事件对象。

 返回值： string

### <a name="symbolhelp-property"></a><a name="SymbolHelp"></a> symbolHelp 属性
 返回为其请求快速信息弹出框的完成项。 此属性可用于 `statementcompletionhint` 事件对象。

 返回值： `symbolHelp` 对象。

 对象的某些属性（ `symbolHelp` 如 `locid` ）对应于常见的 [XML 文档注释](../ide/xml-documentation-comments-javascript.md) 特性。

 以下是对象的成员 `symbolHelp` ：

- `name`. 读/写。 返回一个字符串，其中包含标识符名称。

- `symbolType`. 读/写。 返回一个字符串，该字符串表示符号类型。 可能的值包括 Unknown、Boolean、Number、String、Object、Function、Array、Date 和 Regex。

- `symbolDisplayType`. 读/写。 返回一个字符串，该字符串包含要显示的类型名称。 如果 `symbolDisplayType` 未设置， `symbolType` 则使用。

- `elementType`. 读/写。 如果 `symbolType` 为 `Array` ，则返回一个字符串，该字符串表示数组中元素的类型。

- `scope`. 读/写。 返回表示符号范围的字符串。 可能的值包括全局、本地、参数和成员。

- `description`. 读/写。 返回一个字符串，该字符串包含符号说明。

- `locid`. 读/写。 返回一个字符串标识符，其中包含有关符号的本地化信息。

- `helpKeyword`. 读/写。 返回一个字符串，其中包含 Help 关键字。

- `externalFile`. 读/写。 返回一个字符串，该字符串表示包含成员 ID 的文件。

- `externalid`. 读/写。 返回一个字符串，该字符串表示符号的成员 ID。

- `functionHelp`. 读/写。 返回一个 [FunctionHelp 属性](#FunctionHelp)，该属性在 is 函数时可能包含信息 `symbolType` 。

### <a name="scope-property"></a><a name="Scope"></a> 作用域属性
 返回事件的完成范围。 完成范围的可能值是全局和成员。 此属性可用于 `statementcompletion` 事件对象。

 返回值： string

## <a name="debugging-intellisense-extensions"></a>调试 IntelliSense 扩展
 无法调试扩展，但是可以使用 [Intellisense 对象](#intellisenseObject) 函数将信息发送到 Visual Studio "输出" 窗口。 有关演示如何使用此函数的示例，请参阅本主题后面的将 [消息发送到输出窗口](#Logging) 。 `logMessage`若要运行，必须在一个扩展中注册至少一个事件处理程序。

## <a name="code-examples"></a><a name="CodeExamples"></a> 代码示例
 本部分包含的代码示例演示如何使用 IntelliSense 扩展性 Api。 还有其他方法可以使用这些 Api。 有关其他示例，请参阅 \\ \\ *Visual Studio 安装路径*\JavaScript\References 文件夹中的以下文件。 这些是 JavaScript 语言服务使用的示例。

- underscoreFilter.js。 此代码将隐藏 IntelliSense 中的私有成员。 它包含事件的事件处理程序 `statementcompletion` 。

- showPlainComments.js。 此代码为标准注释提供 IntelliSense 支持。 它包括和事件的事件处理程序 `signaturehelp` `statementcompletionhint` 。

### <a name="adding-intellisense-annotations"></a><a name="Annotations"></a> 添加 IntelliSense 批注
 下面的过程演示如何在不直接修改库的情况下为第三方库提供 IntelliSense 文档支持。 为此，可以 `intellisense.annotate` 在扩展中使用。

 为使此示例正常工作，您需要项目中有以下 JavaScript 文件: 

- demoLib.js，它是一个表示第三方库的项目文件。

- demoLib.intellisense.js，它是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。

- appCode.js，是表示应用程序代码的项目文件。

##### <a name="to-add-an-intellisense-annotation"></a>添加 IntelliSense 批注

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

4. 在 appCode.js，键入以下代码。 你将在扩展中看到 XML 文档注释作为 IntelliSense 参数信息显示。

     ![显示 intellisense.annotate 使用情况的示例](../ide/media/js-intellisense-annotate-paraminfo.png "js_intellisense_annotate_paraminfo")

5. 在 appCode.js，键入以下代码。 键入时，会在扩展中看到标准注释，其中显示为 IntelliSense Quick Info。

     ![显示 intellisense.annotate 使用情况的示例](../ide/media/js-intellisense-annotations.png "js_intellisense_annotations")

### <a name="sending-messages-to-the-output-window"></a><a name="Logging"></a> 将消息发送到输出窗口
 下面的过程演示如何将消息发送到 "输出" 窗口。 可以发送消息来帮助调试 IntelliSense 扩展。

 为使此示例正常工作，您需要项目中有以下 JavaScript 文件: 

- exampleLib.js，它是一个表示第三方库的项目文件。

- exampleLib.intellisense.js，它是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。

- appCode.js，是表示应用程序代码的项目文件。

##### <a name="to-send-a-message-to-the-output-window"></a>向 "输出" 窗口发送消息

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

4. 在 "输出" 窗口中，选择 "**显示输出来源**" 列表中的**JavaScript Language Service** 。  (若要查看 "输出" 窗口，请从 "视图" 菜单中选择 " **输出** "。 ) 

5. 在 appCode.js，键入以下代码。 键入时，"输出" 窗口将显示语言服务中的消息。 "输出" 窗口中的第一条消息指示已请求当前范围的语句完成。

    ```javascript
    some
    ```

     下面是你应看到的输出的分部视图。

    ```scr
    03:16:14.3113: statement completion for current scope requested
    03:16:14.3113: [completion item] break, kind:reserved, scope:undefined, value:undefined
    03:16:14.3113: [completion item] case, kind:reserved, scope:undefined, value:undefined
    03:16:14.3113: [completion item] catch, kind:reserved, scope:undefined, value:undefined

    …
    ```

6. 选择 "输出" 窗口中的 " **全部清除** " 按钮。

7. 键入以下代码。 "输出" 窗口中的第一条消息指示已请求成员列表。

    ```javascript
    someVar.
    ```

     下面是你应看到的输出的分部视图：

    ```scr
    03:17:43.4032: member list requested, target: someVar
    03:17:43.4032: [completion item] a, kind:field, scope:member, value:1
    03:17:43.4032: [completion item] b, kind:field, scope:member, value:hello
    03:17:43.4032: [completion item] constructor, kind:method, scope:member, value:

    …
    ```

### <a name="changing-the-intellisense-icons"></a><a name="Icons"></a> 更改 IntelliSense 图标
 下面的过程演示如何在默认情况下更改 IntelliSense 显示的图标。 当您提供有关特定于库的概念（如命名空间、类、接口和枚举）的 IntelliSense 信息时，这可能很有用。

 有关可用图标值，请参阅 <xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup> 。

 为使此示例正常工作，您需要项目中有以下 JavaScript 文件: 

- exampleLib.js，它是 represens 第三方库的项目文件。

- exampleLib.intellisense.js，它是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。

- appCode.js，是表示应用程序代码的项目文件。

##### <a name="to-change-the-icons"></a>更改图标

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

4. 在 appCode.js，键入以下代码。 键入时，你会看到命名空间的图标已更改为 " {} "，因为在 c # 中使用了。

     ![显示标志符号属性使用情况的示例](../ide/media/js-intellisense-glyph-namespace.png "js_intellisense_glyph_namespace")

5. 在 appCode.js，键入以下代码。 键入时，你将看到 Enum1 成员的新枚举图标，以及 SomeClass1 成员的新类图标。

     ![显示标志符号属性使用情况的示例](../ide/media/js-intellisense-glyph-class-enum.png "js_intellisense_glyph_class_enum")

### <a name="avoiding-run-time-effects-on-intellisense-results"></a><a name="Overriding"></a> 避免在 IntelliSense 结果上运行时影响
 JavaScript 语言服务运行代码以动态提供 IntelliSense 信息。 因此，运行时行为有时会干扰所需的结果。 下面的过程演示如何在运行时行为导致不正确的 IntelliSense 时覆盖 IntelliSense 结果。

 为使此示例正常工作，您需要项目中有以下 JavaScript 文件: 

- exampleLib.js，它是一个表示第三方库的项目文件。

- exampleLib.intellisense.js，它是 IntelliSense 扩展。 此文件位于不需要包括在项目中，但它需要位于和 exampleLib.js 相同的文件夹。

- appCode.js，是表示应用程序代码的项目文件。

##### <a name="to-avoid-run-time-effects-on-intellisense-results"></a>避免对 IntelliSense 结果产生运行时影响

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

     在前面的代码中，已包装函数将基于的值忽略初始调用， `count` 并且不返回结果。

2. 将下列引用指令添加为 appCode.js 的第一行。 此处使用的路径指示 JavaScript 文件位于同一文件夹中。

    ```javascript
    /// <reference path="exampleLib.js" />

    ```

3. 在 appCode.js，键入以下代码。 标识符列表会出现，而不是 IntelliSense，因为永远不会调用包装函数，这意味着 `throttled` 函数不会返回任何结果。

     ![覆盖 intellisense 结果的示例](../ide/media/js-intellisense-override.png "js_intellisense_override")

4. 将以下代码添加到 exampleLib.intellisense.js。 这将更改设计时行为，以便按预期方式为包装函数显示 IntelliSense。

    ```javascript
    window.after = function (count, func) {
        // Just return func.
        return func;
    };
    ```

5. 在 appCode.js 中，键入之前键入的相同代码测试结果。 这次，IntelliSense 提供所需的信息。

     ![覆盖 IntelliSense 结果的示例](../ide/media/js-intellisense-override-fixed.png "js_intellisense_override_fixed")

## <a name="see-also"></a>另请参阅
 标识符的[JavaScript IntelliSense](../ide/javascript-intellisense.md) [语句完成](../ide/statement-completion-for-identifiers.md)
