---
title: 旧版语言 Service2 中的参数信息 |Microsoft Docs
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
ms.openlocfilehash: dff6e871320d0727ed2fbec4188e8f7af2e5c5fe
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88237953"
---
# <a name="parameter-info-in-a-legacy-language-service-2"></a>旧版语言服务中的参数信息2
IntelliSense 参数信息是一个工具提示，当用户键入参数列表开始字符时，该工具会显示方法的签名 (通常为方法参数列表的左括号) 。 在输入每个参数并且参数分隔符 (通常是键入逗号) 时，工具提示将更新以显示以粗体显示的下一个参数。

 管理包框架 (MPF) 类提供对管理参数信息工具提示的支持。 分析器必须检测参数 start、parameter next 和 parameters 结束字符，并且必须提供方法签名及其关联参数的列表。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="implementation"></a>实现
 分析程序应设置在 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 找到参数列表开始字符时设置的触发器值 (通常) 左括号。 它 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 在查找参数分隔符时应设置触发器， (通常为逗号) 。 这将导致更新 "参数信息" 工具提示，并以粗体显示下一个参数。 <xref:Microsoft.VisualStudio.Package.TokenTriggers>如果找到参数列表结束字符 (通常) 右括号，则分析器应设置触发器值。

 <xref:Microsoft.VisualStudio.Package.TokenTriggers>触发器值启动对方法的调用 <xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A> ，该方法反过来调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法分析器，分析原因为 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 如果分析器确定参数列表开始字符之前的标识符是识别的方法名称，它将返回对象中匹配方法签名的列表 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 。 如果找到任何方法签名，则会在列表中显示第一个签名的参数信息工具提示。 然后，在键入签名时，将更新此工具提示。 键入参数列表结束字符后，将从视图中删除参数信息工具提示。

> [!NOTE]
> 若要确保参数信息工具提示的格式正确，必须重写类的属性 <xref:Microsoft.VisualStudio.Package.Methods> 以提供相应的字符。 基类 <xref:Microsoft.VisualStudio.Package.Methods> 采用 c # 样式的方法签名。 <xref:Microsoft.VisualStudio.Package.Methods>有关如何执行此操作的详细信息，请参阅类。

## <a name="enabling-support-for-the-parameter-info"></a>启用对参数信息的支持
 若要支持参数信息工具提示，必须将 `ShowCompletion` 的命名参数设置 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 为 `true` 。 语言服务从属性读取此注册表项的值 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> 。

 此外，必须将 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A> 属性设置为，才能 `true` 显示参数信息工具提示。

### <a name="example"></a>示例
 下面是检测参数列表字符和设置适当触发器的简单示例。 此示例仅用于说明目的。 它假定您的扫描程序包含一个方法 `GetNextToken` ，该方法用于标识和返回文本行中的标记。 示例代码只是在发现正确的字符类型时设置触发器。

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

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>支持分析器中的参数信息工具提示
 <xref:Microsoft.VisualStudio.Package.Source>类在 <xref:Microsoft.VisualStudio.Package.AuthoringScope> <xref:Microsoft.VisualStudio.Package.AuthoringSink> 显示和更新参数信息工具提示时对和类的内容作出一些假设。

- <xref:Microsoft.VisualStudio.Package.ParseReason>类型化参数列表开始字符时，将提供分析器。

- 对象中指定的位置 <xref:Microsoft.VisualStudio.Package.ParseRequest> 紧跟在参数列表开始字符之后。 分析器必须收集该位置可用的所有方法声明的签名，并将其存储在对象版本的列表中 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 。 此列表包括方法名称、方法类型 (或返回类型) ，以及可能参数的列表。 稍后将在此列表中搜索要在参数信息工具提示中显示的方法签名或签名。

  然后，分析器必须分析对象指定的行 <xref:Microsoft.VisualStudio.Package.ParseRequest> ，以收集所输入的方法的名称以及用户在键入参数中的距离。 这是通过将方法的名称传递给对象的方法来实现的， <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink> 然后 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> 在分析参数列表开始字符时调用方法，分析参数 <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> 列表下一个字符时调用方法，最后在 <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> 分析参数列表结束字符时调用方法。 类使用这些方法调用的结果 <xref:Microsoft.VisualStudio.Package.Source> 来相应地更新参数信息工具提示。

### <a name="example"></a>示例
 下面是用户可能输入的文本行。 该行下面的数字指示分析器在行中该位置执行的步骤， (假设分析从左到右移动) 。 此处的假设是已经为方法签名（包括 "testfunc" 方法签名）分析了行之前的所有内容。

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 下面概述了分析器使用的步骤：

1. 分析器调用 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> 带有文本 "testfunc" 的。

2. 分析器调用 <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> 。

3. 分析器调用 <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> 。

4. 分析器调用 <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> 。
