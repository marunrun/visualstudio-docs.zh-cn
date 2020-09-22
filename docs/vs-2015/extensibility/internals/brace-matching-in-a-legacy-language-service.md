---
title: 旧版语言服务中的大括号匹配 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840391"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>旧版语言服务中的大括号匹配
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

大括号匹配有助于开发人员跟踪需要同时出现的语言元素，如括号和大括号。 当开发人员输入右大括号时，将突出显示左大括号。  
  
 可以匹配两个或三个共同发生的元素，称为对等。 三元组是三个共同发生的元素的集合。 例如，在 c # 中， `foreach` 语句形成了三个： " `foreach()` "、" `{` " 和 " `}` "。 键入右大括号时，将突出显示所有三个元素。  
  
 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现大括号匹配的新方法的详细信息，请参阅 [演练：显示匹配的大括号](../../extensibility/walkthrough-displaying-matching-braces.md)。  
  
> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。  
  
 <xref:Microsoft.VisualStudio.Package.AuthoringSink>类支持和三对 <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A> 和 <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A> 方法。  
  
## <a name="implementation"></a>实现  
 语言服务需要标识语言中的所有匹配元素，然后查找所有匹配对。 这通常通过实现 <xref:Microsoft.VisualStudio.Package.IScanner> 来检测匹配的语言，然后使用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法匹配元素。  
  
 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用扫描器以标记行并在插入符号的紧前面返回标记。 扫描程序通过 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 在当前令牌上设置的令牌触发器值来指示已找到语言元素对。 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>方法调用方法 <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> ，该方法将调用 <xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A> 具有分析原因值的方法 <xref:Microsoft.VisualStudio.Package.ParseReason> 来查找匹配的语言元素。 当找到匹配的语言元素时，将突出显示这两个元素。  
  
 有关键入大括号如何触发大括号突出显示的完整说明，请参阅主题 [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)中的 "示例分析操作" 一节。  
  
## <a name="enabling-support-for-brace-matching"></a>启用对大括号匹配的支持  
 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>特性可以设置 `MatchBraces` 、 `MatchBracesAtCaret` 和 `ShowMatchingBrace` 命名参数，这些参数用于设置类的对应属性 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。 还可以由用户设置语言首选项属性。  
  
|注册表项|Property|说明|  
|--------------------|--------------|-----------------|  
|`MatchBraces`|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|启用大括号匹配|  
|`MatchBracesAtCaret`|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|启用与插入符号移动的大括号匹配。|  
|`ShowMatchingBrace`|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|突出显示匹配的大括号。|  
  
## <a name="matching-conditional-statements"></a>匹配条件语句  
 可以通过与 `if` `else if` `else` `#if` `#elif` `#else` `#endif` 匹配分隔符相同的方式匹配条件语句，如、、和。 您可以为 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 类添加子类，并提供一个方法，该方法可以将文本范围以及分隔符添加到匹配元素的内部数组。  
  
## <a name="setting-the-trigger"></a>设置触发器  
 下面的示例演示如何检测匹配的括号、大括号和方括号，并在扫描程序中为其设置触发器。 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>类上的方法将 <xref:Microsoft.VisualStudio.Package.Source> 检测触发器，并调用分析器来查找匹配对 (参阅本主题中的 "查找匹配项" 部分) 。 此示例仅用于说明目的。 它假定您的扫描程序包含一个方法 `GetNextToken` ，该方法用于标识和返回文本行中的标记。  
  
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
 下面是一个简化的示例，用于匹配语言元素 {}、 ( ) 和 []，并将其范围添加到 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 对象。 此方法不是用于分析源代码的建议方法;它仅用于说明目的。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)   
 [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
