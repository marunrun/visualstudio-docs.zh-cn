---
title: 旧语言服务中的语法着色 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 02723a09254255b98291cb921ae5ec091d8b9859
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704706"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>旧版语言服务中的语法着色
语法着色是一种功能，它会导致编程语言的不同元素以不同的颜色和样式显示在源文件中。 要支持此功能，您需要提供一个解析器或扫描仪，用于标识文件中的词法元素或令牌的类型。 许多语言通过以不同的方式着色关键字、分隔符（如括号或大括号）和注释来区分它们。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="implementation"></a>实现
 为了支持着色，托管包框架 （MPF） 包括实现<xref:Microsoft.VisualStudio.Package.Colorizer>接口的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>类。 类与 交互<xref:Microsoft.VisualStudio.Package.IScanner>以确定令牌和颜色。 有关扫描仪的详细信息，请参阅[旧语言服务解析器和扫描仪](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。 然后<xref:Microsoft.VisualStudio.Package.Colorizer>，类使用颜色信息标记令牌的每个字符，并将该信息返回给显示源文件的编辑器。

 返回到编辑器的颜色信息是可着色项列表中的索引。 每个可着色项指定颜色值和一组字体属性，如粗体或粗体。 编辑器提供一组默认的可着色项，语言服务可以使用这些项目。 您只需为每个令牌类型指定适当的颜色索引。 但是，您可以提供一组自定义可着色项和为令牌提供的索引，并引用您自己的可着色项列表，而不是默认列表。 还必须将`RequestStockColors`注册表项设置为 0（或根本不指定`RequestStockColors`该条目）以支持自定义颜色。 您可以使用命名参数将此注册表项设置为<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>用户定义的属性。 有关注册语言服务并设置其选项的详细信息，请参阅[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

## <a name="custom-colorable-items"></a>自定义可着色项
 要提供您自己的自定义可着色项，必须重写<xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A><xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类 上的 和 方法。 第一种方法返回语言服务支持的自定义可着色项数，第二种方法按索引获取自定义可着色项。 创建自定义可着色项的默认列表。 在语言服务的构造函数中，您只需为每个可着色项提供名称。 Visual Studio 会自动处理用户选择一组不同的可着色项目的情况。 此名称是"**选项**"对话框（可从可视化工作室**工具**菜单）上的"**字体和颜色**"属性页中显示的名称，此名称确定用户已覆盖的颜色。 用户的选择存储在注册表中的缓存中，并由颜色名称访问。 **"字体和颜色**"属性页按字母顺序列出所有颜色名称，因此您可以按语言名称在每个颜色名称之前对自定义颜色进行分组;例如，"**测试语言-注释**"和"**测试语言-关键字**"。 或者，您可以按类型对可着色项目进行分组，"**注释（测试语言）"** 和"**关键字（测试语言）"。** 首选按语言名称分组。

> [!CAUTION]
> 强烈建议您在可着色项名称中包括语言名称，以避免与现有可着色项名称发生冲突。

> [!NOTE]
> 如果在开发过程中更改了其中一种颜色的名称，则必须重置 Visual Studio 首次访问颜色时创建的缓存。 您可以通过从可视化 Studio SDK 程序菜单中运行 **"重置实验蜂巢**"命令来执行此操作。

 请注意，永远不会引用可着色项列表中的第一项。 Visual Studio 始终提供该项目的默认文本颜色和属性。 处理此问题的最简单方法是将占位符着色为第一项。

### <a name="high-color-colorable-items"></a>高彩色可着色物品
 可着色项还可以通过<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>界面支持 24 位或高颜色值。 MPF<xref:Microsoft.VisualStudio.Package.ColorableItem>类支持<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>接口，24 位颜色与普通颜色一起在构造函数中指定。 有关更多详细信息，请参见 <xref:Microsoft.VisualStudio.Package.ColorableItem> 类。 下面的示例演示如何为关键字和注释设置 24 位颜色。 当用户的桌面上支持 24 位颜色时，将使用 24 位颜色;否则，将使用普通文本颜色。

 请记住，这些是语言的默认颜色;用户可以将这些颜色更改为所需的任何颜色。

### <a name="example"></a>示例
 此示例显示了使用 类声明和填充自定义可着色项数组的<xref:Microsoft.VisualStudio.Package.ColorableItem>一种方法。 本示例使用 24 位颜色设置关键字和注释颜色。

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

## <a name="the-colorizer-class-and-the-scanner"></a>着色器类和扫描仪
 基<xref:Microsoft.VisualStudio.Package.LanguageService>类具有实例<xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A>化<xref:Microsoft.VisualStudio.Package.Colorizer>类的方法。 从方法返回的<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>扫描程序将传递给<xref:Microsoft.VisualStudio.Package.Colorizer>类构造函数。

 必须在自己的<xref:Microsoft.VisualStudio.Package.LanguageService>类版本中<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>实现该方法。 类<xref:Microsoft.VisualStudio.Package.Colorizer>使用扫描仪获取所有令牌颜色信息。

 扫描仪需要为其找到的每个令牌<xref:Microsoft.VisualStudio.Package.TokenInfo>填充一个结构。 此结构包含诸如令牌占用的跨度、要使用的颜色索引、令牌的类型和令牌触发器（请参阅<xref:Microsoft.VisualStudio.Package.TokenTriggers>）等信息。 <xref:Microsoft.VisualStudio.Package.Colorizer>类着色只需要范围和颜色索引。

 存储在结构中<xref:Microsoft.VisualStudio.Package.TokenInfo>的颜色索引通常是枚举中的值<xref:Microsoft.VisualStudio.Package.TokenColor>，它提供与各种语言元素（如关键字和运算符）对应的命名索引。 如果自定义可着色项列表与枚举中<xref:Microsoft.VisualStudio.Package.TokenColor>显示的项目匹配，则只需将枚举用作每个标记的颜色即可。 但是，如果您有其他可着色项，或者不希望按该顺序使用现有值，则可以排列自定义可着色项列表以满足您的需要，并将相应的索引返回到该列表中。 只需在<xref:Microsoft.VisualStudio.Package.TokenColor><xref:Microsoft.VisualStudio.Package.TokenInfo>结构中存储索引时，请确保将索引转换为[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)]只能看到索引。

### <a name="example"></a>示例
 下面的示例显示了扫描仪如何识别三种令牌类型：数字、标点符号和标识符（任何不是数字或标点符号）。 此示例仅用于说明目的，不表示全面的解析器和扫描仪实现。 它假定有一个`Lexer``GetNextToken()`类，其方法返回字符串。

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
