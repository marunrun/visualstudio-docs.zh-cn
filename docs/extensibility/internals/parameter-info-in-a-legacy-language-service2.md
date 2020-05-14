---
title: 旧语言服务中的参数信息2 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e2c40c9ca5c038a70714545f4133db0c0dd686d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706746"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>旧版语言服务中的参数信息
IntelliSense 参数信息是一个工具提示，当用户键入方法参数列表的参数列表开始字符（通常是打开的括号）时，显示方法的签名。 当输入每个参数并键入参数分隔符（通常是逗号）时，工具提示将更新以粗体显示下一个参数。

 托管包框架 （MPF） 类支持管理参数信息工具提示。 解析器必须检测参数开始、参数下一个和参数结束字符，并且必须提供方法签名及其关联参数的列表。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="implementation"></a>实现
 解析器应设置触发值<xref:Microsoft.VisualStudio.Package.TokenTriggers>，当它找到参数列表开始字符（通常是开放的括号）时设置它。 当它找到参数分隔<xref:Microsoft.VisualStudio.Package.TokenTriggers>符（通常是逗号）时，它应设置触发器。 这将导致更新参数信息工具提示，以粗体显示下一个参数。 如果找到参数列表结束字符（通常是<xref:Microsoft.VisualStudio.Package.TokenTriggers>近括号），解析器应设置触发器值。

 触发器<xref:Microsoft.VisualStudio.Package.TokenTriggers>值启动对 方法的<xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A>调用，该方法反过来调用具有<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A><xref:Microsoft.VisualStudio.Package.ParseReason>分析原因的方法解析器。 如果解析器确定参数列表开始字符之前的标识符是可识别的方法名称，它将返回<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象中的匹配方法签名的列表。 如果找到任何方法签名，则参数信息工具提示将显示列表中的第一个签名。 然后，当键入更多的签名时，将更新此工具提示。 键入参数列表结束字符时，将从视图中删除参数信息工具提示。

> [!NOTE]
> 为了确保参数信息工具提示的格式正确，必须重写<xref:Microsoft.VisualStudio.Package.Methods>类的属性以提供相应的字符。 基<xref:Microsoft.VisualStudio.Package.Methods>类假定 C#样式的方法签名。 有关如何完成<xref:Microsoft.VisualStudio.Package.Methods>此操作的详细信息，请参阅该类。

## <a name="enabling-support-for-the-parameter-info"></a>启用参数信息支持
 要支持参数信息工具提示，必须将 的`ShowCompletion`<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>命名参数设置为`true`。 语言服务从<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>属性中读取此注册表项的值。

 此外，<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A>必须将`true`属性设置为"参数信息"工具提示才能显示。

### <a name="example"></a>示例
 下面是检测参数列表字符和设置相应触发器的简化示例。 此示例仅用于说明目的。 它假定扫描仪包含一个标识和返回`GetNextToken`文本行中的令牌的方法。 示例代码只要看到正确的字符类型，即可设置触发器。

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

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>支持解析器中的参数信息工具提示
 当<xref:Microsoft.VisualStudio.Package.Source>显示和更新参数信息工具提示时，类<xref:Microsoft.VisualStudio.Package.AuthoringScope>对<xref:Microsoft.VisualStudio.Package.AuthoringSink>和 类的内容进行一些假设。

- 键入参数列表开始字符<xref:Microsoft.VisualStudio.Package.ParseReason>时，将给出解析器。

- 对象中<xref:Microsoft.VisualStudio.Package.ParseRequest>给出的位置紧接参数列表开始字符。 解析器必须收集该位置上可用的所有方法声明的签名，并将它们存储在<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象版本中的列表中。 此列表包括方法名称、方法类型（或返回类型）和可能参数的列表。 稍后将搜索此列表，查找要在参数信息工具提示中显示的方法签名或签名。

  然后，解析器必须分析<xref:Microsoft.VisualStudio.Package.ParseRequest>对象指定的行，以收集要输入的方法的名称以及用户在键入参数方面所走的路。 这是通过将方法的名称<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A>传递给<xref:Microsoft.VisualStudio.Package.AuthoringSink>对象上的方法，然后在解析参数列表开始字符时调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>该方法，在解析参数列表下一个字符时调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>该方法，最后在解析参数列表结束字符时调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>该方法来实现。 <xref:Microsoft.VisualStudio.Package.Source>类使用这些方法调用的结果来适当地更新参数信息工具提示。

### <a name="example"></a>示例
 下面是用户可能输入的文本行。 行下方的数字指示解析器在行中该位置执行哪个步骤（假设解析移动从左到右）。 此处的假设是，行之前的所有内容已解析为方法签名，包括"testfunc"方法签名。

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 解析器执行的步骤概述如下：

1. 解析器使用文本<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A>"testfunc"调用。

2. 解析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>。

3. 解析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>。

4. 解析器调用<xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>。
