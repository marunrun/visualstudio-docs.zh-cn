---
title: 实现旧版语言 Service2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: df44b92cdf311689397a062b127d4c3e514a15e6
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238694"
---
# <a name="implementing-a-legacy-language-service-2"></a>实现旧版语言服务2
若要使用托管包框架 (MPF) 实现语言服务，必须从类派生一个类 <xref:Microsoft.VisualStudio.Package.LanguageService> ，并实现以下抽象方法和属性：

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> 属性

  有关实现这些方法和属性的详细信息，请参阅以下相应部分。

  若要支持其他功能，语言服务可能必须从一个 MPF 语言服务类派生一个类;例如，若要支持其他菜单命令，你必须从类派生一个类 <xref:Microsoft.VisualStudio.Package.ViewFilter> 并重写几个命令处理方法 (参阅 <xref:Microsoft.VisualStudio.Package.ViewFilter> 获取详细信息) 。 <xref:Microsoft.VisualStudio.Package.LanguageService>类提供了许多方法，这些方法可用于创建各种类的新实例，并重写适当的创建方法来提供类的实例。 例如，你需要重写 <xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A> 类中的方法， <xref:Microsoft.VisualStudio.Package.LanguageService> 以返回你自己的类的实例 <xref:Microsoft.VisualStudio.Package.ViewFilter> 。 有关更多详细信息，请参阅 "实例化自定义类" 一节。

  你的语言服务还可以提供自己的图标，这些图标在多个位置使用。 例如，当显示 IntelliSense 完成列表时，列表中的每一项都可以有与之关联的图标，将项标记为方法、类、命名空间、属性或语言所需的任何内容。 这些图标在所有 IntelliSense 列表、 **导航栏**和 " **错误列表** 任务" 窗口中使用。 有关详细信息，请参阅下面的 "语言服务映像" 部分。

## <a name="getlanguagepreferences-method"></a>GetLanguagePreferences 方法
 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>方法始终返回类的同一实例 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。 <xref:Microsoft.VisualStudio.Package.LanguagePreferences>如果你不需要语言服务的任何其他首选项，则可以使用基类。 MPF 语言服务类假定至少存在基类 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。

### <a name="example"></a>示例
 此示例演示方法的典型实现 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 。 此示例使用基类 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(TestLanguageService).GUID,
                                                        this.Name );
                m_preferences.Init();
            }
            return m_preferences;
        }
    }
}
```

## <a name="getscanner-method"></a>GetScanner 方法
 此方法返回一个 <xref:Microsoft.VisualStudio.Package.IScanner> 对象的实例，该实例实现用于获取令牌及其类型和触发器的面向行的分析器或扫描仪。 此扫描程序在类中用于 <xref:Microsoft.VisualStudio.Package.Colorizer> 着色，不过也可以使用扫描程序以 prelude 的方式获取令牌类型和触发器，以便进行更复杂的分析操作。 您必须提供实现接口的类 <xref:Microsoft.VisualStudio.Package.IScanner> ，并且必须实现该接口上的所有方法 <xref:Microsoft.VisualStudio.Package.IScanner> 。

### <a name="example"></a>示例
 此示例演示方法的典型实现 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 。 `TestScanner`类实现接口， <xref:Microsoft.VisualStudio.Package.IScanner> (未显示) 。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private TestScanner m_scanner;

        public override IScanner GetScanner(IVsTextLines buffer)
        {
            if (m_scanner == null)
            {
                m_scanner = new TestScanner(buffer);
            }
            return m_scanner;
        }
    }
}
    internal class TestScanner : IScanner
    {
        private IVsTextBuffer m_buffer;
        string m_source;

        public TestScanner(IVsTextBuffer buffer)
        {
            m_buffer = buffer;
        }

        bool IScanner.ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo, ref int state)
        {
            tokenInfo.Type = TokenType.Unknown;
            tokenInfo.Color = TokenColor.Text;
            return true;
        }

        void IScanner.SetSource(string source, int offset)
        {
            m_source = source.Substring(offset);
        }
    }

```

## <a name="parsesource-method"></a>ParseSource 方法
 根据许多不同的原因分析源文件。 此方法提供一个 <xref:Microsoft.VisualStudio.Package.ParseRequest> 对象，该对象描述特定分析操作所需的内容。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法调用更复杂的分析器来确定令牌功能和范围。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法用于支持 IntelliSense 操作和大括号匹配。 即使你不支持此类高级操作，你仍必须返回有效 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 的对象，并且需要你创建实现接口的类 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 并在该接口上实现所有方法。 你可以从所有方法返回 null 值，但 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象本身不能为 null 值。

### <a name="example"></a>示例
 此示例演示方法和类的最小实现 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope> ，足以允许语言服务编译和运行，而无需实际支持任何更高级的功能。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            return new TestAuthoringScope();
        }
    }

    internal class TestAuthoringScope : AuthoringScope
    {
        public override string GetDataTipText(int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return null;
        }

        public override string Goto(VSConstants.VSStd97CmdID cmd, IVsTextView textView, int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Methods GetMethods(int line, int col, string name)
        {
            return null;
        }
}
```

## <a name="name-property"></a>Name 属性
 此属性将返回语言服务的名称。 此名称必须与注册语言服务时给定的名称相同。 此名称用于多个位置，最重要的地方是 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 用于访问注册表的类。 此属性返回的名称不能进行本地化，因为它用于注册表项和键名称。

### <a name="example"></a>示例
 此示例显示了属性的一个可能的实现 <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> 。 请注意，此处的名称是硬编码的：实际名称应从资源文件获取，以便它可用于注册语言服务 (参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)) 。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override string Name
        {
            get { return "Test Language"; }
        }
    }
}
```

## <a name="instantiating-custom-classes"></a>实例化自定义类
 可以重写指定类中的以下方法，以提供您自己版本的每个类的实例。

### <a name="in-the-languageservice-class"></a>在 LanguageService 类中

|方法|返回的类|说明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|支持对文本视图进行自定义添加。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|支持自定义文档属性。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|支持 **导航栏**。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|支持代码段模板中的函数。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|若要支持代码片段 (通常不会重写此方法) 。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|为支持自定义 <xref:Microsoft.VisualStudio.Package.ParseRequest> 结构 (通常不会) 重写此方法。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|若为，则支持设置源代码的格式、指定注释字符和自定义方法签名。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|支持其他菜单命令。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|若要支持语法突出显示 (通常不会重写此方法) 。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|支持对语言首选项的访问。 必须实现此方法，但可以返回基类的实例。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|提供用于标识行中的标记类型的分析器。 此方法必须实现，并且 <xref:Microsoft.VisualStudio.Package.IScanner> 必须派生自。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|提供用于在整个源文件中标识功能和范围的分析器。 此方法必须实现，并且必须返回类版本的实例 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 。 如果要支持的所有内容都是语法突出显示 (需要 <xref:Microsoft.VisualStudio.Package.IScanner> 从方法) 返回的分析器 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> ，则除了返回类的版本，而不是返回 <xref:Microsoft.VisualStudio.Package.AuthoringScope> null 值。|

### <a name="in-the-source-class"></a>在源类中

|方法|返回的类|说明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|为了自定义 IntelliSense 完成列表的显示 (通常不会) 重写此方法。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|错误列表任务列表中的支持标记;具体而言，支持除打开文件并跳转到导致错误的行以外的功能。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|用于自定义 IntelliSense 参数信息工具提示的显示。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|用于支持注释代码。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|用于在分析操作过程中收集信息。|

### <a name="in-the-authoringscope-class"></a>在 AuthoringScope 类中

|方法|返回的类|说明|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|提供一个声明列表，如成员或类型。 必须实现此方法，但可以返回 null 值。 如果此方法返回有效的对象，则该对象必须是您的类版本的实例 <xref:Microsoft.VisualStudio.Package.Declarations> 。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|提供给定上下文的方法签名列表。 必须实现此方法，但可以返回 null 值。 如果此方法返回有效的对象，则该对象必须是您的类版本的实例 <xref:Microsoft.VisualStudio.Package.Methods> 。|

## <a name="language-service-images"></a>语言服务映像
 若要提供要在整个语言服务中使用的图标列表，请重写 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> 类中的方法， <xref:Microsoft.VisualStudio.Package.LanguageService> 并返回 <xref:System.Windows.Forms.ImageList> 包含图标的。 基类 <xref:Microsoft.VisualStudio.Package.LanguageService> 加载默认的图标集。 由于在需要图标的地方指定了精确的图像索引，因此如何排列自己的图像列表完全取决于你。

### <a name="images-used-in-intellisense-completion-lists"></a>IntelliSense 完成列表中使用的图像
 对于 IntelliSense 完成列表，为类的方法中的每个项指定了图像索引 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> <xref:Microsoft.VisualStudio.Package.Declarations> ，若要提供图像索引，必须重写此索引。 从方法返回的值 <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> 是提供给类构造函数的图像列表中的索引 <xref:Microsoft.VisualStudio.Package.CompletionSet> ，并且是从类中的方法返回的相同图像列表 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> (<xref:Microsoft.VisualStudio.Package.CompletionSet> 如果你重写 <xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A> 类中的方法 <xref:Microsoft.VisualStudio.Package.Source> 以提供不同的图像) 列表，则可以更改要用于的图像列表。

### <a name="images-used-in-the-navigation-bar"></a>导航栏中使用的图像
 **导航栏**会显示类型和成员列表，并用于快速导航显示图标。 这些图标是从 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> 类中的方法获取的 <xref:Microsoft.VisualStudio.Package.LanguageService> ，不能专门用于 **导航栏**。 用于组合框中的每一项的索引是在类的方法中填充了表示组合框的列表时指定的 <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> (请参阅 [旧版语言服务中的导航栏](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)) 。 这些图像索引是从分析器获得的，通常是通过类的版本获取的 <xref:Microsoft.VisualStudio.Package.Declarations> 。 获取索引的方式完全取决于你。

### <a name="images-used-in-the-error-list-task-window"></a>用于错误列表任务窗口的图像
 每当 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法分析器 (查看 [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)) 遇到错误并将该错误传递给 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> 类中的方法时，将 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 在 **错误列表** 任务窗口中报告该错误。 图标可以与 "任务" 窗口中显示的每个项相关联，并且该图标来自类中从方法返回的同一图像列表 <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> 。 MPF 类的默认行为是不显示包含错误消息的图像。 但是，您可以通过从类派生一个类并重写方法来重写此行为 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A> 。 在此方法中，您将创建一个新的 <xref:Microsoft.VisualStudio.Package.DocumentTask> 对象。 返回该对象之前，可以使用 <xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A> 对象上的属性 <xref:Microsoft.VisualStudio.Package.DocumentTask> 设置图像索引。 这类似于下面的示例。 请注意， `TestIconImageIndex` 是一个枚举，它列出了所有图标并且特定于此示例。 你可以使用不同的方式来识别语言服务中的图标。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestSource : Source
    {
        public override DocumentTask CreateErrorTaskItem(
            TextSpan          span,
            string            filename,
            string            message,
            TaskPriority      priority,
            TaskCategory      category,
            MARKERTYPE        markerType,
            TaskErrorCategory errorCategory)
        {
            DocumentTask taskItem = base.CreateErrorTaskItem(
                                           span,
                                           filename,
                                           message,
                                           priority,
                                           category,
                                           markerType,
                                           errorCategory);
            if (errorCategory == TaskErrorCategory.Error)
            {
                taskItem.ImageIndex = TestIconImageIndex.Error;
            }
            return taskItem;
        }
    }
}
```

## <a name="the-default-image-list-for-a-language-service"></a>语言服务的默认图像列表
 随基本 MPF 语言服务类提供的默认图像列表包含多个与更常见的语言元素相关联的图标。 这三个图标按六个变体的形式进行排列，对应于公共、内部、友元、受保护、私有和快捷方式的访问概念。 例如，可以为方法提供不同的图标，具体取决于该方法是公共的、受保护的还是私有的。

 下面的枚举指定每个图标集的典型名称并指定关联的索引。 例如，根据枚举，可以将受保护的方法的图像索引指定为 `(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected` 。 您可以根据需要更改此枚举中的名称。

```csharp
public enum IconImageIndex
        {
            // access types
            AccessPublic = 0,
            AccessInternal = 1,
            AccessFriend = 2,
            AccessProtected = 3,
            AccessPrivate = 4,
            AccessShortcut = 5,

            Base = 6,
            // Each of the following icon type has 6 versions,
            //corresponding to the access types
            Class = Base + 0,
            Constant = Base + 1,
            Delegate = Base + 2,
            Enumeration = Base + 3,
            EnumMember = Base + 4,
            Event = Base + 5,
            Exception = Base + 6,
            Field = Base + 7,
            Interface = Base + 8,
            Macro = Base + 9,
            Map = Base + 10,
            MapItem = Base + 11,
            Method = Base + 12,
            OverloadedMethod = Base + 13,
            Module = Base + 14,
            Namespace = Base + 15,
            Operator = Base + 16,
            Property = Base + 17,
            Struct = Base + 18,
            Template = Base + 19,
            Typedef = Base + 20,
            Type = Base + 21,
            Union = Base + 22,
            Variable = Base + 23,
            ValueType = Base + 24,
            Intrinsic = Base + 25,
            JavaMethod = Base + 26,
            JavaField = Base + 27,
            JavaClass = Base + 28,
            JavaNamespace = Base + 29,
            JavaInterface = Base + 30,
            // Miscellaneous icons with one icon for each type.
            Error = 187,
            GreyedClass = 188,
            GreyedPrivateMethod = 189,
            GreyedProtectedMethod = 190,
            GreyedPublicMethod = 191,
            BrowseResourceFile = 192,
            Reference = 193,
            Library = 194,
            VBProject = 195,
            VBWebProject = 196,
            CSProject = 197,
            CSWebProject = 198,
            VB6Project = 199,
            CPlusProject = 200,
            Form = 201,
            OpenFolder = 202,
            ClosedFolder = 203,
            Arrow = 204,
            CSClass = 205,
            Snippet = 206,
            Keyword = 207,
            Info = 208,
            CallBrowserCall = 209,
            CallBrowserCallRecursive = 210,
            XMLEditor = 211,
            VJProject = 212,
            VJClass = 213,
            ForwardedType = 214,
            CallsTo = 215,
            CallsFrom = 216,
            Warning = 217,
        }
```

## <a name="see-also"></a>另请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
