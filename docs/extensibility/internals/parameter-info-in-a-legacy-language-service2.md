---
title: 旧版语言服务 2 中的参数信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ed95be7611c4733e2d10691bb0bf5eeb798a67b4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314667"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>旧版语言服务中的参数信息
参数的 IntelliSense 信息是在用户键入的参数列表时显示的一种方法签名的工具提示启动的方法参数列表的字符 （通常左括号）。 在输入每个参数和类型化参数分隔符 （通常为逗号） 时，工具提示将更新以显示下一个参数以粗体显示。

 托管的包框架 (MPF) 类提供用于管理参数信息工具提示支持。 分析器必须检测参数启动，则参数接下来，并且参数结束字符，并且它必须提供方法签名和及其相关的参数的列表。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="implementation"></a>实现
 分析器应设置触发器值<xref:Microsoft.VisualStudio.Package.TokenTriggers>找到参数列表的开始字符 （通常左括号） 时设置。 应设置<xref:Microsoft.VisualStudio.Package.TokenTriggers>找到参数分隔符 （通常逗号） 时触发。 这将导致参数信息工具提示，以更新并显示下一个参数以粗体显示。 分析器应设置触发器值<xref:Microsoft.VisualStudio.Package.TokenTriggers>时如果查找的参数列表末尾字符 （通常右括号）。

 <xref:Microsoft.VisualStudio.Package.TokenTriggers>触发器值开始调用<xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A>方法，后者又调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法分析器分析原因为<xref:Microsoft.VisualStudio.Package.ParseReason>。 如果分析器会认为该标识符的参数列表的开始字符之前是已识别的方法名称，它将返回一系列匹配方法签名中的<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象。 如果未找到任何方法签名，参数信息工具提示会显示在列表中的第一个签名。 随输入的多个签名，然后将更新该工具提示。 参数列表末尾字符键入时，将从视图中删除参数信息工具提示。

> [!NOTE]
> 若要确保正确格式化的参数信息工具提示，您必须在重写属性<xref:Microsoft.VisualStudio.Package.Methods>类，以提供相应的字符。 基<xref:Microsoft.VisualStudio.Package.Methods>类假定 C#-样式方法签名。 请参阅<xref:Microsoft.VisualStudio.Package.Methods>有关如何执行此操作的详细信息的类。

## <a name="enabling-support-for-the-parameter-info"></a>启用对参数信息的支持
 若要支持的参数信息工具提示，必须设置`ShowCompletion`名为的参数<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>到`true`。 语言服务中读取中此注册表项的值<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>属性。

 此外，<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A>属性必须设置为`true`的参数信息工具提示显示。

### <a name="example"></a>示例
 下面是检测参数列表字符并设置相应的触发器的简化的示例。 此示例是仅供说明用途。 它假定您的扫描仪，包含一种方法`GetNextToken`的标识，并返回从文本行的令牌。 示例代码只需设置触发器，只要它发现正确类型的字符。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char parameterListStartChar = '(';
        private const char parameterListEndChar   = ')';
        private const char parameterNextChar      = ',';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (Char.IsPunctuation(c))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                    tokenInfo.EndIndex = index;

                    if (c == parameterListStartChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterStart;
                    }
                    else if (c == parameterListNextChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterNext;
                    else if (c == parameterListEndChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterEnd;
                    }
                }
            return foundToken;
        }
    }
}
```

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>在分析器中支持的参数信息工具提示
 <xref:Microsoft.VisualStudio.Package.Source>类会进行某些假设的内容<xref:Microsoft.VisualStudio.Package.AuthoringScope>和<xref:Microsoft.VisualStudio.Package.AuthoringSink>类时显示和更新的参数信息工具提示。

- 给定分析器<xref:Microsoft.VisualStudio.Package.ParseReason>时键入参数列表的起始字符。

- 给定的位置<xref:Microsoft.VisualStudio.Package.ParseRequest>对象是参数列表的起始字符之后立即。 分析器必须收集的位置并将其存储在你的版本的列表中的所有可在方法声明签名<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象。 此列表包括方法名称，方法类型 （或返回类型），以及可能的参数的列表。 更高版本的方法签名或签名的参数信息工具提示中显示搜索此列表。

  分析器必须然后分析由指定的行<xref:Microsoft.VisualStudio.Package.ParseRequest>中键入参数是对象来收集输入的方法以及多久完成用户的名称。 这通过传递到方法的名称来实现<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A>方法<xref:Microsoft.VisualStudio.Package.AuthoringSink>对象，然后再调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>分析方法时参数列表的起始字符时，调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>方法时参数列表下一个字符是已分析，并最后调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>方法分析的参数列表末尾字符时。 将使用这些方法调用的结果<xref:Microsoft.VisualStudio.Package.Source>类，以相应地更新参数信息工具提示。

### <a name="example"></a>示例
 下面是文本的用户可能输入行。 线下方的数字表示哪些步骤均由该位置中的行 （假设分析移动从左到右） 分析器。 此处的假设是，在行之前的所有内容已进行分析的方法签名，包括"testfunc"方法签名。

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 解析程序采用的步骤如下所示：

1. 分析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A>带有文本"testfunc"。

2. 分析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>。

3. 分析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>。

4. 分析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>。