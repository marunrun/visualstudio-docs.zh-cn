---
title: 支持旧语言服务中的代码段 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad871eb73341f6ab87229687e2a6df898ffda32d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704911"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>旧版语言服务中的代码片段支持
代码段是插入到源文件中的代码段。 代码段本身是一个基于 XML 的模板，包含一组字段。 这些字段在插入代码段后突出显示，并根据插入代码段的上下文的不同值。 插入代码段后，语言服务可以立即格式化代码段。

 代码段插入到特殊的编辑模式，允许使用 TAB 键导航代码段的字段。 这些字段可以支持 IntelliSense 风格的下拉菜单。 用户通过键入 ENTER 或 ESC 密钥将代码段提交到源文件。 要了解有关代码段的更多，请参阅[代码段](../../ide/code-snippets.md)。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[演练：实现代码代码段](../../extensibility/walkthrough-implementing-code-snippets.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="managed-package-framework-support-for-code-snippets"></a>代码段的托管包框架支持
 托管包框架 （MPF） 支持大多数代码段功能，从读取模板到插入代码段和启用特殊编辑模式。 支持通过类<xref:Microsoft.VisualStudio.Package.ExpansionProvider>进行管理。

 实例化<xref:Microsoft.VisualStudio.Package.Source>类时，将调用<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法以获取对象<xref:Microsoft.VisualStudio.Package.ExpansionProvider>（请注意，基<xref:Microsoft.VisualStudio.Package.LanguageService>类始终为每个<xref:Microsoft.VisualStudio.Package.ExpansionProvider><xref:Microsoft.VisualStudio.Package.Source>对象返回一个新对象）。

 MPF 不支持扩展功能。 扩展函数是嵌入在代码段模板中的命名函数，并返回要放置在字段中的一个或多个值。 这些值由语言服务本身通过<xref:Microsoft.VisualStudio.Package.ExpansionFunction>对象返回。 该<xref:Microsoft.VisualStudio.Package.ExpansionFunction>对象必须由语言服务实现以支持扩展函数。

## <a name="providing-support-for-code-snippets"></a>支持代码段
 若要启用对代码段的支持，必须提供或安装代码段，并且必须为用户提供插入这些代码段的方法。 支持代码段有三个步骤：

1. 安装代码段文件。

2. 为您的语言服务启用代码段。

3. 调用对象<xref:Microsoft.VisualStudio.Package.ExpansionProvider>。

### <a name="installing-the-snippet-files"></a>安装代码段文件
 语言的所有代码段都存储在 XML 文件中的模板中，通常每个文件一个代码段模板。 有关用于代码段模板的 XML 架构的详细信息，请参阅[代码段架构参考](../../ide/code-snippets-schema-reference.md)。 每个代码段模板都使用语言 ID 标识。 此语言 ID 在注册表中指定，并放入模板`Language`中\<代码>标记的属性中。

 存储代码段模板文件的通常有两个位置：1） 安装语言的位置和 2） 在用户的文件夹中。 这些位置将添加到注册表中，以便可视化工作室**代码代码段管理器**可以找到代码段。 用户的文件夹是存储用户创建的代码段的位置。

 已安装的代码段模板文件的典型文件夹布局如下所示 *：[安装Root]*\\ *[测试语言]*[代码段\\ *[LCID]*[片段。

 *[安装Root]* 是您的语言安装的文件夹。

 *[测试语言]* 是您的语言的名称作为文件夹名称。

 *[LCID]* 是区域设置 ID。 这是存储代码段的本地化版本的方式。 例如，英语区域设置 ID 为 1033，因此 *[LCID]* 替换为 1033。

 必须提供一个附加文件，该文件是索引文件，通常称为 SnippetsIndex.xml 或扩展索引.xml（您可以使用以 .xml 结尾的任何有效文件名）。 此文件通常存储在 *[InstallRoot]*\\ *[Test语言]* 文件夹中，并指定代码段文件夹的确切位置以及使用代码段的语言服务的语言 ID 和 GUID。 索引文件的确切路径被放入注册表中，如后面的"安装注册表条目"中所述。 下面是 SnippetsIndex.xml 文件的示例：

```
<?xml version="1.0" encoding="utf-8" ?>
<SnippetCollection>
    <Language Lang="Testlanguage" Guid="{b614a40a-80d9-4fac-a6ad-fc2868fff7cd}">
        <SnippetDir>
            <OnOff>On</OnOff>
            <Installed>true</Installed>
            <Locale>1033</Locale>
            <DirPath>%InstallRoot%\TestLanguage\Snippets\%LCID%\Snippets\</DirPath>
            <LocalizedName>Snippets</LocalizedName>
        </SnippetDir>
    </Language>
</SnippetCollection>
```

 语言\<>标记指定语言 ID（`Lang`属性）和语言服务 GUID。

 本示例假定您已在 Visual Studio 安装文件夹中安装了语言服务。 %LCID% 替换为用户的当前区域设置 ID。 可以\<添加多个代码段>标记，每个不同的目录和区域设置一个。 此外，代码段文件夹可以包含子文件夹，每个子文件夹都标识在索引文件中，其中包含嵌入在\<\<代码段>标记中的 SnippetSubDir> 标记。

 用户还可以为您的语言创建自己的代码段。 这些代码通常存储在用户的设置文件夹中，例如 *[TestDocs]*[代码代码段\\ *]测试语言][* 测试代码代码片段]，其中 *[TestDocs]* 是可视化工作室的用户设置文件夹的位置。

 以下替换元素可以放置在索引文件中\<的 DirPath> 标记中存储的路径中。

|元素|描述|
|-------------|-----------------|
|%LCID%|区域设置 ID。|
|%安装根百分比|Visual Studio 的根安装文件夹，例如，C：*程序文件\微软可视化工作室 8。|
|%赞成率|包含当前项目的文件夹。|
|%ProjItem%|包含当前项目项的文件夹。|
|%测试文档百分比|用户设置文件夹中的文件夹，例如，C：\文档和设置\\ *[用户名]*[我的文档]可视化工作室\8。|

### <a name="enabling-code-snippets-for-your-language-service"></a>为您的语言服务启用代码段
 您可以通过将<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>属性添加到 VSPackage 来启用语言服务的代码段（有关详细信息，请参阅[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)）。 和<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A><xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A>参数是可选的，但应包含`SearchPaths`命名参数，以便通知**代码段管理器**代码段代码段的位置。

 以下是如何使用此属性的示例：

```
[ProvideLanguageCodeExpansion(
         typeof(TestSnippetLanguageService),
         "Test Snippet Language",          // Name of language used as registry key
         0,                               // Resource ID of localized name of language service
         "Test Snippet Language",        // Name of Language attribute in snippet template
         @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\SnippetsIndex.xml",  // Path to snippets index
         SearchPaths = @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\")]    // Path to snippets
```

### <a name="calling-the-expansion-provider"></a>调用扩展提供程序
 语言服务控制任何代码段的插入，以及调用插入的方式。

## <a name="calling-the-expansion-provider-for-code-snippets"></a>调用代码段的扩展提供程序
 有两种方法可以调用扩展提供程序：通过使用菜单命令或使用完成列表中的快捷方式。

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>使用菜单命令插入代码段
 要使用菜单命令显示代码段浏览器，请添加菜单命令，然后在<xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A><xref:Microsoft.VisualStudio.Package.ExpansionProvider>界面中调用 方法以响应该菜单命令。

1. 向 .vsct 文件添加命令和按钮。 您可以在[使用菜单命令创建扩展](../../extensibility/creating-an-extension-with-a-menu-command.md)时找到执行此操作的说明。

2. 从<xref:Microsoft.VisualStudio.Package.ViewFilter>类派生类并重写<xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A>方法以指示对新菜单命令的支持。 此示例始终启用菜单命令。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public TestViewFilter(CodeWindowManager mgr, IVsTextView view)
                : base(mgr, view)
            {
            }

            protected override int QueryCommandStatus(ref Guid guidCmdGroup,
                                                      uint nCmdId)
            {
                int hr = base.QueryCommandStatus(ref guidCmdGroup, nCmdId);
                // If the base class did not recognize the command then
                // see if we can handle the command.
                if (hr == (int)Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP)
                {
                    if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                    {
                        if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                        {
                            hr = (int)(OLECMDF.OLECMDF_SUPPORTED | OLECMDF.OLECMDF_ENABLED);
                        }
                    }
                }
                return hr;
            }
        }
    }
    ```

3. 重写类<xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A>中<xref:Microsoft.VisualStudio.Package.ViewFilter>的方法以获取<xref:Microsoft.VisualStudio.Package.ExpansionProvider>该对象，并调用该对象上<xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A>的方法。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public override bool HandlePreExec(ref Guid guidCmdGroup,
                                               uint nCmdId,
                                               uint nCmdexecopt,
                                               IntPtr pvaIn,
                                               IntPtr pvaOut)
            {
                if (base.HandlePreExec(ref guidCmdGroup,
                                       nCmdId,
                                       nCmdexecopt,
                                       pvaIn,
                                       pvaOut))
                {
                    // Base class handled the command.  Do nothing more here.
                    return true;
                }

                if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                {
                    if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                    {
                        ExpansionProvider ep = this.GetExpansionProvider();
                        if (this.TextView != null && ep != null)
                        {
                            bool bDisplayed = ep.DisplayExpansionBrowser(
                                this.TextView,
                                "TestLanguagePackage Snippet:",
                                null,
                                false,
                                null,
                                false);
                        }
                        return true;   // Handled the command.
                    }
                }
                return false;   // Did not handle the command.
            }
        }
    }

    ```

     在插入代码段的过程中<xref:Microsoft.VisualStudio.Package.ExpansionProvider>，Visual Studio 按给定的顺序调用类中的以下方法：

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     调用<xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>方法后，已插入代码段，<xref:Microsoft.VisualStudio.Package.ExpansionProvider>并且对象处于用于修改刚刚插入的代码段的特殊编辑模式。

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>使用快捷方式插入代码段
 从完成列表中实现快捷方式比实现菜单命令要涉及得多。 您必须首先将代码段快捷方式添加到 IntelliSense 单词完成列表中。 然后，您必须检测何时由于完成而插入了代码段快捷方式名称。 最后，您必须使用快捷方式名称获取代码段标题和路径，并将该信息传递给<xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A><xref:Microsoft.VisualStudio.Package.ExpansionProvider>方法上的方法。

 要将代码段快捷方式添加到单词完成列表中，请将它们添加到<xref:Microsoft.VisualStudio.Package.Declarations><xref:Microsoft.VisualStudio.Package.AuthoringScope>类中的对象。 您必须确保可以将快捷方式标识为代码段名称。 例如，请参阅[演练：获取已安装的代码段列表（旧版实现）。](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 可以检测类<xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A>方法中的代码段快捷方式的<xref:Microsoft.VisualStudio.Package.Declarations>插入。 由于代码段名称已插入到源文件中，因此在插入扩展时必须将其删除。 该方法<xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A>采用一个范围来描述代码段的插入点;如果范围包含源文件中的整个代码段名称，则该名称将被代码段替换。

 下面是一个<xref:Microsoft.VisualStudio.Package.Declarations>类的版本，该类处理具有快捷方式名称的代码段插入。 为了清楚起见，<xref:Microsoft.VisualStudio.Package.Declarations>省略了类中的其他方法。 请注意，此类的构造函数采用对象<xref:Microsoft.VisualStudio.Package.LanguageService>。 这可以从<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象的版本传入（例如，<xref:Microsoft.VisualStudio.Package.AuthoringScope>类的实现可能会在其构造函数中获取<xref:Microsoft.VisualStudio.Package.LanguageService>对象并将该对象传递给类`TestDeclarations`构造函数）。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclarations : Declarations
    {
        private ArrayList       declarations;
        private LanguageService languageService;
        private TextSpan        commitSpan;

        public TestDeclarations(LanguageService langService)
            : base()
        {
            languageService = langService;
            declarations = new ArrayList();
        }

        // This method is used to add declarations to the internal list.
        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        // This method is called to get the string to commit to the source buffer.
        // Note that the initial extent is only what the user has typed so far.
        public override string OnCommit(IVsTextView textView,
                                        string textSoFar,
                                        char commitCharacter,
                                        int index,
                                        ref TextSpan initialExtent)
        {
            // We intercept this call only to get the initial extent
            // of what was committed to the source buffer.
            commitSpan = initialExtent;

            return base.OnCommit(textView,
                                 textSoFar,
                                 commitCharacter,
                                 index,
                                 ref initialExtent);
        }

        // This method is called after the string has been committed to the source buffer.
        public override char OnAutoComplete(IVsTextView textView,
                                            string committedText,
                                            char commitCharacter,
                                            int index)
        {
            TestDeclaration item = declarations[index] as TestDeclaration;
            if (item != null)
            {
                // In this example, TestDeclaration identifies types with a string.
                // You can choose a different approach.
                if (item.Type == "snippet")
                {
                    Source src = languageService.GetSource(textView);
                    if (src != null)
                    {
                        ExpansionProvider ep = src.GetExpansionProvider();
                        if (ep != null)
                        {
                            string title;
                            string path;
                            int commitLength = commitSpan.iEndIndex - commitSpan.iStartIndex;
                            if (commitLength < committedText.Length)
                            {
                                // Replace everything that was inserted
                                // so calculate the span of the full
                                // insertion, taking into account what
                                // was inserted when the commitSpan
                                // was obtained in the first place.
                                commitSpan.iEndIndex += (committedText.Length - commitLength);
                            }

                            if (ep.FindExpansionByShortcut(textView,
                                                           committedText,
                                                           commitSpan,
                                                           true,
                                                           out title,
                                                           out path))
                            {
                                ep.InsertNamedExpansion(textView,
                                                        title,
                                                        path,
                                                        commitSpan,
                                                        false);
                            }
                        }
                    }
                }
            }
            return '\0';
        }
    }
}
```

 当语言服务获取快捷方式名称时，它将调用<xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A>方法以获取文件名和代码段标题。 然后，<xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A>语言服务在<xref:Microsoft.VisualStudio.Package.ExpansionProvider>类中调用 方法以插入代码段。 在插入代码段的过程中，Visual <xref:Microsoft.VisualStudio.Package.ExpansionProvider> Studio 在类中的给定顺序调用了以下方法：

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   有关获取语言服务已安装的代码段列表的详细信息，请参阅[演练：获取已安装的代码段列表（旧版实现）。](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

## <a name="implementing-the-expansionfunction-class"></a>实现扩展功能类
 扩展函数是嵌入在代码段模板中的命名函数，并返回要放置在字段中的一个或多个值。 为了支持语言服务中的扩展函数，必须从<xref:Microsoft.VisualStudio.Package.ExpansionFunction>类派生一个类并实现方法。 <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> 然后，<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>必须重写类中<xref:Microsoft.VisualStudio.Package.LanguageService>的方法，以便返回对所支持的每个扩展函数的<xref:Microsoft.VisualStudio.Package.ExpansionFunction>类版本的新实例化。 如果支持扩展函数中可能的值列表，则还必须重写<xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A><xref:Microsoft.VisualStudio.Package.ExpansionFunction>类中的方法以返回这些值的列表。

 获取参数或需要访问其他字段的扩展函数不应与可编辑字段关联，因为在调用扩展函数时，扩展提供程序可能无法完全初始化。 因此，扩展函数无法获得其参数或任何其他字段的值。

### <a name="example"></a>示例
 下面是如何实现称为`GetName`的简单扩展函数的示例。 每次实例化扩展函数时，此扩展函数都会将一个数字追加到基类名称（这与每次插入关联的代码段时都对应）。

```csharp
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private int classNameCounter = 0;

        public override ExpansionFunction CreateExpansionFunction(
            ExpansionProvider provider,
            string functionName)
        {
            ExpansionFunction function = null;
            if (functionName == "GetName")
            {
                ++classNameCounter;
                function = new TestGetNameExpansionFunction(provider, classNameCounter);
            }
            return function;
        }
    }

    internal class TestGetNameExpansionFunction : ExpansionFunction
    {
        private int nameCount;

        TestGetNameExpansionFunction(ExpansionProvider provider, int counter)
            : base(provider)
        {
            nameCount = counter;
        }

        public override string GetCurrentValue()
        {
            string name = "TestClass";
            name += nameCount.ToString();
            return name;
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [代码段](../../ide/code-snippets.md)
- [演练：获取安装代码片段（旧版实现）的列表](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)
