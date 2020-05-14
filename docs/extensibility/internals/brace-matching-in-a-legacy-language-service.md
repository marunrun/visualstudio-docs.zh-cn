---
title: 旧语言服务中的大括号匹配 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- brace matching
- language services [managed package framework], brace matching
ms.assetid: 4e3d0a70-f22f-49dd-92d8-edf48ab62b52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0081be3e3ab5a53f7d85f77475d4288aa5c87092
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709809"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>旧语言服务中的支撑匹配
大括号匹配可帮助开发人员跟踪需要一起出现的语言元素，例如括号和大括号。 当开发人员进入关闭大括号时，打开大括号将突出显示。

 您可以匹配两个或三个共发生的元素，称为对和三重元素。 三重组是三个共发生元素集。 例如，在 C# 中`foreach`，语句形成三重`foreach()`：`{`和`}`。 键入右大括号时，所有三个元素都突出显示。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现大括号匹配的新方法的更多，请参阅[演练：显示匹配大括号](../../extensibility/walkthrough-displaying-matching-braces.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

 类<xref:Microsoft.VisualStudio.Package.AuthoringSink>支持 对和三重<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A>与 和<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A>方法。

## <a name="implementation"></a>实现
 语言服务需要标识语言中的所有匹配元素，然后找到所有匹配对。 这通常是通过实现<xref:Microsoft.VisualStudio.Package.IScanner>来检测匹配的语言，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>然后使用 方法匹配元素来实现的。

 该方法<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>调用扫描仪标记行并在 caret 之前返回令牌。 扫描程序指示通过在当前令牌上设置 的<xref:Microsoft.VisualStudio.Package.TokenTriggers>令牌触发器值找到语言元素对。 该方法<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>调用的方法<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>，该方法反过来调用<xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A>该方法具有解析原因值<xref:Microsoft.VisualStudio.Package.ParseReason>以查找匹配的语言元素。 找到匹配的语言元素时，这两个元素都会突出显示。

 有关键入大括号如何触发大括号突出显示的完整说明，请参阅文章["旧语言服务解析器"和"扫描器](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)"中的 *"示例解析"操作*部分。

## <a name="enable-support-for-brace-matching"></a>启用对大括号匹配的支持
 该<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性可以设置**匹配Braces、MatchBracesAtCaret**和**ShowMatchBrace**注册表项，这些注册表项设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类的相应属性。 **MatchBracesAtCaret** 也可以由用户设置语言首选项属性。

|注册表项|properties|描述|
|--------------------|--------------|-----------------|
|匹配支架|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|启用大括号匹配。|
|匹配支架AtCaret|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|启用大括号匹配，因为护理器移动。|
|显示匹配支架|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|突出显示匹配的大括号。|

## <a name="match-conditional-statements"></a>匹配条件语句
 `if`可以匹配条件语句，如 、`else if`和`else``#if``#elif``#else`、 `#endif`、、、、与匹配分隔符相同。 可以对类进行类<xref:Microsoft.VisualStudio.Package.AuthoringSink>子类，并提供一个方法，可以将文本范围以及分隔符添加到匹配元素的内部数组中。

## <a name="set-the-trigger"></a>设置触发器
 下面的示例演示如何检测匹配的括号、大括号和方形大括号，以及如何在扫描仪中为其设置触发器。 类<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>上<xref:Microsoft.VisualStudio.Package.Source>的方法检测触发器并调用解析器以查找匹配对（请参阅本文中的 *"查找匹配*"部分）。 此示例仅用于说明目的。 它假定扫描仪包含一个标识和返回`GetNextToken`文本行中的令牌的方法。

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

## <a name="match-the-braces"></a>匹配大括号
 下面是一个用于匹配语言`{ }`元素`( )`和`[ ]`以及将其范围添加到对象中的<xref:Microsoft.VisualStudio.Package.AuthoringSink>简化示例。 此方法不是分析源代码的建议方法;因此，此方法不是分析源代码的方法。仅用于说明目的。

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
- [传统语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [旧语言服务解析器和扫描仪](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
