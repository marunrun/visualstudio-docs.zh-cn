---
title: 旧版语言服务中的大纲显示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6096f89a36cdd47d2dec68af5801a94dc77acb43
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408562"
---
# <a name="outlining-in-a-legacy-language-service"></a>旧版语言服务中的大纲显示
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

大纲显示使可能复杂程序折叠为概述或大纲。 例如，在 C# 中的所有方法可以都折叠为单个行，其中显示仅方法签名。 此外，结构和类可以折叠以显示仅的结构和类的名称。 在单一方法中，可以折叠复杂逻辑以通过如显示的语句中的，仅第一行中显示的总体流程`foreach`， `if`，和`while`。  
  
 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[演练：大纲显示](../../extensibility/walkthrough-outlining.md)。  
  
> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。  
  
## <a name="enabling-support-for-outlining"></a>启用支持用于大纲显示  
 `AutoOutlining`注册表项设置为 1 以启用自动大纲显示。 自动大纲显示设置了整个源的分析，加载或更改，以确定的隐藏的区域并显示大纲显示标志符号文件时。 大纲显示也能受手动用户。  
  
 值`AutoOutlining`可以通过获取注册表项<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A>属性上的<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。 `AutoOutlining`注册表项可以使用的命名参数初始化<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性 (请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)有关详细信息)。  
  
## <a name="the-hidden-region"></a>隐藏的区域  
 若要提供大纲显示，你的语言服务必须支持的隐藏的区域。 这些是的可以展开或折叠文本范围。 可以通过标准的语言符号，如大括号，或通过自定义的符号分隔的隐藏的区域。 例如，具有 C# `#region` / `#endregion`分隔隐藏的区域对。  
  
 隐藏的区域管理的隐藏的区域管理器，它公开为<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>接口。  
  
 大纲显示使用的隐藏的区域<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion>接口，并包含隐藏的区域、 当前可见的状态和跨度处于折叠状态时显示的横幅的跨度。  
  
 语言服务分析器会采用<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A>方法以添加新的隐藏的区域隐藏区域的默认行为时<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A>方法，可自定义外观和行为的概要中。 一旦到隐藏的区域会话中，提供的隐藏的区域[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]管理语言服务的隐藏的区域。  
  
 如果需要确定销毁隐藏的区域会话时，隐藏的区域发生更改，或者您需要确保特定的隐藏的区域可见，则你必须从派生类<xref:Microsoft.VisualStudio.Package.Source>类，并替换为适当的方法， <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A>， <xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A>，和<xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A>分别。  
  
### <a name="example"></a>示例  
 下面是创建为所有成对的大括号的隐藏的区域的简化的示例。 将假定该语言提供了大括号匹配，并在大括号匹配至少包括大括号 （{和}）。 这种方法是仅供说明用途。 完整的实现必须全面的处理中的事例<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>。 此示例还演示如何设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A>首选项设置为`true`暂时。 一种替代方法是指定`AutoOutlining`中的参数名为`ProvideLanguageServiceAttribute`语言包中的属性。  
  
 此示例假定 C# 注释、 字符串和文本的规则。  
  
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
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)   
 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
