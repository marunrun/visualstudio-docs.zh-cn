---
title: 实现旧版语言服务 2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6105f46740dc854f4c498adad5bbd5fe675b41f6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335146"
---
# <a name="implementing-a-legacy-language-service"></a>实现旧版语言服务
若要实现使用托管的包框架 (MPF) 的语言服务，你必须从派生类<xref:Microsoft.VisualStudio.Package.LanguageService>类并实现以下抽象方法和属性：

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法

- <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> 属性

  实现这些方法和属性，请参阅下面有关详细信息的相应部分。

  若要支持其他功能，你的语言服务可能需要从 MPF 语言服务类; 之一派生一个类例如，若要支持其他菜单命令，必须派生一个类从<xref:Microsoft.VisualStudio.Package.ViewFilter>类并重写几个命令处理方法 (请参阅<xref:Microsoft.VisualStudio.Package.ViewFilter>有关详细信息)。 <xref:Microsoft.VisualStudio.Package.LanguageService>类提供了多种方法可通过调用创建的各种类的新实例，并重写相应的创建方法以提供您的类的实例。 例如，你需要重写<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类以返回您自己的实例<xref:Microsoft.VisualStudio.Package.ViewFilter>类。 请参阅更多详细信息"实例化自定义类"部分。

  语言服务还可以提供自己的许多地方使用的图标。 例如，IntelliSense 完成列表显示时，列表中的每个项可以有与之关联，将项标记为方法、 类、 命名空间、 property、 一个图标或任何内容是你的语言的必要条件。 使用这些图标位于所有 IntelliSense 列表中，**导航栏**，然后在**错误列表**任务窗口。 请参阅以下"语言服务映像"部分以了解详细信息。

## <a name="getlanguagepreferences-method"></a>GetLanguagePreferences 方法
 <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>方法始终返回同一个实例<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。 可以使用基<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类如果不需要语言服务的任何其他首选项。 MPF 语言服务类假定存在至少基本<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。

### <a name="example"></a>示例
 此示例演示的典型实现<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>方法。 此示例使用基本<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。

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
 此方法返回的实例<xref:Microsoft.VisualStudio.Package.IScanner>实现面向行的分析器或扫描程序用于获取令牌及其类型和触发器的对象。 此扫描程序中使用<xref:Microsoft.VisualStudio.Package.Colorizer>尽管扫描程序还可用于获取令牌类型和触发器以作更复杂的分析操作但对着色类。 必须提供实现的类<xref:Microsoft.VisualStudio.Package.IScanner>接口，并且您必须实现的所有方法上<xref:Microsoft.VisualStudio.Package.IScanner>接口。

### <a name="example"></a>示例
 此示例演示的典型实现<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法。 `TestScanner`类实现<xref:Microsoft.VisualStudio.Package.IScanner>（未显示） 的接口。

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
 分析基于多种不同原因的源代码文件。 此方法提供<xref:Microsoft.VisualStudio.Package.ParseRequest>对象，描述从特定的分析操作的预期。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法调用更复杂的分析程序，用于确定令牌功能和作用域。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法用在支持的智能感知操作以及大括号匹配。 即使不支持此类高级的操作，您仍必须返回有效<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象，并且需要创建一个实现类<xref:Microsoft.VisualStudio.Package.AuthoringScope>接口并实现该接口上的所有方法。 你可以从所有方法返回 null 值，但<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象本身不能为 null 值。

### <a name="example"></a>示例
 此示例中显示的最小实现<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法和<xref:Microsoft.VisualStudio.Package.AuthoringScope>类，不足以允许语言服务，才能编译和运行而无需实际支持任何更高级的功能。

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
 此属性返回的语言服务的名称。 这必须是已注册的语言服务时指定的相同名称。 此名称用于在许多位置，最突出的是<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类的名称用于访问注册表。 返回此属性的名称必须不会本地化，因为它将用于在注册表中的注册表项和密钥名称。

### <a name="example"></a>示例
 此示例演示一种可能的实现<xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A>属性。 请注意，此处的名称是硬编码： 的实际名称应获取从资源文件，可以注册语言服务中使用它 (请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md))。

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
 可以重写中指定的类的以下方法以提供您自己版本的每个类的实例。

### <a name="in-the-languageservice-class"></a>LanguageService 类中

|方法|返回类|描述|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|若要支持自定义添加到文本视图。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|若要支持自定义文档属性。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|若要支持**导航栏**。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|若要支持中的代码片段模板函数。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|若要支持代码段 （此方法通常未重写）。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|若要支持的自定义<xref:Microsoft.VisualStudio.Package.ParseRequest>结构 （此方法通常未重写）。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|若要支持格式设置源代码，指定注释字符和自定义方法签名。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|若要支持其他菜单命令。|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|若要支持语法突出显示 （此方法通常未重写）。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|若要支持对语言首选项的访问。 此方法必须实现，但可以返回基的类的实例。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|若要提供用于标识类型的行上的标记的分析器。 必须实现此方法和<xref:Microsoft.VisualStudio.Package.IScanner>必须派生自。|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|若要提供用于标识功能和范围贯穿整个源文件的分析器。 此方法必须实现，并且必须返回实例的版本<xref:Microsoft.VisualStudio.Package.AuthoringScope>类。 如果所有你想要支持语法突出显示 (这需要<xref:Microsoft.VisualStudio.Package.IScanner>从返回的分析器<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>方法)，则可以执行任何操作不返回此方法中的版本<xref:Microsoft.VisualStudio.Package.AuthoringScope>类的方法都将返回 null 值。|

### <a name="in-the-source-class"></a>在源类

|方法|返回类|描述|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|用于自定义的 IntelliSense 完成列表 （此方法通常未重写） 显示。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|在错误列表任务列表; 支持标记具体而言，支持打开文件并跳转到导致该错误的行之外的功能。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|用于自定义的 IntelliSense 参数信息工具提示显示。|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|有关支持注释的代码。|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|用于收集分析操作过程中的信息。|

### <a name="in-the-authoringscope-class"></a>AuthoringScope 类中

|方法|返回类|描述|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|提供了一系列等成员或类型声明。 此方法必须实现，但可以返回 null 值。 如果此方法返回有效的对象，该对象必须是实例的版本<xref:Microsoft.VisualStudio.Package.Declarations>类。|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|对于给定的上下文中提供方法签名的列表。 此方法必须实现，但可以返回 null 值。 如果此方法返回有效的对象，该对象必须是实例的版本<xref:Microsoft.VisualStudio.Package.Methods>类。|

## <a name="language-service-images"></a>语言服务映像
 若要提供图标，以在整个语言服务中使用的列表，请重写<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类，并返回<xref:System.Windows.Forms.ImageList>包含图标。 基<xref:Microsoft.VisualStudio.Package.LanguageService>类加载一组默认的图标。 由于在需要的图标的位置指定完全相同的映像索引，映像列表的排列方式是完全取决于您。

### <a name="images-used-in-intellisense-completion-lists"></a>IntelliSense 完成列表中使用的图像
 对于 IntelliSense 完成列表的图像索引指定中每一项<xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A>方法的<xref:Microsoft.VisualStudio.Package.Declarations>类，如果你想要提供一个图像索引时，必须重写。 从返回的值<xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A>方法是提供给的图像列表索引<xref:Microsoft.VisualStudio.Package.CompletionSet>类构造函数，并且在同一个图像列表返回从<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类 （您可以更改到的图像列表用于<xref:Microsoft.VisualStudio.Package.CompletionSet>如果重写<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>中的方法<xref:Microsoft.VisualStudio.Package.Source>类来提供不同的图像列表)。

### <a name="images-used-in-the-navigation-bar"></a>在导航栏中使用的图像
 **导航栏**显示类型和成员的列表，并使用快速导航可以显示图标。 这些图标从获取<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类，并不能重写专用于**导航栏**。 表示组合框的列表填充时指定用于组合框中的每个项的索引<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A>中的方法<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>类 (请参阅[支持旧版语言服务中的导航栏](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)). 这些映像索引从分析器，通常是通过你的版本以某种方式获取<xref:Microsoft.VisualStudio.Package.Declarations>类。 获取索引的方式是完全取决于您。

### <a name="images-used-in-the-error-list-task-window"></a>在错误列表任务窗口中使用的图像
 每当<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法分析程序 (请参阅[旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)) 时遇到错误，并将传递到该错误<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A>中的方法<xref:Microsoft.VisualStudio.Package.AuthoringSink>类内报告错误**错误列表**任务窗口。 图标可以显示在任务窗口中每个项与相关联，并且该图标来自从返回的相同映像列表<xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A>中的方法<xref:Microsoft.VisualStudio.Package.LanguageService>类。 MPF 类的默认行为是不显示的图像并显示错误消息。 但是，通过派生类中的重写此行为<xref:Microsoft.VisualStudio.Package.Source>类并重写<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>方法。 在该方法中，您创建一个新<xref:Microsoft.VisualStudio.Package.DocumentTask>对象。 再返回该对象，可以使用<xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A>属性上的<xref:Microsoft.VisualStudio.Package.DocumentTask>对象，以设置的图像索引。 这看起来如下例所示。 请注意，`TestIconImageIndex`是一个枚举，列出了所有图标和特定于此示例。 您可能必须识别语言服务中的图标的不同方法。

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
 提供基本的 MPF 语言服务类的默认图像列表包含大量的更常用的语言元素与关联的图标。 在六个变体，公共、 内部、 友元，受保护、 专用的、 和快捷方式的访问权限概念相对应的组中排列这些图标的大容量。 例如，可以有不同的图标根据它是公共、 受保护或私有方法。

 以下枚举指定为每个图标集的典型名称，并指定相关联的索引。 例如，根据枚举，您可以指定为受保护的方法的图像索引`(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected`。 你可以根据需要此枚举中的名称。

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