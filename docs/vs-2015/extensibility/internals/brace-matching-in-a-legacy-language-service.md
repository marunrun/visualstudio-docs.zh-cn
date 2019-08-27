---
title: 旧版语言服务中的括号匹配 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- brace matching
- language services [managed package framework], brace matching
ms.assetid: 4e3d0a70-f22f-49dd-92d8-edf48ab62b52
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d6d7243c8032b22f9abe89021af138f638729011
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437636"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>旧版语言服务中的大括号匹配
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

大括号匹配可帮助开发人员跟踪需要发生在一起，例如成对的圆括号和大括号的语言元素。 当开发人员输入一个右大括号时，左大括号突出显示。  
  
 你可以匹配两个或三个一起出现的元素，调用对和三元组。 三元组是三个一起出现的元素的集合。 例如，在 C#`foreach`语句构成三元组:"`foreach()`"，"`{`"，并"`}`"。 键入右大括号时，将突出显示所有三个元素。  
  
 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现的大括号匹配的新方法的详细信息，请参阅[演练：显示匹配的括号](../../extensibility/walkthrough-displaying-matching-braces.md)。  
  
> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。  
  
 <xref:Microsoft.VisualStudio.Package.AuthoringSink>类支持这两个对，用两倍<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A>和<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A>方法。  
  
## <a name="implementation"></a>实现  
 语言服务需要确定语言中的所有匹配的元素，然后查找所有匹配对。 这通常通过实现<xref:Microsoft.VisualStudio.Package.IScanner>检测匹配的语言，然后使用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法来匹配的元素。  
  
 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用的扫描程序以对行进行词汇切分并返回之前插入符号的标记。 通过设置令牌触发器值找到了一个语言元素对扫描程序指示<xref:Microsoft.VisualStudio.Package.TokenTriggers>上当前的令牌。 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>又会调用的方法<xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A>方法的分析原因值<xref:Microsoft.VisualStudio.Package.ParseReason>查找匹配的语言元素。 当找到匹配的语言元素时，这两个元素将突出显示。  
  
 有关如何键入大括号触发的大括号突出显示的完整说明，请参阅本主题中的"示例分析操作"部分[旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。  
  
## <a name="enabling-support-for-brace-matching"></a>启用支持的大括号匹配  
 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性可以设置`MatchBraces`， `MatchBracesAtCaret`，和`ShowMatchingBrace`名为设置相应的属性的参数<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。 此外可以由用户设置语言首选项属性。  
  
|注册表项|属性|描述|  
|--------------------|--------------|-----------------|  
|`MatchBraces`|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|启用大括号匹配|  
|`MatchBracesAtCaret`|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|启用大括号匹配作为插入点移动。|  
|`ShowMatchingBrace`|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|会突出显示匹配括号。|  
  
## <a name="matching-conditional-statements"></a>匹配条件语句  
 如与匹配条件语句`if`， `else if`，并`else`，或`#if`， `#elif`， `#else`， `#endif`，方式与匹配的分隔符相同。 你可以子类化<xref:Microsoft.VisualStudio.Package.AuthoringSink>类，并提供到内部数组的匹配元素的分隔符以及跨越可以添加文本的方法。  
  
## <a name="setting-the-trigger"></a>设置触发器  
 下面的示例演示如何检测到匹配的括号、 大括号和方括号，并在扫描程序中为其设置触发器。 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法<xref:Microsoft.VisualStudio.Package.Source>类检测该触发器，并调用分析器来查找匹配的对 （请参阅本主题中的"查找匹配项"部分）。 此示例是仅供说明用途。 它假定您的扫描仪，包含一种方法`GetNextToken`的标识，并返回从文本行的令牌。  
  
```csharp  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    public class TestScanner : IScanner  
    {  
        private const string braces = "()[]{}";  
        private Lexer lex;  
  
        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,  
                                                   ref int state)  
        {  
            bool foundToken = false;  
            string token = lex.GetNextToken();  
            if (token != null)  
            {  
                foundToken = true;  
                char firstChar = token[0];  
                if (Char.IsPunctuation(firstChar) && token.Length > 0)  
                {  
                    if (braces.IndexOf(firstChar) != -1)  
                    {  
                        tokenInfo.Trigger = TokenTriggers.MatchBraces;  
                    }  
                }  
            }  
            return foundToken;  
        }  
```  
  
## <a name="matching-the-braces"></a>匹配大括号  
 下面是一个简化的示例匹配的语言元素 {}，（） 和 []，并添加到其范围<xref:Microsoft.VisualStudio.Package.AuthoringSink>对象。 此方法不是分析源代码; 的建议的方法它是仅供说明用途。  
  
```csharp  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    public class Parser  
    {  
         private IList<TextSpan[]> m_braces;  
         public IList<TextSpan[]> Braces  
         {  
             get { return m_braces; }  
         }  
         private void AddMatchingBraces(TextSpan braceSpan1, TextSpan braceSpan2)  
         {  
             if IsMatch(braceSpan1, braceSpan2)  
                 m_braces.Add(new TextSpan[] { braceSpan1, braceSpan2 });  
         }  
  
         private bool IsMatch(TextSpan braceSpan1, TextSpan braceSpan2)  
         {  
             //definition for matching here  
          }  
    }  
  
    public class TestLanguageService : LanguageService  
    {  
         Parser parser = new Parser();  
         Source source = (Source) this.GetSource(req.FileName);  
  
         private AuthoringScope ParseSource(ParseRequest req)  
         {  
             if (req.Sink.BraceMatching)  
             {  
                 if (req.Reason==ParseReason.MatchBraces)  
                 {  
                     foreach (TextSpan[] brace in parser.Braces)  
                     {  
                         req.Sink.MatchPair(brace[0], brace[1], 1);  
                     }  
                 }  
             }  
             return new TestAuthoringScope();  
         }  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)   
 [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
