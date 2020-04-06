---
title: 在传统语言服务中概述 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be485a0e7406d49c4dcce77958c720e0b62504b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706814"
---
# <a name="outlining-in-a-legacy-language-service"></a>旧版语言服务中的大纲显示
大纲使复杂的程序折叠成概述或大纲成为可能。 例如，在 C# 中，所有方法都可以折叠到一行，仅显示方法签名。 此外，可以折叠结构和类，仅显示结构和类的名称。 在单个方法内，可以通过仅显示 语句的第一行（如`foreach`、`if`和`while`）来折叠复杂逻辑以显示总体流。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[演练：概述](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="enabling-support-for-outlining"></a>支持大纲
 注册表`AutoOutlining`项设置为 1 以启用自动大纲。 自动大纲在加载或更改文件时设置整个源的解析，以便识别隐藏区域并显示大纲字形。 大纲也可以由用户手动控制。

 `AutoOutlining`注册表项的值可以通过<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A><xref:Microsoft.VisualStudio.Package.LanguagePreferences>类上的属性获取。 注册表`AutoOutlining`项可以使用<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性的命名参数进行初始化（有关详细信息，请参阅[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)）。

## <a name="the-hidden-region"></a>隐藏区域
 要提供大纲，您的语言服务必须支持隐藏区域。 这些是可以展开或折叠的文本范围。 隐藏区域可以由标准语言符号（如大括号）或自定义符号分隔。 例如，C# 具有`#region`/`#endregion`分隔隐藏区域的对。

 隐藏区域由隐藏区域管理器管理，该管理器作为<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>接口公开。

 大纲使用隐藏区域接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion>，并包含隐藏区域的范围、当前可见状态和折叠时要显示的横幅。

 语言服务解析器使用<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A>方法添加具有隐藏区域默认行为的新隐藏区域，而<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A>该方法允许您自定义大纲的外观和行为。 将隐藏区域提供给隐藏区域会话后，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理语言服务的隐藏区域。

 如果需要确定何时销毁隐藏区域会话，则更改隐藏区域，或者需要确保特定隐藏区域可见;否则，需要确保隐藏区域可见。必须从<xref:Microsoft.VisualStudio.Package.Source>类派生一个类，并分别重写相应的方法<xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A>、<xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A>和<xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A>。

### <a name="example"></a>示例
 下面是为所有大括号创建隐藏区域的简化示例。 假定语言提供大括号匹配，并且要匹配的大括号至少包括大括号 （* 和 *）。 这种方法仅用于说明目的。 全面实施将完全处理 中的<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>案例。 此示例还演示如何<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A>`true`暂时设置首选项。 另一种方法是在语言包`AutoOutlining`中`ProvideLanguageServiceAttribute`的属性中指定命名参数。

 此示例假定注释、字符串和文本的 C# 规则。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{

    public class MyLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences  GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(MyLanguageService).GUID,
                                                        Name);
                m_preferences.Init();
                // Temporarily enabled auto-outlining
                m_preferences.AutoOutlining = true;
            }
            return m_preferences;
        }

        public override AuthoringScope  ParseSource(ParseRequest req)
        {
            Source source = (Source) this.GetSource(req.FileName);
            switch (req.Reason)
            {
               case ParseReason.HighlightBraces:
               case ParseReason.MatchBraces:
               case ParseReason.MemberSelectAndHighlightBraces:
                  if (source.Braces != null)
                  {
                      foreach (TextSpan[] brace in source.Braces)
                      {
                         if (brace.Length == 2)
                         {
                             if (req.Sink.HiddenRegions == true
                                   && source.GetText(brace[0]).Equals("{")
                                   && source.GetText(brace[1]).Equals("}"))
                             {
                                //construct a TextSpan of everything between the braces
                                TextSpan hideSpan = new TextSpan();
                                hideSpan.iStartIndex = brace[0].iStartIndex;
                                hideSpan.iStartLine = brace[0].iStartLine;
                                hideSpan.iEndIndex = brace[1].iEndIndex;
                                hideSpan.iEndLine = brace[1].iEndLine;
                                req.Sink.ProcessHiddenRegions = true;
                                req.Sink.AddHiddenRegion(hideSpan);
                             }
                             req.Sink.MatchPair(brace[0], brace[1], 1);
                         }
                         else if (brace.Length >= 3)
                             req.Sink.MatchTriple(brace[0], brace[1], brace[2], 1);
                  }
        }
                   break;
               default:
                   break;
      }
            // Must always return a valid AuthoringScope object.
            return new MyAuthoringScope();
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
