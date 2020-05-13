---
title: 旧语言服务中的成员完成 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b6445aec4954590e4d361189f053592eebe7767e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707196"
---
# <a name="member-completion-in-a-legacy-language-service"></a>旧版语言服务中的成员完成

IntelliSense 成员完成是一个工具提示，用于显示特定作用域（如类、结构、枚举或命名空间）的可能成员的列表。 例如，在 C# 中，如果用户键入"THIS"后跟句点，则在当前作用域中显示类或结构的所有成员的列表，用户可以从中选择该列表。

托管包框架 （MPF） 支持工具提示和管理工具提示中的列表;只需要解析器提供列表中显示的数据方面的合作。

旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="how-it-works"></a>工作原理

以下是使用 MPF 类显示成员列表的两种方式：

- 将 care 放在标识符或成员完成字符之后，并从**IntelliSense**菜单中选择 **"列表成员**"。

- 扫描仪<xref:Microsoft.VisualStudio.Package.IScanner>检测成员完成字符并设置[令牌触发器](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)的令牌触发器。

成员完成字符指示要遵循类、结构或枚举的成员。 例如，在 C# 或 Visual Basic 中，`.`成员完成字符为 ，而在C++`.`该字符`->`为 或 。 扫描成员选择字符时设置触发器值。

### <a name="the-intellisense-member-list-command"></a>感知成员列表命令

该<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>命令<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>启动对<xref:Microsoft.VisualStudio.Package.Source>类上方法的调用<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>，该方法又使用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>[ParseReason.Display成员列表的](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>)解析原因调用方法解析器。

解析器确定当前位置的上下文以及当前位置下方或紧接于当前位置的令牌。 基于此令牌，将显示声明列表。 例如，在 C# 中，如果将 caret 放置在类成员上并选择 **"列表成员"，** 则获取类所有成员的列表。 如果在对象变量之后的句点之后放置 caret，则获取对象表示的类的所有成员的列表。 请注意，如果在成员列表显示时，该示者位于成员上，则从列表中选择一个成员将该成员替换为列表中的成员。

### <a name="the-token-trigger"></a>令牌触发器

[令牌触发器.成员选择](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>触发器启动对<xref:Microsoft.VisualStudio.Package.Source>类上方法的调用，<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>而方法则使用[ParseReason](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)的解析原因调用解析器。 如果令牌触发器还包括[令牌触发器.MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>)标志，则解析原因是[ParseEE.成员选择和高光，](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)它结合了成员选择和大括号突出显示。

解析器确定当前位置的上下文以及成员选择字符之前键入的内容。 根据此信息，解析器创建请求作用域的所有成员的列表。 此声明列表存储在从<xref:Microsoft.VisualStudio.Package.AuthoringScope><xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法返回的对象中。 如果返回任何声明，将显示成员完成工具提示。 工具提示由<xref:Microsoft.VisualStudio.Package.CompletionSet>类的实例管理。

## <a name="enable-support-for-member-completion"></a>启用对成员完成的支持

您必须将`CodeSense`注册表项设置为 1 以支持任何 IntelliSense 操作。 此注册表项可以使用传递给与语言包关联的用户属性的<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>命名参数进行设置。 语言服务类从<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A><xref:Microsoft.VisualStudio.Package.LanguagePreferences>类的属性中读取此注册表项的值。

如果扫描仪返回[令牌触发器的令牌触发器.成员选择](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)，并且解析器返回声明列表，则会显示成员完成列表。

## <a name="support-member-completion-in-the-scanner"></a>支持扫描仪中的成员完成

扫描程序必须能够检测成员完成字符并设置[令牌触发器](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)的令牌触发器。

### <a name="scanner-example"></a>扫描仪示例

下面是检测成员完成字符和设置相应<xref:Microsoft.VisualStudio.Package.TokenTriggers>标志的简化示例。 此示例仅用于说明目的。 它假定扫描仪包含一个标识和返回`GetNextToken`文本行中的令牌的方法。 示例代码只要看到正确的字符类型，即可设置触发器。

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

## <a name="support-member-completion-in-the-parser"></a>支持 Parser 中的会员完成

对于成员完成，<xref:Microsoft.VisualStudio.Package.Source>类调用<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>方法。 必须在派生自类的<xref:Microsoft.VisualStudio.Package.Declarations>类中实现该列表。 有关必须<xref:Microsoft.VisualStudio.Package.Declarations>实现的方法的详细信息，请参阅 该类。

解析器使用[ParseReason.成员选择](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)或[ParseReason 调用。成员选择和突出显示在](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)成员选择字符键入时。 <xref:Microsoft.VisualStudio.Package.ParseRequest>对象中给出的位置紧接成员选择字符。 解析器必须收集可在源代码中该特定点出现在成员列表中的所有成员的名称。 然后，解析器必须分析当前行以确定用户希望与成员选择字符关联的范围。

此作用域基于成员选择字符之前标识符的类型。 例如，在 C# 中，给定具有`languageService``LanguageService`类型 的成员变量键入**语言服务。** 生成`LanguageService`类的所有成员的列表。 此外，在 C# 中，键入**此。** 生成当前作用域中类的所有成员的列表。

### <a name="parser-example"></a>分析器示例

下面的示例显示了填充列表的一<xref:Microsoft.VisualStudio.Package.Declarations>种方法。 此代码假定解析器构造一个声明，并通过在`AddDeclaration``TestAuthoringScope`类上调用方法将其添加到列表中。

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
