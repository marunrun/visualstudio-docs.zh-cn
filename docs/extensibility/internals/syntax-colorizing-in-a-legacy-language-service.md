---
title: 旧版语言服务中的语法着色 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: edbb7f2dca6bc0bc28a328276680dd9e273f4176
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331136"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>旧版语言服务中的语法着色
语法颜色设置是一项功能，使不同的编程语言来显示不同的颜色和样式中的源代码文件中的元素。 若要支持此功能，您需要提供分析器或扫描程序识别词法元素或在文件中的标记的类型。 许多语言的着色它们以不同的方式加以区别关键字、 分隔符 （例如圆括号或大括号） 和注释。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="implementation"></a>实现
 若要支持着色，托管的包框架 (MPF) 包括<xref:Microsoft.VisualStudio.Package.Colorizer>类，该类实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口。 与此类交互<xref:Microsoft.VisualStudio.Package.IScanner>以确定令牌和颜色。 扫描程序的详细信息，请参阅[旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。 <xref:Microsoft.VisualStudio.Package.Colorizer>类，然后将标记每个字符的具有颜色信息的令牌和该信息返回到编辑器中显示的源文件。

 返回到编辑器的颜色信息是为一系列可着色项的索引。 每个可着色项指定颜色值和一系列的字体特性，如粗体或删除线。 编辑器中提供语言服务可以使用的默认可着色项的组。 需要做的就是指定每种令牌类型的适当的颜色索引。 但是，可以提供一组自定义可着色项和您提供的索引的令牌，并引用而不是默认列表可着色项的列表。 您还必须设置`RequestStockColors`为 0 的注册表项 (或不指定`RequestStockColors`处所有项) 来支持自定义颜色。 可以设置到一个命名参数与此注册表项<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>用户定义的属性。 注册语言服务并设置其选项的详细信息，请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

## <a name="custom-colorable-items"></a>自定义可着色项
 若要提供自己的自定义可着色项，必须重写<xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A>并<xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A>方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。 第一种方法返回的语言服务支持的自定义可着色项数和第二个按索引获取自定义可着色项。 创建自定义可着色项的默认列表。 在语言服务的构造函数中，您需要做是提供一个名称与每个可着色项。 Visual Studio 会自动处理其中用户选择一组不同的可着色项的情况。 此名称将会出现在**字体和颜色**上的属性页**选项**对话框 (可从 Visual Studio**工具**菜单) 和此名称确定将哪个用户已重写的颜色。 在注册表中缓存中存储和访问的颜色名称的用户的选择。 **字体和颜色**属性页列出了所有的颜色名称按字母顺序，因此可以按你的语言名称; 每个颜色名称之前分组自定义颜色，如"**TestLanguage 注释**"和"**TestLanguage-关键字**"。 可以按类型，你可着色项进行分组或者"**注释 (TestLanguage)** "和"**关键字 (TestLanguage)** "。 按语言名称分组是首选方法。

> [!CAUTION]
> 强烈建议在要避免与现有的可着色项名称发生冲突的可着色项名称中包括的语言名称。

> [!NOTE]
> 如果在开发过程中更改一个您的颜色的名称，必须重置 Visual Studio 创建第一次访问了您的颜色的缓存。 可以执行此操作通过运行**重置实验性配置单元**从 Visual Studio SDK 程序菜单命令。

 请注意，永远不会引用可着色项列表中的第一个项。 Visual Studio 始终会将默认文本颜色和该项的属性提供。 解决此问题的最简单方法是提供作为第一项的占位符可着色项。

### <a name="high-color-colorable-items"></a>高颜色可着色项
 可着色项还可以支持 24 位或高颜色值到<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>接口。 MPF<xref:Microsoft.VisualStudio.Package.ColorableItem>类支持<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>正常颜色以及构造函数中指定接口和 24 位颜色。 有关更多详细信息，请参见 <xref:Microsoft.VisualStudio.Package.ColorableItem> 类。 下面的示例演示如何设置关键字和注释的 24 位颜色。 在用户的桌面上; 支持 24 位颜色时，将使用 24 位颜色否则，使用普通文本颜色。

 请记住，这些是你的语言; 的默认颜色用户可以更改为所需的任何这些颜色。

### <a name="example"></a>示例
 此示例演示一种方法来声明和使用自定义可着色项数组中填充<xref:Microsoft.VisualStudio.Package.ColorableItem>类。 此示例设置关键字和注释使用 24 位颜色的颜色。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private ColorableItem[] m_colorableItems;

        TestLanguageService() : base()
        {
            m_colorableItems = new ColorableItem[] {
                new ColorableItem("TestLanguage - Text",
                                  "Text",
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.Empty,
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT),
                new ColorableItem("TestLanguage - Keyword",
                                  "Keyword",
                                  COLORINDEX.CI_MAROON,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.FromArgb(192,32,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_BOLD),
                new ColorableItem("TestLanguage - Comment",
                                  "Comment",
                                  COLORINDEX.CI_DARKGREEN,
                                  COLORINDEX.CI_LIGHTGRAY,
                                  System.Drawing.Color.FromArgb(32,128,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT)
                // ...
                // Add as many colorable items as you want to support.
            };
        }
    }
}
```

## <a name="the-colorizer-class-and-the-scanner"></a>着色器类和扫描程序
 基<xref:Microsoft.VisualStudio.Package.LanguageService>类具有<xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A>方法的 instantiantes<xref:Microsoft.VisualStudio.Package.Colorizer>类。 从返回的扫描程序<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法将传递给<xref:Microsoft.VisualStudio.Package.Colorizer>类构造函数。

 必须实现<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>自己的版本中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。 <xref:Microsoft.VisualStudio.Package.Colorizer>类使用扫描程序获取令牌的颜色的所有信息。

 扫描程序需要填充<xref:Microsoft.VisualStudio.Package.TokenInfo>进行安排为每个令牌中找到。 此结构包含的信息，如跨度令牌占用，颜色索引可以使用，是哪种类型的令牌和令牌触发器 (请参阅<xref:Microsoft.VisualStudio.Package.TokenTriggers>)。 仅跨和颜色索引所需的通过着色<xref:Microsoft.VisualStudio.Package.Colorizer>类。

 颜色索引存储在<xref:Microsoft.VisualStudio.Package.TokenInfo>结构通常是一个介于<xref:Microsoft.VisualStudio.Package.TokenColor>枚举，它提供了一定数量的命名对应于各种语言元素，如关键字和运算符的索引。 如果你的自定义可着色项列表中的匹配项中显示项<xref:Microsoft.VisualStudio.Package.TokenColor>枚举，则你可以只使用枚举作为颜色为每个令牌。 但是，如果其他可着色项或不想使用该顺序中的现有值，您可以排列自定义可着色项列表来满足您的需要并返回到该列表中的适当的索引。 只是一定要强制转换到的索引<xref:Microsoft.VisualStudio.Package.TokenColor>时将其存储在<xref:Microsoft.VisualStudio.Package.TokenInfo>结构;[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)]会看到仅索引。

### <a name="example"></a>示例
 下面的示例演示如何扫描程序可能会识别三种令牌类型： 数字、 标点符号和标识符 （任何不是数字或标点）。 此示例仅供说明用途，并不表示一个全面的分析器和扫描程序实现。 它假定存在`Lexer`类的`GetNextToken()`方法返回的字符串。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    private Lexer lex;

    public class TestScanner : IScanner
    {
        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                }
                else if (Char.IsNumber(firstChar))
                {
                    tokenInfo.Type = TokenType.Literal;
                    tokenInfo.Color = TokenColor.Number;
                }
                else
                {
                    tokenInfo.Type = TokenType.Identifier;
                    tokenInfo.Color = TokenColor.Identifier;
                }
            }
            return foundToken;
        }
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)