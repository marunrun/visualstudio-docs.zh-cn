---
title: 传统语言服务解析器和扫描仪 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c87f447a4b8bca804d27aae4967f4adaf389c627
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707317"
---
# <a name="legacy-language-service-parser-and-scanner"></a>旧版语言服务分析器和扫描程序
解析器是语言服务的核心。 托管包框架 （MPF） 语言类需要语言解析器来选择有关显示的代码的信息。 解析器将文本分隔成词法标记，然后按类型和功能标识这些标记。

## <a name="discussion"></a>讨论区
 下面是 C# 方法。

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

 在此示例中，标记是单词和标点符号。 令牌的种类如下。

|令牌名称|令牌类型|
|----------------|----------------|
|命名空间， 类， 公共， 无效， int|关键字 (keyword)|
|=|运算符后的表达式|
|{ } ( ) ;|delimiter|
|MyNamespace， 我的类， 我的功能， arg1， var1|标识符 (identifier)|
|我的命名空间|namespace|
|MyClass|class|
|我的功能|method|
|arg1|参数 (parameter)|
|瓦尔1|局部变量 (local variable)|

 解析器的作用是标识令牌。 某些令牌可以有多个类型。 解析器标识令牌后，语言服务可以使用该信息提供有用的功能，如语法突出显示、大括号匹配和 IntelliSense 操作。

## <a name="types-of-parsers"></a>分析器的类型
 语言服务解析器与用作编译器一部分的解析器不同。 但是，这种解析器需要同时使用扫描仪和解析器，就像编译器解析器一样。

- 扫描仪用于标识令牌的类型。 此信息用于语法突出显示和快速标识可触发其他操作（例如括号匹配）的标记类型。 此扫描仪由<xref:Microsoft.VisualStudio.Package.IScanner>接口表示。

- 解析器用于描述令牌的函数和范围。 此信息用于 IntelliSense 操作中，用于标识语言元素，如方法、变量、参数和声明，并基于上下文提供成员和方法签名的列表。 此解析器还用于查找匹配的语言元素对，如大括号和括号。 此解析器通过<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法进行访问。

  如何为语言服务实现扫描仪和分析程序由您决定。 有几个资源可用于描述解析器的工作原理以及如何编写自己的解析器。 此外，还有几种免费和商业产品，有助于创建解析器。

### <a name="the-parsesource-parser"></a>The ParseSource Parser
 与用作编译器一部分的解析器（其中令牌转换为某种形式的可执行代码）不同，可以出于许多不同的原因和许多不同的上下文中调用语言服务解析器。 如何在<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法中实现此方法由您决定。 请务必记住，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>该方法可能在后台线程上调用。

> [!CAUTION]
> 结构<xref:Microsoft.VisualStudio.Package.ParseRequest>包含对<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象的引用。 此<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象不能在后台线程中使用。 事实上，许多基本 MPF 类不能在后台线程中使用。 其中包括 、<xref:Microsoft.VisualStudio.Package.Source><xref:Microsoft.VisualStudio.Package.ViewFilter>类<xref:Microsoft.VisualStudio.Package.CodeWindowManager>和直接或间接与视图通信的任何其他类。

 此解析器通常在首次调用整个源文件或给出 的<xref:Microsoft.VisualStudio.Package.ParseReason>解析原因值时对其进行分析。 对 方法的<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>后续调用处理已分析代码的一小部分，并且可以使用上一个完整分析操作的结果更快地执行。 该方法<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>通过<xref:Microsoft.VisualStudio.Package.AuthoringSink>和<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象传达分析操作的结果。 该<xref:Microsoft.VisualStudio.Package.AuthoringSink>对象用于收集特定分析原因的信息，例如，有关匹配大括号或具有参数列表的方法签名范围的信息。 提供<xref:Microsoft.VisualStudio.Package.AuthoringScope>声明和方法签名的集合，并支持"转到高级编辑"选项（**转到定义**、**转到声明**、**转到引用**）。

### <a name="the-iscanner-scanner"></a>IScanner 扫描仪
 还必须实现 实现<xref:Microsoft.VisualStudio.Package.IScanner>的扫描程序。 但是，由于此扫描仪通过<xref:Microsoft.VisualStudio.Package.Colorizer>类逐行运行，因此通常更容易实现。 在每行的开头，MPF 为<xref:Microsoft.VisualStudio.Package.Colorizer>类提供一个值，用作传递给扫描仪的状态变量。 在每行的末尾，扫描仪返回更新的状态变量。 MPF 缓存每行的状态信息，以便扫描程序可以从任何行开始解析，而无需从源文件的开头开始。 这种对单行的快速扫描使编辑器能够向用户提供快速反馈。

## <a name="parsing-for-matching-braces"></a>分析匹配大括号
 此示例显示用于匹配用户键入的关闭大括号的控制流。 在此过程中，用于着色的扫描仪还用于确定令牌的类型以及令牌是否可以触发匹配括号操作。 如果找到触发器，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>则调用 该方法以查找匹配的大括号。 最后，两个大括号高亮显示。

 即使大括号用于触发器的名称和分析原因，此过程也不限于实际大括号。 支持指定为匹配对的任何字符对。 示例包括 （\<和 ） 和 > 以及 [ 和 ] 和 ] 。

 假定语言服务支持匹配大括号。

1. 用户键入关闭大括号 （*）。

2. 大括号插入到源文件中的光标上，光标由 1 前进。

3. <xref:Microsoft.VisualStudio.Package.Source>类<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>中的方法使用键入的闭合大括号调用。

4. 方法<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>调用类中<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A><xref:Microsoft.VisualStudio.Package.Source>的方法以在当前游标位置之前的位置获取令牌。 此令牌对应于键入的右大括号）。

    1. 该方法<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>调用<xref:Microsoft.VisualStudio.Package.Colorizer>对象上<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>的方法以获取当前行上的所有令牌。

    2. 该方法<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>使用当前行<xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A>的文本调用<xref:Microsoft.VisualStudio.Package.IScanner>对象上的方法。

    3. 该方法<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>反复调用<xref:Microsoft.VisualStudio.Package.IScanner>对象上<xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A>的方法以从当前行收集所有令牌。

    4. 该方法<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>调用类中的<xref:Microsoft.VisualStudio.Package.Source>私有方法以获取包含所需位置的令牌，并传递从<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法获取的令牌列表中。

5. 该方法<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>在从<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法返回的令牌上<xref:Microsoft.VisualStudio.Package.TokenTriggers>查找 令牌触发器标志;即表示关闭大括号的令牌）。

6. 如果找到 的<xref:Microsoft.VisualStudio.Package.TokenTriggers>触发器标志，则调用<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A><xref:Microsoft.VisualStudio.Package.Source>类中的方法。

7. 该方法<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>启动具有 的解析原因值的<xref:Microsoft.VisualStudio.Package.ParseReason>解析操作。 此操作最终调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类上的方法。 如果启用异步分析，则对该方法<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>的此调用将发生在后台线程上。

8. 分析操作完成后，`HandleMatchBracesResponse`<xref:Microsoft.VisualStudio.Package.Source>类中调用名为的内部完成处理程序（也称为回调方法）。 此调用由<xref:Microsoft.VisualStudio.Package.LanguageService>基类自动进行，而不是由解析器进行。

9. 该方法`HandleMatchBracesResponse`从存储在<xref:Microsoft.VisualStudio.Package.AuthoringSink><xref:Microsoft.VisualStudio.Package.ParseRequest>对象中的对象获取范围列表。 （范围是指定<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>源文件中的行和字符范围的结构。此范围列表通常包含两个范围，每个范围用于开口和关闭大括号。

10. 该方法`HandleBracesResponse`调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A>存储在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView><xref:Microsoft.VisualStudio.Package.ParseRequest>对象中的对象上的方法。 这将突出显示给定的跨度。

11. 如果启用<xref:Microsoft.VisualStudio.Package.LanguagePreferences>了<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>该属性，`HandleBracesResponse`该方法将获取匹配范围包含的文本，并在状态栏中显示该范围的前 80 个字符。 如果<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>该方法包含匹配对附带的语言元素，则此方法效果最佳。 有关更多信息，请参见 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 属性。

12. 完成。

### <a name="summary"></a>总结
 匹配的大括号操作通常仅限于简单的语言元素对。 更复杂的元素，如匹配三重`if(...)`元素（""，""`{`和""，"`}`或"""""""`else``{`和""），`}`可以作为单词完成操作的一部分突出显示。 例如，当"else"字完成后，可以突出显示匹配的""`if`语句。 如果有一系列`if`/`else if`语句，则可以使用与匹配大括号相同的机制突出显示所有这些语句。 基<xref:Microsoft.VisualStudio.Package.Source>类已经支持此功能，如下所示：扫描程序必须返回令牌触发器值<xref:Microsoft.VisualStudio.Package.TokenTriggers>与游标位置之前标记的触发器<xref:Microsoft.VisualStudio.Package.TokenTriggers>值组合。

 有关详细信息，请参阅[旧语言服务中的"大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)"。

## <a name="parsing-for-colorization"></a>色化分析
 着色源代码非常简单，只需标识令牌的类型并返回有关该类型的颜色信息。 类<xref:Microsoft.VisualStudio.Package.Colorizer>充当编辑器和扫描仪之间的中介，以提供有关每个令牌的颜色信息。 类<xref:Microsoft.VisualStudio.Package.Colorizer>使用 对象<xref:Microsoft.VisualStudio.Package.IScanner>帮助对行着色，还收集源文件中所有行的状态信息。 在 MPF 语言服务类中<xref:Microsoft.VisualStudio.Package.Colorizer>，不必重写该类，因为它只能通过<xref:Microsoft.VisualStudio.Package.IScanner>接口与扫描仪通信。 通过重写<xref:Microsoft.VisualStudio.Package.LanguageService>类上的方法来<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>提供<xref:Microsoft.VisualStudio.Package.IScanner>实现接口的对象。

 通过<xref:Microsoft.VisualStudio.Package.IScanner><xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A>该方法为扫描仪提供了一行源代码。 重复对<xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A>方法的调用以获取行中的下一个令牌，直到行用完令牌。 对于着色，MPF 将所有源代码视为行序列。 因此，扫描仪必须能够处理源作为行。 此外，任何线路可以随时传递到扫描仪，唯一的保证是扫描仪在要扫描的行之前从行接收状态变量。

 该<xref:Microsoft.VisualStudio.Package.Colorizer>类还用于标识令牌触发器。 这些触发器告诉 MPF 特定令牌可以启动更复杂的操作，例如单词完成或匹配大括号。 由于识别此类触发器必须快速，并且必须在任何位置发生，因此扫描仪最适合此任务。

 有关详细信息，请参阅[旧语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。

## <a name="parsing-for-functionality-and-scope"></a>分析功能和范围
 分析功能和范围需要付出更多的努力，而不仅仅是识别遇到的令牌类型。 解析器不仅要标识令牌的类型，还要标识使用令牌的功能。 例如，标识符只是一个名称，但在您的语言中，标识符可以是类、命名空间、方法或变量的名称，具体取决于上下文。 令牌的一般类型可能是标识符，但标识符可能还有其他含义，具体取决于它是什么和在哪里定义它。 此标识要求解析器对正在分析的语言有更广泛的知识。 这就是<xref:Microsoft.VisualStudio.Package.AuthoringSink>课程的用处。 该<xref:Microsoft.VisualStudio.Package.AuthoringSink>类收集有关标识符、方法、匹配语言对（如大括号和括号）和语言三重（类似于语言对，但有三个部分，例如""""`foreach()``{`和"）`}`的信息。 此外，还可以重写<xref:Microsoft.VisualStudio.Package.AuthoringSink>类以支持代码标识（用于早期验证断点，以便不必加载调试器）和**Autos**调试窗口，该窗口在调试程序时自动显示局部变量和参数，并要求解析器除调试器提供这些变量和参数外，还标识适当的局部变量和参数。

 对象<xref:Microsoft.VisualStudio.Package.AuthoringSink>作为<xref:Microsoft.VisualStudio.Package.ParseRequest>对象的一部分传递给解析器，并且每次创建新<xref:Microsoft.VisualStudio.Package.AuthoringSink><xref:Microsoft.VisualStudio.Package.ParseRequest>对象时都会创建新对象。 此外，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>该方法必须返回一个<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象，该对象用于处理各种 IntelliSense 操作。 对象<xref:Microsoft.VisualStudio.Package.AuthoringScope>维护声明的列表和方法的列表，其中任一都填充，具体取决于分析的原因。 必须<xref:Microsoft.VisualStudio.Package.AuthoringScope>实现类。

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)
- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
