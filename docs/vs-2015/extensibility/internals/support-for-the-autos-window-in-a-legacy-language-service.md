---
title: 对旧版语言服务中的自动窗口的支持 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157598"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>旧版语言服务中的自动窗口支持
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**自动**窗口将显示如变量和参数 （无论是由于一个断点或异常） 暂停正在调试的程序时作用域中的表达式。 表达式可以包含变量，本地或全局和局部范围内已更改的参数。 **自动**窗口还可以包括类、 结构或某些其他类型的实例化。 表达式计算器可以计算的任何内容可能会显示在**自动**窗口。  
  
 托管的包框架 (MPF) 不提供直接支持**自动**窗口。 但是，如果重写<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A>方法，可以返回一系列表达式中的呈现**自动**窗口。  
  
## <a name="implementing-support-for-the-autos-window"></a>实现对自动窗口的支持  
 您需要做以支持**自动**窗口是实现<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。 您的实现必须确定，给定表达式应出现在源文件中的位置**自动**窗口。 该方法返回字符串，其中每个字符串都表示一个表达式的列表。 返回值<xref:Microsoft.VisualStudio.VSConstants.S_OK>指示该列表包含表达式，而<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>指示没有要显示的表达式。  
  
 实际返回的表达式是变量或出现在该位置在代码中的参数的名称。 这些名称传递给表达式计算器才能获取值和类型，然后显示在**自动**窗口。  
  
### <a name="example"></a>示例  
 下面的示例演示的实现<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A>方法，可获取的表达式从一系列<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法使用的分析原因<xref:Microsoft.VisualStudio.Package.ParseReason>。 每个表达式被打包为`TestVsEnumBSTR`实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR>接口。  
  
 请注意，`GetAutoExpressionsCount`并`GetAutoExpression`方法是自定义方法上`TestAuthoringSink`对象，并添加了以支持此示例。 它们表示添加到哪个表达式中的一种方法`TestAuthoringSink`分析器的对象 (通过调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A>方法) 可以访问外部分析器。  
  
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
