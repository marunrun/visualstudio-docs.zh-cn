---
title: 旧版语言服务中的语法着色 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 64e57ebc80320ccc133261781eb8ee6611c8e2a0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840680"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>旧版语言服务中的语法着色
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

语法着色是一项功能，它使编程语言的不同元素显示在不同颜色和样式的源文件中。 若要支持此功能，需要提供可在文件中标识词法元素类型或标记的分析器或扫描程序。 许多语言将关键字、分隔符 (如圆括号或大括号) 以及注释通过以不同方式着色来区分。  
  
 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。  
  
> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。  
  
## <a name="implementation"></a>实现  
 为了支持着色，托管包框架 (MPF) 包括 <xref:Microsoft.VisualStudio.Package.Colorizer> 实现接口的类 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 。 此类与进行交互 <xref:Microsoft.VisualStudio.Package.IScanner> ，以确定标记和颜色。 有关扫描仪的详细信息，请参阅 [旧版语言服务分析器和扫描仪](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。 <xref:Microsoft.VisualStudio.Package.Colorizer>然后，类将标记的每个字符标记为颜色信息，并将该信息返回到显示源文件的编辑器中。  
  
 返回到编辑器的颜色信息是可着色项列表中的索引。 每个可着色项指定一个颜色值和一组字体特性，例如粗体或删除线。 编辑器提供您的语言服务可以使用的一组默认可着色项。 只需为每个标记类型指定相应的颜色索引。 但是，你可以提供一组自定义可着色项和你为令牌提供的索引，并引用你自己的可着色项列表，而不是引用默认列表。 还必须将 `RequestStockColors` 注册表项设置为 0 (或不要指定 `RequestStockColors` 所有) 中的项以支持自定义颜色。 可以使用命名参数将此注册表项设置为 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 用户定义的属性。 有关注册语言服务并设置其选项的详细信息，请参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。  
  
## <a name="custom-colorable-items"></a>自定义可着色项  
 若要提供自己的自定义可着色项，必须重 <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> 写 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> 类的和方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 。 第一种方法返回语言服务支持的自定义可着色项的数量，第二种方法按索引获取自定义可着色项。 创建自定义可着色项的默认列表。 在语言服务的构造函数中，只需为每个可着色项提供一个名称。 Visual Studio 会自动处理用户选择一组不同的可着色项的情况。 此名称显示在 "**选项**" 对话框中的 "**字体和颜色**" 属性页中， (Visual Studio "**工具**" 菜单中提供) ，此名称确定用户重写的颜色。 用户的选择存储在注册表的缓存中，并由颜色名称访问。 " **字体和颜色** " 属性页按字母顺序列出所有颜色名称，因此你可以通过将每个颜色名称放在你的语言名称前面来分组自定义颜色;例如，"**TestLanguage**" 和 "**TestLanguage**"。 或者，可以按类型 "**Comment (TestLanguage) **" 和 "**关键字 (TestLanguage) **" 对可着色项分组。 首选按语言名称进行分组。  
  
> [!CAUTION]
> 强烈建议在可着色项名称中包含语言名称，以避免与现有可着色项名称冲突。  
  
> [!NOTE]
> 如果在开发过程中更改某一种颜色的名称，则必须重置 Visual Studio 在第一次访问颜色时创建的缓存。 若要执行此操作，可从 Visual Studio SDK 程序菜单运行 " **重置实验 Hive"** 命令。  
  
 请注意，从不引用可着色项列表中的第一项。 Visual Studio 始终为该项提供默认文本颜色和特性。 处理此项的最简单方法是提供占位符可着色项作为第一项。  
  
### <a name="high-color-colorable-items"></a>高颜色可着色项  
 可着色项还可以通过接口支持24位或高颜色值 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 。 MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> 类支持 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 接口，并在构造函数中指定24位颜色以及正常颜色。 有关更多详细信息，请参见 <xref:Microsoft.VisualStudio.Package.ColorableItem> 类。 下面的示例演示如何为关键字和注释设置24位颜色。 如果用户桌面上支持24位颜色，则使用24位颜色;否则，将使用普通文本颜色。  
  
 请记住，这些是你的语言的默认颜色;用户可以将这些颜色更改为所需的颜色。  
  
### <a name="example"></a>示例  
 此示例演示使用类声明和填充自定义可着色项数组的一种方法 <xref:Microsoft.VisualStudio.Package.ColorableItem> 。 此示例使用24位颜色设置关键字和注释颜色。  
  
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
                new ColorableItem("TestLanguage – Text",  
                                  "Text",  
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,  
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,  
                                  System.Drawing.Color.Empty,  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_DEFAULT),  
                new ColorableItem("TestLanguage – Keyword",  
                                  "Keyword",  
                                  COLORINDEX.CI_MAROON,  
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,  
                                  System.Drawing.Color.FromArgb(192,32,32),  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_BOLD),  
                new ColorableItem("TestLanguage – Comment",  
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
 基类 <xref:Microsoft.VisualStudio.Package.LanguageService> 具有 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> instantiantes 类的方法 <xref:Microsoft.VisualStudio.Package.Colorizer> 。 从方法返回的扫描程序 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 将传递给 <xref:Microsoft.VisualStudio.Package.Colorizer> 类构造函数。  
  
 你必须 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 在自己的类版本中实现方法 <xref:Microsoft.VisualStudio.Package.LanguageService> 。 <xref:Microsoft.VisualStudio.Package.Colorizer>类使用扫描器获取所有令牌颜色信息。  
  
 扫描程序需要为 <xref:Microsoft.VisualStudio.Package.TokenInfo> 它找到的每个令牌填充结构。 此结构包含诸如令牌占用范围、要使用的颜色索引、令牌类型以及令牌触发器 (参阅) 的信息 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 。 类只需使用范围和颜色索引进行着色 <xref:Microsoft.VisualStudio.Package.Colorizer> 。  
  
 结构中存储的颜色索引 <xref:Microsoft.VisualStudio.Package.TokenInfo> 通常是枚举中的一个值 <xref:Microsoft.VisualStudio.Package.TokenColor> ，它提供了与各种语言元素（如关键字和运算符）对应的多个命名索引。 如果自定义可着色项列表与枚举中显示的项相匹配 <xref:Microsoft.VisualStudio.Package.TokenColor> ，则可以只使用枚举作为每个标记的颜色。 但是，如果你有其他可着色项，或者你不希望按顺序使用现有值，则可以排列自定义可着色项列表以满足你的需求，并将相应的索引返回到该列表中。 在将索引存储到结构中时，只需确保将索引强制转换为， <xref:Microsoft.VisualStudio.Package.TokenColor> <xref:Microsoft.VisualStudio.Package.TokenInfo> 只会 [!INCLUDE[vs_current_short](../../includes/vs-current-short-md.md)] 看到索引。  
  
### <a name="example"></a>示例  
 下面的示例演示扫描仪如何识别三个令牌类型：数字、标点和标识符 (不是数字或标点) 的任何内容。 此示例仅用于说明目的，并不表示完整的分析器和扫描程序实现。 它假定存在一个 `Lexer` 具有 `GetNextToken()` 返回字符串的方法的类。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)   
 [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)   
 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
