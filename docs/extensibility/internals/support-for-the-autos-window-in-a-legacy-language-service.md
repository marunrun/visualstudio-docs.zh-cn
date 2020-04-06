---
title: 支持旧语言服务中的自动窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 75f8c761721dde5dad4bb75b8675f71f678b06df
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704887"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>旧版语言服务中的自动窗口支持
**"自动"** 窗口显示表达式，如变量和参数，这些表达式在调试的程序暂停时位于作用域中（由于断点或异常）。 这些表达式可以包括变量、局部变量或全局变量以及已在本地作用域中更改的参数。 **"自动"** 窗口还可以包括类、结构或某些其他类型的实例化。 表达式赋值器可以计算的任何内容都可能显示在 **"自动"** 窗口中。

 托管包框架 （MPF） 不提供对**自动窗口**的直接支持。 但是，如果重写方法，<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A>则可以返回要在 **"自动"** 窗口中显示的表达式列表。

## <a name="implementing-support-for-the-autos-window"></a>实现对自动窗口的支持
 支持**Autos**窗口只需在<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中实现 该方法。 在源文件中的位置，实现必须决定哪些表达式应出现在 **"自动"** 窗口中。 该方法返回字符串列表，其中每个字符串表示单个表达式。 的<xref:Microsoft.VisualStudio.VSConstants.S_OK>返回值表示列表包含表达式，而<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>表示没有要显示的表达式。

 返回的实际表达式是出现在代码中该位置的变量或参数的名称。 这些名称将传递给表达式赋值器，以获取随后在 **"自动"** 窗口中显示的值和类型。

### <a name="example"></a>示例
 下面的示例显示了使用分析原因<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A><xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A><xref:Microsoft.VisualStudio.Package.ParseReason>从 方法获取表达式列表的方法的实现。 每个表达式都包装为实现接口的`TestVsEnumBSTR`<xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR>。

 请注意，`GetAutoExpressionsCount`和`GetAutoExpression`方法是对象上的`TestAuthoringSink`自定义方法，并且添加是为了支持此示例。 它们表示解析器向`TestAuthoringSink`对象添加的表达式（通过调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A>方法）可以在解析器外部访问的一种方式。

```csharp
using Microsoft.VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override int GetProximityExpressions(IVsTextBuffer buffer,
                                                    int line,
                                                    int col,
                                                    int cLines,
                                                    out IVsEnumBSTR ppEnum)
        {
            int retval = VSConstants.E_NOTIMPL;
            ppEnum = null;
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
                                                              ParseReason.Autos,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        retval = VSConstants.S_FALSE;
                        int spanCount = sink.GetAutoExpressionsCount();
                        if (spanCount > 0) {
                            TestVsEnumBSTR bstrList = new TestVsEnumBSTR();
                            for (int i = 0; i < spanCount; i++)
                            {
                                TextSpan span;
                                sink.GetAutoExpression(i, out span);
                                string expression = src.GetText(span.iStartLine,
                                                                span.iStartIndex,
                                                                span.iEndLine,
                                                                span.iEndIndex);
                                bstrList.AddString(expression);
                            }
                            ppEnum = bstrList;
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
