---
title: 旧版语言服务中的大纲显示 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6b2ba55a2e77a1f7261812a181ad780c2ef2b71
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72726180"
---
# <a name="outlining-in-a-legacy-language-service"></a>旧版语言服务中的大纲显示
大纲显示可将复杂程序折叠为概述或大纲。 例如，在所有C#方法中，均可折叠为单个行，只显示方法签名。 此外，可以将结构和类折叠为仅显示结构和类的名称。 在单个方法中，通过仅显示 `foreach`、`if` 和 `while` 等语句的第一行，可以折叠复杂逻辑以显示总体流。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅[演练：大纲显示](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="enabling-support-for-outlining"></a>启用大纲支持
 @No__t_0 注册表项设置为1以启用自动大纲显示。 自动大纲显示加载或更改文件时，将对整个源进行分析，以便标识隐藏区域并显示大纲标志符号。 大纲还可以由用户手动控制。

 @No__t_0 注册表项的值可以通过 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 类的 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> 属性获取。 @No__t_0 注册表项可以使用命名参数初始化 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 属性（有关详细信息，请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)）。

## <a name="the-hidden-region"></a>隐藏区域
 若要提供大纲，你的语言服务必须支持隐藏区域。 这些是可展开或折叠的文本范围。 隐藏区域可以由标准语言符号（例如大括号）或自定义符号分隔。 例如， C#具有分隔隐藏区域的 `#region` / `#endregion` 对。

 隐藏区域由隐藏的区域管理器进行管理，该管理器作为 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 接口公开。

 大纲显示使用隐藏区域 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion> 接口，并包含隐藏区域的范围、当前可见状态以及在折叠范围时要显示的横幅。

 语言服务分析器使用 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> 方法为隐藏区域的默认行为添加新的隐藏区域，而 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> 方法允许您自定义大纲的外观和行为。 将隐藏区域分配给隐藏区域会话后，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 管理语言服务的隐藏区域。

 如果需要确定隐藏区域会话何时销毁，隐藏区域会发生更改，或者需要确保特定隐藏区域可见;您必须从 <xref:Microsoft.VisualStudio.Package.Source> 类派生一个类，并分别重写适当的方法： <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A>、<xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A> 和 <xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A>。

### <a name="example"></a>示例
 下面是为所有大括号创建隐藏区域的简化示例。 假定语言提供大括号匹配，并且要匹配的大括号至少包含大括号（{和}）。 此方法仅用于说明目的。 完全实现将对 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 中的事例进行完整处理。 此示例还演示如何将 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> 首选项设置为暂时 `true`。 一种替代方法是在语言包的 `ProvideLanguageServiceAttribute` 属性中指定 `AutoOutlining` 名为参数。

 此示例假设C#注释、字符串和文本的规则。

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