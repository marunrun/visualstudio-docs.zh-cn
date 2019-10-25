---
title: 旧版语言服务分析器和扫描程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11b172fee8f6f5cf1c80d306a8a8b154f7316bf8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726727"
---
# <a name="legacy-language-service-parser-and-scanner"></a>旧版语言服务分析器和扫描程序
分析器是语言服务的核心。 托管包框架（MPF）语言类需要语言分析器来选择要显示的代码的相关信息。 分析器将文本分为词法标记，然后按类型和功能标识这些标记。

## <a name="discussion"></a>讨论
 下面是一个C#方法。

```csharp
namespace MyNamespace
{
    class MyClass
    {
        public void MyFunction(int arg1)
        {
            int var1 = arg1;
        }
    }
}
```

 在此示例中，标记是单词和标点符号。 标记的种类如下所示。

|标记名称|标记类型|
|----------------|----------------|
|namespace、class、public、void、int|keyword|
|=|operator|
|{ } ( ) ;|后面|
|MyNamespace、MyClass、MyFunction、arg1、var1|标识符 (identifier)|
|MyNamespace|namespace|
|MyClass|class|
|MyFunction|方法|
|arg1|参数 (parameter)|
|var1|局部变量|

 分析器的作用是标识令牌。 某些标记可以有多种类型。 在分析器识别了标记后，语言服务可以使用这些信息来提供有用的功能，如语法突出显示、大括号匹配和 IntelliSense 操作。

## <a name="types-of-parsers"></a>分析器的类型
 语言服务分析器与作为编译器的一部分使用的分析器不同。 但是，这种分析器需要使用扫描器和分析器，其方式与编译器分析器的方式相同。

- 扫描器用于标识令牌的类型。 此信息用于语法突出显示和快速标识可触发其他操作（例如，大括号匹配）的标记类型。 此扫描程序由 <xref:Microsoft.VisualStudio.Package.IScanner> 接口表示。

- 分析器用于描述标记的功能和范围。 IntelliSense 操作中使用此信息来标识语言元素（例如方法、变量、参数和声明），并根据上下文提供成员和方法签名的列表。 此分析器还用于查找匹配的语言元素对，如大括号和圆括号。 此分析器通过 <xref:Microsoft.VisualStudio.Package.LanguageService> 类中的 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法进行访问。

  如何为语言服务实现扫描程序和分析器是由您来实现的。 提供了多个资源，这些资源说明分析器的工作方式以及如何编写您自己的分析器。 另外，还提供了几个免费和商业产品，有助于创建分析器。

### <a name="the-parsesource-parser"></a>ParseSource 分析器
 与用作编译器一部分的分析器（其中的标记转换为某种形式的可执行代码）不同，语言服务分析器可以出于多种不同的原因和在许多不同的上下文中调用。 在 <xref:Microsoft.VisualStudio.Package.LanguageService> 类的 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法中实现此方法的方式取决于你。 请记住，可以在后台线程上调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法。

> [!CAUTION]
> @No__t_0 结构包含对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象的引用。 此 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象不能在后台线程中使用。 事实上，许多基本 MPF 类不能在后台线程中使用。 其中包括 <xref:Microsoft.VisualStudio.Package.Source>、<xref:Microsoft.VisualStudio.Package.ViewFilter>、<xref:Microsoft.VisualStudio.Package.CodeWindowManager> 类以及直接或间接与视图通信的任何其他类。

 此分析器通常在第一次调用时或在给定 <xref:Microsoft.VisualStudio.Package.ParseReason> 的分析原因值时，分析整个源文件。 对 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法的后续调用将处理经过分析的代码的一小部分，并且可以通过使用上一次完全分析操作的结果更快速地执行。 @No__t_0 方法通过 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 和 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象传达分析操作的结果。 @No__t_0 对象用于收集特定分析原因的信息，例如，有关包含参数列表的匹配大括号或方法签名的范围的信息。 @No__t_0 提供声明和方法签名的集合，还支持 "中转到高级" 编辑选项（"**中转到定义**"、"**中转到声明**"、"**跳到引用**"）。

### <a name="the-iscanner-scanner"></a>IScanner 扫描仪
 还必须实现一个实现 <xref:Microsoft.VisualStudio.Package.IScanner> 的扫描程序。 但是，因为此扫描程序通过 <xref:Microsoft.VisualStudio.Package.Colorizer> 类逐行操作，所以通常更容易实现。 在每行的开头，MPF 为 <xref:Microsoft.VisualStudio.Package.Colorizer> 类提供一个值，用作传递给扫描程序的状态变量。 每行结束时，扫描程序返回更新的状态变量。 MPF 将缓存每行的此状态信息，以便扫描程序可以从任何行开始分析，而无需从源文件的开头开始进行分析。 此快速扫描一条线路允许编辑器向用户提供快速反馈。

## <a name="parsing-for-matching-braces"></a>分析匹配的大括号
 此示例演示了用于匹配用户已键入的右大括号的控制流。 在此过程中，用于着色的扫描程序还用于确定令牌类型，以及令牌是否可以触发匹配大括号操作。 如果找到了触发器，则调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法来查找匹配的大括号。 最后，突出显示两个大括号。

 即使在触发器的名称和分析原因中使用了大括号，此过程也不会限制为实际的大括号。 支持指定为匹配对的任何字符对。 示例包括（和）、\< 和 > 以及 [和]。

 假定语言服务支持匹配的大括号。

1. 用户键入右大括号（}）。

2. 将在光标所在的源文件中插入大括号，并将光标前进一。

3. @No__t_1 类中的 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> 方法将与键入的右大括号一起调用。

4. @No__t_0 方法调用 <xref:Microsoft.VisualStudio.Package.Source> 类中的 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> 方法，以获取紧靠当前游标位置之前位置的标记。 此标记对应于键入的右大括号。

    1. @No__t_0 方法对 <xref:Microsoft.VisualStudio.Package.Colorizer> 对象调用 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 方法以获取当前行上的所有标记。

    2. @No__t_0 方法通过当前行的文本调用 <xref:Microsoft.VisualStudio.Package.IScanner> 对象的 <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> 方法。

    3. @No__t_0 方法对 <xref:Microsoft.VisualStudio.Package.IScanner> 对象重复调用 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> 方法，以便从当前行收集所有标记。

    4. @No__t_0 方法调用 <xref:Microsoft.VisualStudio.Package.Source> 类中的私有方法，以获取包含所需位置的标记，并传入从 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 方法获取的标记的列表。

5. @No__t_0 方法在 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> 方法返回的令牌上查找 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 的令牌触发器标志;即表示右大括号的标记）。

6. 如果找到 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 的触发器标志，则将调用 <xref:Microsoft.VisualStudio.Package.Source> 类中的 <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> 方法。

7. @No__t_0 方法使用分析原因值 <xref:Microsoft.VisualStudio.Package.ParseReason> 启动分析操作。 此操作最终对 <xref:Microsoft.VisualStudio.Package.LanguageService> 类调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法。 如果启用了异步分析，则对 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法的调用将在后台线程上发生。

8. 完成分析操作后，将在 <xref:Microsoft.VisualStudio.Package.Source> 类中调用一个名为 `HandleMatchBracesResponse` 的内部完成处理程序（也称为回调方法）。 此调用由 <xref:Microsoft.VisualStudio.Package.LanguageService> 基类自动进行，而不是由分析器进行。

9. @No__t_0 方法从 <xref:Microsoft.VisualStudio.Package.ParseRequest> 对象中存储的 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 对象获取范围列表。 （Span 是 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> 结构，它指定源文件中的行和字符范围。）此范围列表通常包含两个范围，每个范围分别用于左大括号和右大括号。

10. @No__t_0 方法对存储在 <xref:Microsoft.VisualStudio.Package.ParseRequest> 对象中的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 对象调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> 方法。 这将突出显示给定范围。

11. 如果启用了 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 属性 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>，则 `HandleBracesResponse` 方法将获取匹配范围包含的文本，并在状态栏中显示该范围内的前80个字符。 如果 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法包含匹配对随附的 language 元素，则这种方法的效果最佳。 有关更多信息，请参见 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 属性。

12. 效率.

### <a name="summary"></a>总结
 匹配大括号操作通常仅限于简单的语言元素对。 更复杂的元素（如匹配三元组（"`if(...)`"、"`{`" 和 "`}`"、""、"`else`"、"`{`" 和 "`}`"）可在单词完成操作中突出显示。 例如，在 "else" 单词完成后，可以突出显示匹配的 "`if`" 语句。 如果有一系列 `if` / `else if` 语句，则可以使用与匹配大括号相同的机制突出显示它们。 @No__t_0 的基类已支持此操作，如下所示：扫描程序必须将标记触发器值 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 与光标位置之前的标记的触发器值 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 返回。

 有关详细信息，请参阅[旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)。

## <a name="parsing-for-colorization"></a>针对着色进行分析
 着色源代码非常简单，只需标识令牌类型并返回有关该类型的颜色信息。 @No__t_0 类充当编辑器和扫描器之间的中介，以提供有关每个标记的颜色信息。 @No__t_0 类使用 <xref:Microsoft.VisualStudio.Package.IScanner> 对象帮助着色一行，并同时收集源文件中所有行的状态信息。 在 MPF 语言服务类中，无需重写 <xref:Microsoft.VisualStudio.Package.Colorizer> 类，因为它仅通过 <xref:Microsoft.VisualStudio.Package.IScanner> 接口与扫描程序通信。 通过重写 <xref:Microsoft.VisualStudio.Package.LanguageService> 类的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法，提供实现 <xref:Microsoft.VisualStudio.Package.IScanner> 接口的对象。

 通过 <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> 方法为 <xref:Microsoft.VisualStudio.Package.IScanner> 扫描器提供一行源代码。 将重复调用 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> 方法，以获取行中的下一个标记，直到该行用尽了标记。 对于着色，MPF 将所有源代码视为一系列行。 因此，扫描程序必须能够处理作为行传入的源。 此外，可以随时将任何行传递到扫描程序，并且唯一保证是，扫描程序会从将要扫描的行之前的行接收状态变量。

 @No__t_0 类还用于标识标记触发器。 这些触发器告知 MPF，特定令牌可以启动更复杂的操作，如单词完成或匹配大括号。 由于确定此类触发器必须是快速的并且必须出现在任何位置，因此扫描程序最适合用于此任务。

 有关详细信息，请参阅[旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="parsing-for-functionality-and-scope"></a>分析功能和范围
 分析功能和作用域需要更多的精力，而不只是标识所遇到的令牌类型。 分析器不仅需要标识标记的类型，还需要标识用于标记的功能。 例如，标识符只是一个名称，但在您的语言中，标识符可以是类、命名空间、方法或变量的名称，具体取决于上下文。 令牌的常规类型可能是标识符，但标识符也可能具有其他含义，具体取决于它的定义和定义的位置。 此标识要求分析器更全面地了解正在分析的语言。 这是 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 类传入的位置。 @No__t_0 类收集有关标识符、方法、匹配语言对（如大括号和圆括号）和语言三元组的信息（与语言对类似，但有三个部分，例如 "`foreach()`" `{` "和" `}` "）. 此外，您还可以重写 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 类以支持代码标识，这种情况用于在对断点进行早期验证时使用，因此无需加载调试器，还可以**使用 "自动调试"** 窗口显示局部变量和参数在调试程序时自动进行，并且除了调试器提供的变量和参数外，还需要分析器标识相应的局部变量和参数。

 @No__t_0 对象作为 <xref:Microsoft.VisualStudio.Package.ParseRequest> 对象的一部分传递到分析器，每次创建新的 <xref:Microsoft.VisualStudio.Package.ParseRequest> 对象时都会创建一个新的 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 对象。 此外，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法必须返回一个用于处理各种 IntelliSense 操作的 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象。 @No__t_0 对象维护一个声明列表，并为方法（其中任何一个已填充的方法）列表，具体取决于分析的原因。 必须实现 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 类。

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)