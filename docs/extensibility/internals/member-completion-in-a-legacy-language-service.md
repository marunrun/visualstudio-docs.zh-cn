---
title: 旧版语言服务中的成员完成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2c969b0f857e45279488d9ba667b431064375da6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349311"
---
# <a name="member-completion-in-a-legacy-language-service"></a>旧版语言服务中的成员完成

IntelliSense 成员完成是工具提示显示特定的作用域，如类、 结构、 枚举或命名空间的可能的成员的列表。 例如，在 C# 中，如果用户键入"this"后, 跟一个句点，类或结构在当前范围内的所有成员的列表所示，用户可以从中选择的列表。

托管的包框架 (MPF) 提供的工具提示和管理的列表中的工具提示; 支持只需是来自分析器提供显示在列表中的数据的协作正常进行。

旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="how-it-works"></a>其工作原理

以下是中的成员列表中均显示使用 MPF 类的两种方法：

- 定位的标识符上或成员完成字符后面插入符号并选择**成员列表**从**IntelliSense**菜单。

- <xref:Microsoft.VisualStudio.Package.IScanner>扫描程序检测到的成员完成字符和设置的令牌触发器[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) ，该字符。

成员完成字符表示的类、 结构或枚举成员遵循。 例如，在C#或 Visual Basic 的成员完成字符`.`，在C++字符可以是`.`或`->`。 触发器值的成员选择字符扫描时设置。

### <a name="the-intellisense-member-list-command"></a>IntelliSense 成员 List 命令

<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>命令启动对的调用<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>方法<xref:Microsoft.VisualStudio.Package.Source>类和<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>方法，都依次调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法分析器分析原因为[ParseReason.DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>).

分析器确定当前的位置，以及下或当前位置之前的令牌的上下文。 根据此令牌，显示声明的列表。 例如，在 C# 中，如果定位在某个类成员并选择将插入符号**列出成员**，获取类的所有成员的列表。 遵循对象变量一段时间后将插入符号，可以获取类的对象所表示的所有成员的列表。 请注意，是否显示成员列表时，将插入符号定位在成员上，从列表中选择成员替代插入点位于其中一个列表中的成员。

### <a name="the-token-trigger"></a>令牌的触发器

[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)触发器开始调用<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>方法<xref:Microsoft.VisualStudio.Package.Source>类并<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>方法，都依次调用分析原因为分析器[ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)。 如果还包含令牌的触发器[TokenTriggers.MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>)标志，分析原因是[ParseReason.MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)，此功能结合了成员选择和大括号突出显示.

分析器确定当前的上下文位置及成员选择字符之前具有已键入内容。 中的信息，分析器创建请求的作用域的所有成员的列表。 声明此列表存储在<xref:Microsoft.VisualStudio.Package.AuthoringScope>从返回的对象<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法。 如果返回的任何声明，则显示成员完成工具提示。 由的实例管理的工具提示<xref:Microsoft.VisualStudio.Package.CompletionSet>类。

## <a name="enable-support-for-member-completion"></a>支持的成员完成

您必须具有`CodeSense`注册表项设置为 1 以支持 IntelliSense 中的任何操作。 此注册表项可以设置使用命名参数传递给<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>与语言包相关联的用户属性。 语言服务类读取从此注册表项的值<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>属性上的<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。

如果您的扫描仪返回的令牌触发器[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)，和您的分析程序返回一组声明，则显示成员的完成列表。

## <a name="support-member-completion-in-the-scanner"></a>在扫描程序中支持的成员完成

扫描程序必须能够检测成员完成字符并设置令牌的触发器[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)时分析该字符。

### <a name="scanner-example"></a>扫描程序示例

下面是检测成员完成字符并设置适当的简化的示例<xref:Microsoft.VisualStudio.Package.TokenTriggers>标志。 此示例是仅供说明用途。 它假定您的扫描仪，包含一种方法`GetNextToken`的标识，并返回从文本行的令牌。 示例代码只需设置触发器，只要它发现正确类型的字符。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char memberSelectChar = '.';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (c == memberSelectChar)
                {
                        tokenInfo.Trigger |= TokenTriggers.MemberSelect;
                }
            }
            return foundToken;
        }
    }
}
```

## <a name="support-member-completion-in-the-parser"></a>在分析器中支持的成员完成

成员完成情况<xref:Microsoft.VisualStudio.Package.Source>类调用<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>方法。 必须在从派生类中实现列表<xref:Microsoft.VisualStudio.Package.Declarations>类。 请参阅<xref:Microsoft.VisualStudio.Package.Declarations>类必须实现的方法的详细信息。

使用调用分析器[ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)或[ParseReason.MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)时键入成员选择字符。 给定的位置<xref:Microsoft.VisualStudio.Package.ParseRequest>对象是紧跟在成员选择字符。 分析器必须收集可以出现在源代码中该特定点的成员列表中的所有成员的名称。 然后分析器必须分析以确定用户想要与成员选择字符相关联的作用域的当前行。

此作用域基于标识符的类型成员选择字符之前。 例如，在 C# 中，给定成员变量`languageService`具有一种`LanguageService`，键入**languageService。** 生成的所有成员的列表`LanguageService`类。 此外在 C# 中，键入**这。** 生成的当前作用域中的类的所有成员的列表。

### <a name="parser-example"></a>分析器示例

下面的示例演示一种方法来填充<xref:Microsoft.VisualStudio.Package.Declarations>列表。 此代码假定分析器构造声明并将其添加到列表，通过调用`AddDeclaration`方法`TestAuthoringScope`类。

```csharp
using System.Collections;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclaration
    {
        public string Name;            // Name of declaration
        public int     TypeImageIndex; // Glyph index
        public string Description;     // Description of declaration

        public TestDeclaration(string name, int typeImageIndex, string description)
        {
            this.Name = name;
            this.TypeImageIndex = typeImageIndex;
            this.Description = description;
        }
    }

    //===================================================
    internal class TestDeclarations : Declarations
    {
        private ArrayList declarations;

        public TestDeclarations()
            : base()
        {
            declarations = new ArrayList();
        }

        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        //////////////////////////////////////////////////////////////////////
        // Declarations of class methods that must be implemented.
        public override int GetCount()
        {
            // Return the number of declarations to show.
            return declarations.Count;
        }

        public override string GetDescription(int index)
        {
            // Return the description of the specified item.
            string description = "";
            if (index >= 0 && index < declarations.Count)
            {
                description = ((TestDeclaration)declarations[index]).Description;
            }
            return description;
        }

        public override string GetDisplayText(int index)
        {
            // Determine what is displayed in the tool tip list.
            string text = null;
            if (index >= 0 && index < declarations.Count)
            {
                text = ((TestDeclaration)declarations[index]).Name;
            }
            return text;
        }

        public override int GetGlyph(int index)
        {
            // Return index of image to display next to the display text.
            int imageIndex = -1;
            if (index >= 0 && index < declarations.Count)
            {
                imageIndex = ((TestDeclaration)declarations[index]).TypeImageIndex;
            }
            return imageIndex;
        }

        public override string GetName(int index)
        {
            string name = null;
            if (index >= 0 && index < declarations.Count)
            {
                name = ((TestDeclaration)declarations[index]).Name;
            }
            return name;
        }
    }

    //===================================================
    public class TestAuthoringScope : AuthoringScope
    {
        private TestDeclarations declarationsList;

        public void AddDeclaration(TestDeclaration declaration)
        {
            if (declaration != null)
            {
                if (declarationsList == null)
                {
                    declarationsList = new TestDeclarations();
                }
                declarationsList.AddDeclaration(declaration);
            }
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return declarationsList;
        }

        /////////////////////////////////////////////////
        // Remainder of AuthoringScope methods not shown.
        /////////////////////////////////////////////////
    }

    //===================================================
    class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            TestAuthoringScope scope = new TestAuthoringScope();
            if (req.Reason == ParseReason.MemberSelect ||
                req.Reason == ParseReason.MemberSelectAndHighlightBraces)
            {
                // Gather list of declarations based on what the user
                // has typed so far. In this example, this list is an array of
                // MemberDeclaration objects (a helper class you might implement
                // to hold member declarations).
                // How this list is gathered is dependent on the parser
                // and is not shown here.
                MemberDeclarations memberDeclarations;
                memberDeclarations = GetDeclarationsForScope();

                // Now populate the Declarations list in the authoring scope.
                // GetImageIndexBasedOnType() is a helper method you
                // might implement to convert a member type to an index into
                // the image list returned from the language service.
                foreach (MemberDeclaration dec in memberDeclarations)
                {
                    scope.AddDeclaration(new TestDeclaration(
                                             dec.Name,
                                             GetImageIndexBasedOnType(dec.Type),
                                             dec.Description));
                }
            }
            return scope;
        }
    }
}
```