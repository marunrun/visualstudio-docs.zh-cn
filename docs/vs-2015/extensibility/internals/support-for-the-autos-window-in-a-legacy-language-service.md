---
title: 支持旧版语言服务中的 "自动" 窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 01d2046d7693b23865555abb06962dead4a435ae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157598"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>旧版语言服务中的自动窗口支持
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

" **自动" 窗口** 显示一些表达式，如正在调试的程序 (由于断点或异常) 而暂停的变量和参数。 表达式可以包括局部变量、局部变量或全局参数，以及在局部范围内已更改的参数。 "自动" 窗口还可以包括类、结构或其他 **类型的实例** 化。 表达式计算器可以评估的任何内容可能会显示 **在 "自动** " 窗口中。  
  
 托管包框架 (MPF) 不提供 **对 "自动" 窗口的直接** 支持。 但是，如果你重写 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> 方法，则可以返回要显示在 "自动" 窗口中的**Autos**表达式列表。  
  
## <a name="implementing-support-for-the-autos-window"></a>实现对 "自动" 窗口的支持  
 只需实现类中的方法，即可支持 " **自动"** 窗口 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 。 你的实现必须在给定的位置中确定一个位置，表达式应显示在 "自动 **" 窗口中** 。 方法返回字符串列表，其中每个字符串都表示一个表达式。 的返回值 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 指示该列表包含表达式，而指示没有 <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> 要显示的表达式。  
  
 返回的实际表达式是在代码中出现在该位置的变量或参数的名称。 这些名称将传递给表达式计算器，以获取将在 "自动" 窗口中 **显示的值** 和类型。  
  
### <a name="example"></a>示例  
 下面的示例演示 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> 方法的实现，该实现 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 使用分析原因从方法获取表达式列表 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 每个表达式都包装为 `TestVsEnumBSTR` 实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> 接口的。  
  
 请注意， `GetAutoExpressionsCount` 和 `GetAutoExpression` 方法是对象上的自定义方法 `TestAuthoringSink` ，已添加为支持此示例。 它们代表了一种方法，通过调用方法将表达式添加到对象中， `TestAuthoringSink` (通过调用 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> 方法) 可在分析器外部访问。  
  
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
