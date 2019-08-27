---
title: 验证旧版语言服务中的断点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f54dc683aa4287145a27e22d49397241b395f69f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163683"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>验证旧版语言服务中的断点
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

断点指示它在调试器中运行时程序执行应停止的特定点。 用户可以在源文件中的任意行上放置一个断点，因为在编辑器并不知道什么构成了断点的有效位置。 启动调试器时，所有标记断点 （称为挂起断点） 将绑定到正在运行的程序中的相应位置。 在同一时间断点进行验证，以便确保它们将标记有效的代码位置。 例如上一条注释, 的断点无效，因为在源代码中该位置没有任何代码。 调试器将禁用无效的断点。  
  
 由于语言服务知道有关所显示的源代码，它可以验证断点，之后再启动调试器。 您可以重写<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>方法以返回指定断点的有效位置的跨度。 启动调试器，但无需等待调试器加载的无效的断点会通知用户时，仍被验证断点位置。  
  
## <a name="implementing-support-for-validating-breakpoints"></a>实现支持用于验证断点  
  
- <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>方法给定的断点的位置。 您的实现必须确定位置有效，以及指示此通过返回标识的代码的文本跨距关联的行位置断点。  
  
- 返回<xref:Microsoft.VisualStudio.VSConstants.S_OK>位置是否有效，或<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>如果不是有效。  
  
- 如果断点有效文本范围将突出显示以及断点。  
  
- 如果断点无效，在状态栏中会显示一条错误消息。  
  
### <a name="example"></a>示例  
 此示例演示一种实现<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>方法，用于指定位置处调用分析器以获取代码的范围 （如果有）。  
  
 此示例假定您已添加`GetCodeSpan`方法<xref:Microsoft.VisualStudio.Package.AuthoringSink>类，用于验证在文本范围，并返回`true`如果它是有效的断点位置。  
  
```csharp  
using Microsoft VisualStudio;  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    class TestLanguageService : LanguageService  
    {  
        public override int ValidateBreakpointLocation(IVsTextBuffer buffer,  
                                                       int line,  
                                                       int col,  
                                                       TextSpan[] pCodeSpan)  
        {  
            int retval = VSConstants.S_FALSE;  
            if (pCodeSpan != null)  
            {  
                // Initialize span to current line by default.  
                pCodeSpan[0].iStartLine = line;  
                pCodeSpan[0].iStartIndex = col;  
                pCodeSpan[0].iEndLine = line;  
                pCodeSpan[0].iEndIndex = col;  
            }  
  
            if (buffer != null)  
            {  
                IVsTextLines textLines = buffer as IVsTextLines;  
                if (textLines != null)  
                {  
                    Source src = this.GetSource(textLines);  
                    if (src != null)  
                    {  
                        TokenInfo tokenInfo = new TokenInfo();  
                        string text = src.GetText();  
                        ParseRequest req = CreateParseRequest(src,  
                                                              line,  
                                                              col,  
                                                              tokenInfo,  
                                                              text,  
                                                              src.GetFilePath(),  
                                                              ParseReason.CodeSpan,  
                                                              null);  
                        req.Scope = this.ParseSource(req);  
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;  
  
                        TextSpan span = new TextSpan();  
                        if (sink.GetCodeSpan(out span))  
                        {  
                            pCodeSpan[0] = span;  
                            retval = VSConstants.S_OK;  
                        }  
                    }  
                }  
            }  
            return retval;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
