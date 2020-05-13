---
title: 实现传统语言服务2 |微软文档
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
ms.openlocfilehash: e435af68a893c923eafef744762c9da8505c3fb7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707679"
---
# <a name="implementing-a-legacy-language-service"></a>实现旧版语言服务
要使用托管包框架 （MPF） 实现语言服务，必须从<xref:Microsoft.VisualStudio.Package.LanguageService>类派生一个类并实现以下抽象方法和属性：

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> 属性

  有关实现这些方法和属性的详细信息，请参阅以下相应部分。

  为了支持其他功能，您的语言服务可能必须从 MPF 语言服务类之一派生一个类;例如，为了支持其他菜单命令，必须从<xref:Microsoft.VisualStudio.Package.ViewFilter>类派生一个类并重写多个命令处理方法（有关详细信息，请参阅）。 <xref:Microsoft.VisualStudio.Package.ViewFilter> 该<xref:Microsoft.VisualStudio.Package.LanguageService>类提供了许多方法，这些方法被调用以创建各种类的新实例，并重写适当的创建方法以提供类的实例。 例如，您需要重写<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法以返回您自己的<xref:Microsoft.VisualStudio.Package.ViewFilter>类的实例。 有关详细信息，请参阅"即时自定义类"部分。

  您的语言服务还可以提供自己的图标，这些图标在许多地方使用。 例如，当显示 IntelliSense 完成列表时，列表中的每个项都可以具有与其关联的图标，将项标记为方法、类、命名空间、属性或任何语言所需的任何内容。 这些图标用于所有 IntelliSense 列表、**导航栏**和**错误列表**任务窗口中。 有关详细信息，请参阅下面的"语言服务图像"部分。

## <a name="getlanguagepreferences-method"></a>获取语言首选项方法
 该方法<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>始终返回<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类的相同实例。 如果不需要语言服务的任何其他<xref:Microsoft.VisualStudio.Package.LanguagePreferences>首选项，则可以使用基类。 MPF 语言服务类假定至少存在基<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。

### <a name="example"></a>示例
 此示例显示了<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>该方法的典型实现。 此示例使用基<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。

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

## <a name="getscanner-method"></a>获取扫描器方法
 此方法返回一个<xref:Microsoft.VisualStudio.Package.IScanner>对象的实例，该对象实现用于获取令牌及其类型和触发器的面向行解析器或扫描仪。 此扫描仪用于着色类，<xref:Microsoft.VisualStudio.Package.Colorizer>尽管扫描仪还可用于获取令牌类型和触发器，作为更复杂的分析操作的前奏。 必须提供实现接口的<xref:Microsoft.VisualStudio.Package.IScanner>类，并且必须实现<xref:Microsoft.VisualStudio.Package.IScanner>接口上的所有方法。

### <a name="example"></a>示例
 此示例显示了<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>该方法的典型实现。 类`TestScanner`实现<xref:Microsoft.VisualStudio.Package.IScanner>接口（未显示）。

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

## <a name="parsesource-method"></a>解析源方法
 基于许多不同的原因分析源文件。 此方法被赋予一个<xref:Microsoft.VisualStudio.Package.ParseRequest>对象，该对象描述特定分析操作的预期内容。 该方法<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>调用一个更复杂的解析器，用于确定令牌功能和范围。 该方法<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>用于支持 IntelliSense 操作和大括号匹配。 即使您不支持此类高级操作，您仍必须返回一个有效的<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象，并且需要创建一个实现<xref:Microsoft.VisualStudio.Package.AuthoringScope>接口并在该接口上实现所有方法的类。 可以从所有方法返回 null 值，<xref:Microsoft.VisualStudio.Package.AuthoringScope>但对象本身不能为空值。

### <a name="example"></a>示例
 此示例显示了<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法和<xref:Microsoft.VisualStudio.Package.AuthoringScope>类的最小实现，足以允许语言服务编译和运行，而无需实际支持任何更高级的功能。

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
 此属性返回语言服务的名称。 这必须与注册语言服务时给出的名称相同。 此名称用于多个位置，其中最突出的是使用该名称访问注册表的<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。 此属性返回的名称不能本地化，因为它在注册表中用于注册表项和密钥名称。

### <a name="example"></a>示例
 此示例显示<xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A>属性的一个可能实现。 请注意，此处的名称是硬编码的：实际名称应从资源文件获取，以便可用于注册语言服务（请参阅[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)）。

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
 可以重写指定类中的以下方法，以提供每个类的自己版本的实例。

### <a name="in-the-languageservice-class"></a>在语言服务类中

|方法|返回的类|描述|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|支持对文本视图的自定义添加。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|支持自定义文档属性。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|支持**导航栏**。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|支持代码段模板中的函数。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|支持代码段（此方法通常不会重写）。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|支持结构的<xref:Microsoft.VisualStudio.Package.ParseRequest>自定义（此方法通常不会重写）。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|支持设置源代码的格式，指定注释字符和自定义方法签名。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|支持其他菜单命令。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|支持语法突出显示（此方法通常不会重写）。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|支持访问语言首选项。 必须实现此方法，但可以返回基类的实例。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|提供用于标识行上令牌类型的解析器。 此方法必须实现，并且必须<xref:Microsoft.VisualStudio.Package.IScanner>派生自此方法。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|提供用于标识整个源文件中的功能和范围的解析器。 此方法必须实现，并且必须返回<xref:Microsoft.VisualStudio.Package.AuthoringScope>类版本的实例。 如果只想支持的只是语法突出显示（这需要从<xref:Microsoft.VisualStudio.Package.IScanner><xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法返回的解析器），则除了返回<xref:Microsoft.VisualStudio.Package.AuthoringScope>该方法都返回 null 值的类版本外，此方法中没有任何操作。|

### <a name="in-the-source-class"></a>在源类中

|方法|返回的类|描述|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|要自定义 IntelliSense 完成列表的显示（此方法通常不会重写）。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|有关错误列表任务列表中的支持标记;具体来说，除了打开文件和跳转到导致错误的行之外，还支持功能。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|用于自定义 IntelliSense 参数信息工具提示的显示。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|用于支持注释代码。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|用于在分析操作期间收集信息。|

### <a name="in-the-authoringscope-class"></a>在创作范围类中

|方法|返回的类|描述|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|提供声明列表，如成员或类型。 必须实现此方法，但可以返回 null 值。 如果此方法返回有效对象，则该对象必须是<xref:Microsoft.VisualStudio.Package.Declarations>类版本的实例。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|提供给定上下文的方法签名列表。 必须实现此方法，但可以返回 null 值。 如果此方法返回有效对象，则该对象必须是<xref:Microsoft.VisualStudio.Package.Methods>类版本的实例。|

## <a name="language-service-images"></a>语言服务图像
 要提供整个语言服务中使用的图标列表，请重写<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法并返回包含图标的 图标。 <xref:System.Windows.Forms.ImageList> 基<xref:Microsoft.VisualStudio.Package.LanguageService>类加载一组默认的图标。 由于在需要图标的地方指定了确切的图像索引，因此如何排列自己的图像列表完全取决于您。

### <a name="images-used-in-intellisense-completion-lists"></a>在"感知完成列表"中使用的图像
 对于 IntelliSense 完成列表，为<xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A><xref:Microsoft.VisualStudio.Package.Declarations>类方法中的每个项指定了图像索引，如果要提供图像索引，则必须重写该项。 从<xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A>方法返回的值是提供给<xref:Microsoft.VisualStudio.Package.CompletionSet>类构造函数的图像列表中的索引，它是从<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法返回的相同图像列表（<xref:Microsoft.VisualStudio.Package.CompletionSet>如果重写<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A><xref:Microsoft.VisualStudio.Package.Source>类中的方法以提供不同的图像列表，则可以更改要使用的图像列表）。

### <a name="images-used-in-the-navigation-bar"></a>导航栏中使用的图像
 **导航栏**显示类型和成员的列表，用于快速导航可以显示图标。 这些图标是从类中的方法<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>获取的，<xref:Microsoft.VisualStudio.Package.LanguageService>不能专门针对**导航栏**进行重写。 当表示组合框的列表在<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A><xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类中填充方法时，将指定用于组合框中每个项目的索引（请参阅[旧语言服务中导航栏的支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)）。 这些图像索引以某种方式从解析器获得，通常是通过<xref:Microsoft.VisualStudio.Package.Declarations>类的版本获得的。 如何获得指数完全由您决定。

### <a name="images-used-in-the-error-list-task-window"></a>错误列表任务窗口中使用的图像
 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>每当方法解析器（请参阅[旧语言服务解析器和扫描仪](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)）遇到错误并将该错误<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A>传递给<xref:Microsoft.VisualStudio.Package.AuthoringSink>类中的方法时，错误将在**错误列表**任务窗口中报告。 图标可以与任务窗口中显示的每个项相关联，并且该图标来自从<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A><xref:Microsoft.VisualStudio.Package.LanguageService>类中的方法返回的相同图像列表。 MPF 类的默认行为是不显示带有错误消息的图像。 但是，您可以通过从<xref:Microsoft.VisualStudio.Package.Source>类派生类并重写方法来<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>重写此行为。 在该方法中，您将创建一个新<xref:Microsoft.VisualStudio.Package.DocumentTask>对象。 在返回该对象之前，<xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A>可以使用<xref:Microsoft.VisualStudio.Package.DocumentTask>对象上的属性来设置图像索引。 这类似于下面的示例。 请注意，`TestIconImageIndex`这是一个枚举，列出所有图标，并特定于此示例。 您可能有不同的方法来识别语言服务中的图标。

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

## <a name="the-default-image-list-for-a-language-service"></a>语言服务的默认映像列表
 基本 MPF 语言服务类附带的默认映像列表包含许多与更常见语言元素关联的图标。 这些图标的大部分排列在六种变体中，对应于公共、内部、朋友、受保护、私有和快捷方式的访问概念。 例如，根据方法是公共图标、受保护图标还是私有图标，可以为方法使用不同的图标。

 以下枚举为每个图标集指定典型名称，并指定关联的索引。 例如，根据枚举，可以将受保护方法的图像索引指定为`(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected`。 您可以根据需要更改此枚举中的名称。

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

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
