---
title: C# 代码片段
ms.date: 06/05/2017
ms.topic: reference
helpviewer_keywords:
- snippets [C#]
- code snippets [C#]
- Code Snippet Inserter [C#]
- C#, code snippets
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d41907a15b7e0b1692dda3f4d678c2b843dfcd03
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594157"
---
# <a name="c-code-snippets"></a>C# 代码片段

代码片段是现成的代码段，可快速插入到代码中。 例如，`for` 代码片段刻创建一个空 `for` 循环。 有些代码片段为外侧代码片段，让你可以选择代码行，然后选择包含所选代码行的代码片段。 例如，选择代码行并激活 `for` 代码片段时，会通过循环块内的代码行创建 `for` 循环。 使用代码片段可以更快、更容易且更可靠地编写程序代码。

可以在光标位置插入代码片段，或者在当前所选代码旁插入外侧代码片段。 可通过以下方式调用代码片段插入器：单击“IntelliSense”菜单上的“插入代码段”或“外侧代码”，按 Ctrl+K、X，或者按 Ctrl+K、S。

代码片段插入器显示所有可用代码片段的代码片段名称  。 代码片段插入器还包括输入对话框，可在其中键入代码片段名称或部分代码片段。 代码片段插入器突出显示与代码片段名称最接近的匹配。 可随时按按 Tab 关闭代码片段插入器，并插入当前选定的代码片段  。 按 Esc 或在代码编辑器中单击鼠标会关闭代码片段插入器，而不插入代码片段  。

## <a name="default-code-snippets"></a>默认代码片段

Visual Studio for C# 默认包含以下代码片段。

|名称（或快捷方式）|说明|要插入代码片段的有效位置|
| - |-----------------| - |
|#if|创建 [#if](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if) 指令和 [#endif](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endif) 指令。|任何位置。|
|#region|创建 [#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) 指令和 [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion) 指令。|任何位置。|
|~|创建包含类的[终结期](/dotnet/csharp/programming-guide/classes-and-structs/destructors)（析构函数）。|在类中。|
|attribute|为派生自 <xref:System.Attribute> 的类创建声明。|在命名空间（包括全局命名空间）、类或结构中。|
|checked|创建 [checked](/dotnet/csharp/language-reference/keywords/checked) 块。|在方法、索引器、属性访问器或事件访问器内。|
|class|创建类声明。|在命名空间（包括全局命名空间）、类或结构中。|
|ctor|创建包含类的构造函数。|在类中。|
|cw|创建对 <xref:System.Console.WriteLine%2A> 的调用。|在方法、索引器、属性访问器或事件访问器内。|
|do|创建 [do](/dotnet/csharp/language-reference/keywords/do) `while` 循环。|在方法、索引器、属性访问器或事件访问器内。|
|else|创建 [else](/dotnet/csharp/language-reference/keywords/if-else) 块。|在方法、索引器、属性访问器或事件访问器内。|
|enum|创建[枚举](/dotnet/csharp/language-reference/keywords/enum)声明。|在命名空间（包括全局命名空间）、类或结构中。|
|等于|创建一个方法声明，该声明对 <xref:System.Object> 类中定义的 <xref:System.Object.Equals%2A> 方法进行重写。|在类或结构中。|
|exception|为某个从异常（默认情况下为 <xref:System.Exception>）派生的类创建声明。|在命名空间（包括全局命名空间）、类或结构中。|
|for|创建 [for](/dotnet/csharp/language-reference/keywords/for) 循环。|在方法、索引器、属性访问器或事件访问器内。|
|foreach|创建 [foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 循环。|在方法、索引器、属性访问器或事件访问器内。|
|forr|创建 [for](/dotnet/csharp/language-reference/keywords/for) 循环，每次迭代后会减少循环变量。|在方法、索引器、属性访问器或事件访问器内。|
|if|创建 [if](/dotnet/csharp/language-reference/keywords/if-else) 块。|在方法、索引器、属性访问器或事件访问器内。|
|indexer|创建索引器声明。|在类或结构中。|
|interface|创建[接口](/dotnet/csharp/language-reference/keywords/interface)声明。|在命名空间（包括全局命名空间）、类或结构中。|
|invoke|创建安全调用事件的块。|在方法、索引器、属性访问器或事件访问器内。|
|iterator|创建迭代器。|在类或结构中。|
|iterindex|使用嵌套类创建“已命名”迭代器和索引器对。|在类或结构中。|
|lock|创建 [lock](/dotnet/csharp/language-reference/keywords/lock-statement) 块。|在方法、索引器、属性访问器或事件访问器内。|
|mbox|创建对 <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> 的调用。 可能还需要添加对 System.Windows.Forms.dll 的引用  。|在方法、索引器、属性访问器或事件访问器内。|
|命名空间|创建[命名空间](/dotnet/csharp/language-reference/keywords/namespace)声明。|在命名空间（包括全局命名空间）中。|
|prop|创建[自动实现的属性](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)声明。|在类或结构中。|
|propfull|创建具有 `get` 和 `set` 访问器的属性声明。|在类或结构中。|
|propg|创建具有专用 `set` 访问器的只读[自动实现的属性](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)。|在类或结构中。|
|sim|创建 [static](/dotnet/csharp/language-reference/keywords/static) [int](/dotnet/csharp/language-reference/keywords/int) Main 方法声明。|在类或结构中。|
|struct|创建[结构](/dotnet/csharp/language-reference/keywords/struct)声明。|在命名空间（包括全局命名空间）、类或结构中。|
|svm|创建 [static](/dotnet/csharp/language-reference/keywords/static) [void](/dotnet/csharp/language-reference/keywords/void) Main 方法声明。|在类或结构中。|
|switch|创建 [switch](/dotnet/csharp/language-reference/keywords/switch) 块。|在方法、索引器、属性访问器或事件访问器内。|
|尝试|创建 [try-catch](/dotnet/csharp/language-reference/keywords/try-catch) 块。|在方法、索引器、属性访问器或事件访问器内。|
|tryf|创建 [try-finally](/dotnet/csharp/language-reference/keywords/try-finally) 块。|在方法、索引器、属性访问器或事件访问器内。|
|unchecked|创建 [unchecked](/dotnet/csharp/language-reference/keywords/unchecked) 块。|在方法、索引器、属性访问器或事件访问器内。|
|unsafe|创建 [unsafe](/dotnet/csharp/language-reference/keywords/unsafe) 块。|在方法、索引器、属性访问器或事件访问器内。|
|借助|创建 [using](/dotnet/csharp/language-reference/keywords/using-directive) 指令。|在命名空间（包括全局命名空间）中。|
|while|创建 [while](/dotnet/csharp/language-reference/keywords/while) 循环。|在方法、索引器、属性访问器或事件访问器内。|

## <a name="see-also"></a>另请参阅

- [代码片段函数](../ide/code-snippet-functions.md)
- [代码片段](../ide/code-snippets.md)
- [模板参数](../ide/template-parameters.md)
- [如何：使用外侧代码片段](../ide/how-to-use-surround-with-code-snippets.md)
