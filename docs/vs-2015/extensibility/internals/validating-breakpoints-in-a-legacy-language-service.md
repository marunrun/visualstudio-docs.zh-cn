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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68163683"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>验证旧版语言服务中的断点
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

断点指示当程序在调试器中运行时，程序执行应在某个特定时间点停止。 用户可以在源文件中的任意行上放置一个断点，因为该编辑器并不知道哪些内容构成了断点的有效位置。 启动调试器时，所有标记的断点 (称为挂起断点) 被绑定到正在运行的程序中的适当位置。 同时对断点进行验证，以确保它们标记有效的代码位置。 例如，注释上的断点无效，因为源代码中的该位置没有代码。 调试器将禁用无效断点。  
  
 由于语言服务知道要显示的源代码，因此它可以在启动调试器之前验证断点。 您可以重写 <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> 方法以返回指定断点的有效位置的跨度。 启动调试器时仍会验证断点位置，但不等待调试器加载时，用户将收到无效断点的通知。  
  
## <a name="implementing-support-for-validating-breakpoints"></a>实现对验证断点的支持  
  
- 向 <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> 方法提供断点的位置。 你的实现必须确定位置是否有效，并通过返回一个文本跨度来指示这一点，该文本跨度标识与断点的行位置关联的代码。  
  
- <xref:Microsoft.VisualStudio.VSConstants.S_OK>如果位置有效，则返回; 如果无效，则返回 <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> 。  
  
- 如果断点有效，文本跨距将与断点一起突出显示。  
  
- 如果该断点无效，状态栏中将显示一条错误消息。  
  
### <a name="example"></a>示例  
 此示例演示 <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> 方法的实现，该方法调用分析器以获取指定位置的任何)  (的代码范围。  
  
 此示例假设已向类添加了一个 `GetCodeSpan` 方法 <xref:Microsoft.VisualStudio.Package.AuthoringSink> ，用于验证文本跨距并在 `true` 它是有效的断点位置时返回。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
