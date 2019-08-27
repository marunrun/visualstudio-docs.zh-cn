---
title: 旧版语言服务分析器和扫描程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 64f9a9f4d0785f033191ab527084f0dddb1ff104
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434365"
---
# <a name="legacy-language-service-parser-and-scanner"></a>旧版语言服务分析器和扫描程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

分析器是语言服务的核心。 托管包框架 (MPF) 语言类需要一个语言分析器，以选择要显示的代码有关的信息。 分析器将文本分隔成词法标记，然后确定这些令牌的类型和功能。  
  
## <a name="discussion"></a>讨论  
 下面是一个 C# 方法。  
  
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
  
 在此示例中，令牌是单词和标点符号。 类型的标记如下所示。  
  
|令牌名称|标记类型|  
|----------------|----------------|  
|命名空间、 类、 公共的 void、 int|keyword|  
|=|operator|  
|{ } ( ) ;|分隔符|  
|MyNamespace、 MyClass、 MyFunction、 arg1、 var1|identifier|  
|MyNamespace|namespace|  
|MyClass|class|  
|MyFunction|方法|  
|arg1|参数|  
|var1|本地变量|  
  
 分析器的角色是确定令牌。 某些令牌可以具有多个类型。 分析器已识别令牌后，可以使用语言服务，以提供有用的功能，如语法突出显示，大括号匹配、 的信息和 IntelliSense 操作。  
  
## <a name="types-of-parsers"></a>类型的分析器  
 语言服务分析器不与同一编译器的过程中使用的分析器相同。 但是，这种类型的分析器需要编译器分析程序相同的方式使用扫描仪和分析器。  
  
- 扫描程序用于标识类型的令牌。 语法突出显示和快速标识令牌类型，可以触发其他操作，例如，大括号匹配使用此信息。 此扫描程序由<xref:Microsoft.VisualStudio.Package.IScanner>接口。  
  
- 一个分析器用于描述的功能和范围的令牌。 确定语言元素，如方法、 变量、 参数和声明，并提供了成员和基于上下文的方法签名的列表，在 IntelliSense 操作中使用此信息。 此分析器还用于查找匹配的语言元素对，例如，大括号和括号。 通过访问此分析器<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。  
  
  您如何实现为语言服务扫描器和分析器是取决于您。 提供了多个资源，用于描述分析器的工作原理以及如何编写您自己的分析程序。 此外，多个免费和商用产品都可在创建一个分析器的帮助。  
  
### <a name="the-parsesource-parser"></a>ParseSource 分析器  
 与不同的编译器 （其中令牌转换为某种形式的可执行代码） 的一部分使用的分析器，原因有多种不同，在许多不同的上下文中，可以调用语言服务分析器。 如何实现在这种方法<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类是由您决定。 务必要记住的<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>可能会在后台线程上调用方法。  
  
> [!CAUTION]
> <xref:Microsoft.VisualStudio.Package.ParseRequest>结构包含对引用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象。 这<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象不能使用在后台线程中。 事实上，许多 MPF 基类不能在后台线程中使用。 其中包括<xref:Microsoft.VisualStudio.Package.Source>， <xref:Microsoft.VisualStudio.Package.ViewFilter>，<xref:Microsoft.VisualStudio.Package.CodeWindowManager>类和其他任何直接或间接与视图进行通信的类。  
  
 此分析器通常分析整个源文件第一个时间调用它或分析时原因的值<xref:Microsoft.VisualStudio.Package.ParseReason>提供。 对后续调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法处理的已分析的代码的一小部分，并可以通过使用上一个完整的分析操作的结果更加迅速地执行。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法来传递通过分析操作的结果<xref:Microsoft.VisualStudio.Package.AuthoringSink>和<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象。 <xref:Microsoft.VisualStudio.Package.AuthoringSink>对象用于为特定的分析原因，例如，span 的信息匹配大括号或具有参数列表的方法签名中收集信息。 <xref:Microsoft.VisualStudio.Package.AuthoringScope>提供的声明和方法签名以及支持集合对于转到高级的编辑选项 (**转到定义**，**转到声明**，**转到引用**)。  
  
### <a name="the-iscanner-scanner"></a>IScanner 扫描程序  
 您还必须实现的扫描程序实现<xref:Microsoft.VisualStudio.Package.IScanner>。 但是，由于在通过-逐行的基础上运行此扫描程序<xref:Microsoft.VisualStudio.Package.Colorizer>类，它是通常更轻松地实现。 在每个行的开头，MPF 使<xref:Microsoft.VisualStudio.Package.Colorizer>类要用作传递给扫描程序的状态变量的值。 在每个行结束时，扫描程序返回已更新的状态变量。 MPF 缓存每个行的此状态信息，以便扫描程序可以开始分析从任何行，而无需在源文件开头开始。 此快速扫描单个行允许编辑器向用户提供快速反馈。  
  
## <a name="parsing-for-matching-braces"></a>分析，以进行匹配的大括号  
 此示例演示用于匹配用户键入一个右大括号的控制流。 在此过程中，用于着色的扫描程序还用于确定令牌和令牌是否可以触发匹配大括号操作的类型。 如果找到该触发器，则<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>调用方法来查找匹配的括号。 最后，将突出显示两个大括号。  
  
 即使在大括号中的触发器的名称使用和分析的原因，此过程不局限于实际大括号。 支持任何被指定为一对匹配的字符对。 示例包括 （和），\<和 >，和 [和]。  
  
 假定该语言服务支持匹配大括号。  
  
1. 在用户键入右大括号 （}）。  
  
2. 在源文件中的光标处插入大括号和光标高级 1。  
  
3. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>中的方法<xref:Microsoft.VisualStudio.Package.Source>类调用与类型化的右大括号。  
  
4. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>中的方法<xref:Microsoft.VisualStudio.Package.Source>类来获取当前光标位置之前的位置处的令牌。 此标记对应的类型化的右大括号）。  
  
    1. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法调用<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法<xref:Microsoft.VisualStudio.Package.Colorizer>对象，以获取当前行上的所有令牌。  
  
    2. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法调用<xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A>方法<xref:Microsoft.VisualStudio.Package.IScanner>对象与当前行的文本。  
  
    3. <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法将重复调用<xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A>方法<xref:Microsoft.VisualStudio.Package.IScanner>对象从当前行中收集的所有令牌。  
  
    4. <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法调用的私有方法<xref:Microsoft.VisualStudio.Package.Source>类来获取令牌，其中包含所需的位置，并从获取的令牌列表中的传递<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>方法。  
  
5. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法查找的一个令牌触发器标志<xref:Microsoft.VisualStudio.Package.TokenTriggers>从返回的令牌上<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>方法; 即，表示右大括号的标记)。  
  
6. 如果触发器的标志<xref:Microsoft.VisualStudio.Package.TokenTriggers>找到，则<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>中的方法<xref:Microsoft.VisualStudio.Package.Source>调用类。  
  
7. <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>方法启动的分析操作中的分析原因值<xref:Microsoft.VisualStudio.Package.ParseReason>。 此操作最终调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。 如果启用了异步分析，则此调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法在后台线程上发生。  
  
8. 在分析操作完成后，名为内部完成处理程序 （也称为回调方法）`HandleMatchBracesResponse`名为<xref:Microsoft.VisualStudio.Package.Source>类。 自动进行此调用<xref:Microsoft.VisualStudio.Package.LanguageService>基类，不是由分析器。  
  
9. `HandleMatchBracesResponse`方法获取从范围列表<xref:Microsoft.VisualStudio.Package.AuthoringSink>对象存储在<xref:Microsoft.VisualStudio.Package.ParseRequest>对象。 (对 span<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>结构，它在源文件中指定的一系列行和字符。)此列表的范围通常包含两个范围，分别用于左和右大括号。  
  
10. `HandleBracesResponse`方法调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>对象，它存储在<xref:Microsoft.VisualStudio.Package.ParseRequest>对象。 它突出显示了给定的范围。  
  
11. 如果<xref:Microsoft.VisualStudio.Package.LanguagePreferences>属性<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>已启用，`HandleBracesResponse`方法获取匹配的范围包含并在状态栏中显示该范围内的前 80 个字符的文本。 这最适用如果<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法包含附带的匹配对的语言元素。 有关更多信息，请参见 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 属性。  
  
12. 完成。  
  
### <a name="summary"></a>总结  
 匹配大括号操作是通常限制为简单的语言元素对。 更复杂的元素，如匹配三元组 ("`if(…)`"，"`{`"和"`}`"，或"`else`"、"`{`"和"`}`")，可以突出显示文字自动完成操作的一部分。 例如，完成"else"一词后，匹配"`if`"语句可以突出显示。 如果有一系列`if` / `else if`语句，所有这些无法通过使用相同的机制为匹配的大括号突出显示。 <xref:Microsoft.VisualStudio.Package.Source>基本类已支持此操作，请按如下所示：扫描程序必须返回令牌的触发器值<xref:Microsoft.VisualStudio.Package.TokenTriggers>与触发器值结合使用<xref:Microsoft.VisualStudio.Package.TokenTriggers>令牌之前，光标位置。  
  
 有关详细信息，请参阅[旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)。  
  
## <a name="parsing-for-colorization"></a>分析颜色设置  
 着色的源代码非常简单，只需标识该类型的令牌和返回颜色信息的类型。 <xref:Microsoft.VisualStudio.Package.Colorizer>类充当编辑器和扫描程序以提供有关每个令牌中的颜色信息之间的媒介。 <xref:Microsoft.VisualStudio.Package.Colorizer>类使用<xref:Microsoft.VisualStudio.Package.IScanner>对象以便于进行着色的行，并还收集源代码文件中的所有行的状态信息。 MPF 语言服务类中<xref:Microsoft.VisualStudio.Package.Colorizer>类没有需要重写，因为它与扫描程序只能通过<xref:Microsoft.VisualStudio.Package.IScanner>接口。 提供实现的对象<xref:Microsoft.VisualStudio.Package.IScanner>接口通过重写<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。  
  
 <xref:Microsoft.VisualStudio.Package.IScanner>扫描程序有源代码行的行通过<xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A>方法。 调用<xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A>方法重复以获取行中的下一个标记，直到行耗尽的令牌。 对着色，MPF 视为一系列行中添加所有源代码。 因此，扫描程序必须能够处理与在它即将作为行的源。 此外，任何行可以在任何时候，传递给扫描程序，只能保证，扫描程序将收到来自之前要进行扫描的行的行状态变量。  
  
 <xref:Microsoft.VisualStudio.Package.Colorizer>类还用于确定令牌的触发器。 这些触发器告诉 MPF 特定令牌可以启动一个更复杂的操作，例如完整单词或匹配的大括号。 标识此类触发器必须是快速，并且必须在任何位置，因为扫描程序是最适合此任务。  
  
 有关详细信息，请参阅[旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。  
  
## <a name="parsing-for-functionality-and-scope"></a>分析功能和作用域  
 分析功能和作用域需要更多的工作比只识别的遇到的令牌类型。 分析器必须标识类型的令牌： 不仅还使用该令牌的功能。 例如，标识符是只是一个名称，但在您的语言标识符可能的类、 命名空间、 方法或变量，具体取决于上下文的名称。 令牌的常规类型可能是一个标识符，但标识符可能还具有其他含义，具体取决于它是什么和定义位置。 此标识需要具有更广泛的了解正在分析的语言分析器。 这就是<xref:Microsoft.VisualStudio.Package.AuthoringSink>类传入。 <xref:Microsoft.VisualStudio.Package.AuthoringSink>类收集有关标识符、 方法、 匹配的语言对 （如大括号和括号） 和语言三元组的信息 (类似于语言对不同的是三部分组成，例如，"`foreach()`""`{`"和"`}`")。 此外，您可以重写<xref:Microsoft.VisualStudio.Package.AuthoringSink>类，以支持代码标识断点的早期验证中使用，以便调试器不一定要加载，并**自动**调试窗口，其中显示本地变量和参数自动当程序正在调试并需要分析器以标识相应的本地变量和除了调试器可显示的参数。  
  
 <xref:Microsoft.VisualStudio.Package.AuthoringSink>对象传递给分析器作为的一部分<xref:Microsoft.VisualStudio.Package.ParseRequest>对象和一个新<xref:Microsoft.VisualStudio.Package.AuthoringSink>对象是每次创建一个新<xref:Microsoft.VisualStudio.Package.ParseRequest>创建对象。 此外，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法必须返回<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象，用于处理各种 IntelliSense 操作。 <xref:Microsoft.VisualStudio.Package.AuthoringScope>对象维护的声明列表和列表的方法，或者其中已填充，具体取决于用于分析的原因。 <xref:Microsoft.VisualStudio.Package.AuthoringScope>必须实现类。  
  
## <a name="see-also"></a>请参阅  
 [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)   
 [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)   
 [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)   
 [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
