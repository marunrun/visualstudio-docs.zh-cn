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
ms.openlocfilehash: 19561363affada05154e15142bd32a30a5d051d0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722836"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>旧版语言服务中的语法着色
语法着色是一项功能，它使编程语言的不同元素显示在不同颜色和样式的源文件中。 若要支持此功能，需要提供可在文件中标识词法元素类型或标记的分析器或扫描程序。 许多语言将关键字、分隔符（如圆括号或大括号）与注释着色，并以不同的方式对其进行区分。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="implementation"></a>实现
 为了支持着色，托管包框架（MPF）包含 <xref:Microsoft.VisualStudio.Package.Colorizer> 类，该类实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 此类与 <xref:Microsoft.VisualStudio.Package.IScanner> 进行交互，以确定标记和颜色。 有关扫描仪的详细信息，请参阅[旧版语言服务分析器和扫描仪](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。 然后 <xref:Microsoft.VisualStudio.Package.Colorizer> 类将标记的每个字符标记为颜色信息，并将该信息返回到显示源文件的编辑器中。

 返回到编辑器的颜色信息是可着色项列表中的索引。 每个可着色项指定一个颜色值和一组字体特性，例如粗体或删除线。 编辑器提供您的语言服务可以使用的一组默认可着色项。 只需为每个标记类型指定相应的颜色索引。 但是，你可以提供一组自定义可着色项和你为令牌提供的索引，并引用你自己的可着色项列表，而不是引用默认列表。 还必须将 `RequestStockColors` 注册表项设置为0（或根本不指定 `RequestStockColors` 项）以支持自定义颜色。 可以使用命名参数将此注册表项设置为 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 用户定义的属性。 有关注册语言服务并设置其选项的详细信息，请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

## <a name="custom-colorable-items"></a>自定义可着色项
 若要提供自己的自定义可着色项，必须重写 <xref:Microsoft.VisualStudio.Package.LanguageService> 类的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> 和 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> 方法。 第一种方法返回语言服务支持的自定义可着色项的数量，第二种方法按索引获取自定义可着色项。 创建自定义可着色项的默认列表。 在语言服务的构造函数中，只需为每个可着色项提供一个名称。 Visual Studio 会自动处理用户选择一组不同的可着色项的情况。 此名称显示在 "**选项**" 对话框中的 "**字体和颜色**" 属性页上（可从 Visual Studio "**工具**" 菜单获得），此名称确定用户重写的颜色。 用户的选择存储在注册表的缓存中，并由颜色名称访问。 "**字体和颜色**" 属性页按字母顺序列出所有颜色名称，因此你可以通过将每个颜色名称放在你的语言名称前面来分组自定义颜色;例如，"**TestLanguage**" 和 "**TestLanguage**"。 或者，你可以按 "**注释（TestLanguage）** " 和 "**关键字（TestLanguage）** " 类型对可着色项进行分组。 首选按语言名称进行分组。

> [!CAUTION]
> 强烈建议在可着色项名称中包含语言名称，以避免与现有可着色项名称冲突。

> [!NOTE]
> 如果在开发过程中更改某一种颜色的名称，则必须重置 Visual Studio 在第一次访问颜色时创建的缓存。 若要执行此操作，可从 Visual Studio SDK 程序菜单运行 "**重置实验 Hive"** 命令。

 请注意，从不引用可着色项列表中的第一项。 Visual Studio 始终为该项提供默认文本颜色和特性。 处理此项的最简单方法是提供占位符可着色项作为第一项。

### <a name="high-color-colorable-items"></a>高颜色可着色项
 可着色项还可以通过 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 接口支持24位或高颜色值。 MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> 类支持 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 接口，并在构造函数中指定24位颜色以及正常颜色。 有关更多详细信息，请参见 <xref:Microsoft.VisualStudio.Package.ColorableItem> 类。 下面的示例演示如何为关键字和注释设置24位颜色。 如果用户桌面上支持24位颜色，则使用24位颜色;否则，将使用普通文本颜色。

 请记住，这些是你的语言的默认颜色;用户可以将这些颜色更改为所需的颜色。

### <a name="example"></a>示例
 此示例演示了一种使用 <xref:Microsoft.VisualStudio.Package.ColorableItem> 类声明和填充自定义可着色项数组的方法。 此示例使用24位颜色设置关键字和注释颜色。

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

## <a name="the-colorizer-class-and-the-scanner"></a>Colorizer 类和扫描程序
 Base <xref:Microsoft.VisualStudio.Package.LanguageService> 类具有 instantiantes <xref:Microsoft.VisualStudio.Package.Colorizer> 类的 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> 方法。 从 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法返回的扫描程序将传递到 <xref:Microsoft.VisualStudio.Package.Colorizer> 类构造函数。

 你必须在你自己的 <xref:Microsoft.VisualStudio.Package.LanguageService> 类版本中实现 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法。 @No__t_0 类使用扫描器获取所有令牌颜色信息。

 扫描程序需要为它找到的每个令牌填充 <xref:Microsoft.VisualStudio.Package.TokenInfo> 结构。 此结构包含以下信息：令牌占用范围、要使用的颜色索引、令牌类型和标记触发器（请参阅 <xref:Microsoft.VisualStudio.Package.TokenTriggers>）。 @No__t_0 类只需使用范围和颜色索引进行着色。

 存储在 <xref:Microsoft.VisualStudio.Package.TokenInfo> 结构中的颜色索引通常是 <xref:Microsoft.VisualStudio.Package.TokenColor> 枚举中的一个值，它提供了与各种语言元素（如关键字和运算符）对应的多个命名索引。 如果自定义可着色项列表与 <xref:Microsoft.VisualStudio.Package.TokenColor> 枚举中提供的项相匹配，则可以只使用枚举作为每个标记的颜色。 但是，如果你有其他可着色项，或者你不希望按顺序使用现有值，则可以排列自定义可着色项列表以满足你的需求，并将相应的索引返回到该列表中。 只需确保在将索引存储在 <xref:Microsoft.VisualStudio.Package.TokenInfo> 结构中时，将索引强制转换为 <xref:Microsoft.VisualStudio.Package.TokenColor>; [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] 仅查看索引。

### <a name="example"></a>示例
 下面的示例演示扫描仪如何识别三个标记类型：数字、标点符号和标识符（非数字或标点的任何内容）。 此示例仅用于说明目的，并不表示完整的分析器和扫描程序实现。 它假定存在一个 `Lexer` 类，该类具有返回字符串的 `GetNextToken()` 方法。

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