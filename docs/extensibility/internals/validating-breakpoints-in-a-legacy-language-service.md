---
title: 验证传统语言服务中的断点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af09e4f8f2156100bea9267c92ffebeb64ce1aa3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704096"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>验证旧版语言服务中的断点
断点指示程序执行应在调试器中运行时在特定点停止。 用户可以在源文件中的任何行上放置断点，因为编辑器不知道什么是断点的有效位置。 启动调试器时，所有标记的断点（称为挂起断点）都绑定到正在运行的程序中的相应位置。 同时验证断点，以确保它们标记有效的代码位置。 例如，注释上的断点无效，因为源代码中该位置没有代码。 调试器禁用无效的断点。

 由于语言服务知道正在显示的源代码，它可以在启动调试器之前验证断点。 可以重写<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>方法以返回指定断点有效位置的跨距。 启动调试器时，断点位置仍被验证，但用户会收到无效断点的通知，而无需等待调试器加载。

## <a name="implementing-support-for-validating-breakpoints"></a>实施对验证断点的支持

- 给出<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>断点的位置的方法。 您的实现必须确定该位置是否有效，并通过返回标识与断点位置的行位置关联的代码的文本范围来指示这一点。

- 如果<xref:Microsoft.VisualStudio.VSConstants.S_OK>位置有效，或者<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>该位置无效，则返回。

- 如果断点有效，则文本范围将与断点一起突出显示。

- 如果断点无效，状态栏中将显示一条错误消息。

### <a name="example"></a>示例
 此示例演示调用解析器以获取指定<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>位置的代码范围（如果有）的方法的实现。

 本示例假定您向`GetCodeSpan`<xref:Microsoft.VisualStudio.Package.AuthoringSink>类添加了一个方法，该类验证文本范围，如果文本范围`true`是有效的断点位置，则返回该方法。

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
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
