---
title: 用于不可改变阵列的罗斯林分析仪和代码感知库 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2076bc9fe3cabbfef8d3f3fb0248724835fa83f5
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444565"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>用于不可改变阵列的 Roslyn 分析仪和代码感知库

[.NET 编译器平台](https://github.com/dotnet/roslyn)（"Roslyn"） 可帮助您构建代码感知库。 代码感知库提供了可以使用和工具（Roslyn 分析器）的功能，以帮助您以最佳方式使用库或避免错误。 本主题介绍如何构建真实世界 Roslyn 分析器，以在使用 System[时](https://www.nuget.org/packages/System.Collections.Immutable)捕获常见错误。 该示例还演示如何为分析器找到的代码问题提供代码修复。 用户在 Visual Studio 灯泡 UI 中看到代码修复，并可以自动应用代码的修复程序。

## <a name="get-started"></a>入门

构建此示例需要以下内容：

* Visual Studio 2015（不是速成版）或更高版本。 您可以使用免费[的视觉工作室社区版](https://visualstudio.microsoft.com/vs/community/)
* [视觉工作室 SDK](../extensibility/visual-studio-sdk.md). 您还可以在安装 Visual Studio 时，在 **"通用工具**"下检查**可视化工作室扩展工具**以同时安装 SDK。 如果您已经安装了 Visual Studio，还可以通过访问主菜单 **"文件** > **新项目** > **"来**安装此 SDK，在左侧导航窗格中选择**C#，** 然后选择 **"可扩展性**"。 当您选择"**安装可视化工作室扩展工具**"面包屑项目模板时，它会提示您下载并安装 SDK。
* [.NET 编译器平台 （"罗斯林"） SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK). 您还可以通过访问主菜单 **"文件** > **新项目** > **"来**安装此 SDK，在左侧导航窗格中选择**C#，** 然后选择 **"可扩展性**"。 当您选择"**下载.NET编译器平台 SDK"** 面包屑项目模板时，它会提示您下载并安装 SDK。 此 SDK 包括[罗斯林语法可视化工具](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer)。 此工具可帮助您确定应在分析器中查找的代码模型类型。 分析器基础结构会调用代码以进行特定的代码模型类型，因此代码仅在必要时执行，并且只能专注于分析相关代码。

## <a name="whats-the-problem"></a>怎么了？

假设您提供了一个包含不可改变阵列（例如）<xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>支持的库。 C# 开发人员在 .NET 阵列方面拥有丰富的经验。 但是，由于实现中使用的 ImmutableArray 和优化技术的性质，C# 开发人员直觉会导致库的用户编写损坏的代码，如下所述。 此外，用户在运行时之前不会看到自己的错误，这不是他们在带有 .NET 的 Visual Studio 中习惯的质量体验。

用户熟悉编写代码，如下所示：

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

创建空数组以填充后续代码行并使用集合初始化器语法是 C# 开发人员所熟悉的。 但是，为运行时的不可改变阵列崩溃编写相同的代码：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

第一个错误是由于 ImmutableArray 实现使用结构来包装基础数据存储。 结构必须具有无参数构造函数，`default(T)`以便表达式可以返回包含所有零或空成员的结构。 当代码访问`b1.Length`时，存在运行时 null 取消引用错误，因为 ImmutableArray 结构中没有基础存储数组。 创建空不可改变数组的正确方法是`ImmutableArray<int>.Empty`。

集合初始化程序出现错误的原因是，每次调用`ImmutableArray.Add`该方法时，该方法都会返回新实例。 由于 ImmutableArray 永远不会更改，因此在添加新元素时，您将获得一个新的 ImmutableArray 对象（出于性能原因，该对象可能与以前存在的 ImmutableArray 共享存储）。 因为`b2`在调用`Add()`五次之前指向第一个不可改变数组，`b2`因此是默认的不可改变数组。 调用长度上也崩溃与空取消引用错误。 在不手动调用 Add 的情况下初始化不可量数组的正确方法是使用`ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})`。

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>查找触发分析器的相关语法节点类型

 要开始构建分析器，首先确定需要查找的语法Node类型。 从菜单启动**语法可视化工具****查看** > **其他 Windows** > **罗斯林语法可视化工具**。

将编辑器的图子放在声明 的行上`b1`。 您将看到语法可视化器显示您位于语法树的`LocalDeclarationStatement`节点中。 此节点有`VariableDeclaration`一个 ，它反过来`VariableDeclarator`又有 一个`EqualsValueClause`，最后有一个`ObjectCreationExpression`。 当您单击节点的语法可视化器树时，编辑器窗口中的语法将突出显示以显示该节点表示的代码。 语法节点子类型的名称与 C# 语法中使用的名称匹配。

## <a name="create-the-analyzer-project"></a>创建分析器项目

从主菜单中，选择 **"文件** > **新项目** > **"。** 在 **"新项目**"对话框中，在左侧导航栏中的**C#** 项目下，选择 **"可扩展性**"，并在右侧窗格中选择 **"具有代码修复器"项目模板的"分析器**"。 输入名称并确认对话框。

模板将打开*一个DiagnosticAnalyzer.cs*文件。 选择该编辑器缓冲区选项卡。此文件具有从`DiagnosticAnalyzer`（Roslyn API 类型）派生的分析器类（由您给项目的名称构成）。 您的新类具有声明`DiagnosticAnalyzerAttribute`分析器与 C# 语言相关的声明，以便编译器发现并加载分析器。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

您可以使用面向 C# 代码的 Visual Basic 实现分析器，反之亦然。 在诊断分析器属性中，选择分析器是针对一种语言还是两种语言更为重要。 需要详细建模语言的更复杂的分析器只能针对一种语言。 例如，如果分析器仅检查类型名称或公共成员名称，则可以使用 Roslyn 跨 Visual Basic 和 C# 提供的通用语言模型。 例如，FxCop 警告类实现<xref:System.Runtime.Serialization.ISerializable>，但类没有独立于语言<xref:System.SerializableAttribute>的属性，适用于 Visual Basic 和 C# 代码。

## <a name="initialize-the-analyzer"></a>初始化分析器

 在类中`DiagnosticAnalyzer`向下滚动一点以查看方法`Initialize`。 激活分析器时编译器调用此方法。 该方法采用一个`AnalysisContext`对象，该对象允许分析器获取上下文信息，并为要分析的代码类型注册事件回调。

```csharp
public override void Initialize(AnalysisContext context) {}
```

在此方法中打开一条新行，并键入"上下文"。 查看 IntelliSense 完成列表。 您可以在完成列表中看到有许多`Register...`方法可以处理各种事件。 例如，第一个 ，`RegisterCodeBlockAction`调用回您的代码块，这通常是代码之间的大括号。 注册块还会调用到代码，用于字段的初始化器、给定到属性的值或可选参数的值。

另一个示例`RegisterCompilationStartAction`在编译开始时调用回代码，当您需要收集多个位置的状态时，这非常有用。 您可以创建数据结构，例如，收集使用的所有符号，每次调用分析器以查找某些语法或符号时，都可以保存有关数据结构中每个位置的信息。 当您由于编译结束而被回调时，可以分析保存的所有位置，例如，报告代码使用每个`using`语句的符号。

使用**语法可视化工具**，您了解到当编译器处理 Object 创造表达式时，您希望被调用。 使用此代码设置回调：

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

注册语法节点，并仅注册对象创建语法节点的筛选器。 按照惯例，分析器作者在注册操作时使用 lambda，这有助于使分析器保持无状态。 您可以使用"**从使用情况生成**"视觉工作室功能来创建`AnalyzeObjectCreation`该方法。 这也会为您生成正确的上下文参数类型。

## <a name="set-properties-for-users-of-your-analyzer"></a>为分析器用户设置属性

因此，您的分析器适当地显示在 Visual Studio UI 中，请查找并修改以下代码行以标识分析器：

```csharp
internal const string Category = "Naming";
```

将 `"Naming"` 更改为 `"API Guidance"`。

使用**解决方案资源管理器**在项目中查找并打开*资源.resx*文件。 您可以为分析器、标题等提供说明。您可以将所有这些`"Don't use ImmutableArray<T> constructor"`值更改为现在。 您可以将字符串{0}格式参数放在字符串中 （、{1}等），稍后调用`Diagnostic.Create()`时，可以提供要传递的参数`params`数组。

## <a name="analyze-an-object-creation-expression"></a>分析对象创建表达式

该方法`AnalyzeObjectCreation`采用代码分析器框架提供的不同类型的上下文。 该方法`Initialize``AnalysisContext`允许您注册操作回调以设置分析器。 例如`SyntaxNodeAnalysisContext`，有一个`CancellationToken`可以传递的。 如果用户开始键入编辑器，Roslyn 将取消运行分析器以节省工作并提高性能。 另一个示例是，此上下文具有返回对象创建语法节点的 Node 属性。

获取节点，您可以假定该节点是筛选语法节点操作的类型：

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>首次使用分析器启动可视化工作室

通过构建和执行分析器启动可视化工作室（按**F5**）。 由于**解决方案资源管理器**中的启动项目是 VSIX 项目，因此运行代码将生成代码和 VSIX，然后启动安装了该 VSIX 的可视化工作室。 以这种方式启动 Visual Studio 时，它会使用不同的注册表配置单元启动，这样您在构建分析器时对 Visual Studio 的主要使用不会受到测试实例的影响。 首次以这种方式启动时，Visual Studio 会执行多个初始化，类似于安装后首次启动 Visual Studio 时的初始化。

创建控制台项目，然后将数组代码输入到控制台应用程序中 Main 方法：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

带`ImmutableArray`的代码行有波浪形，因为您需要获取不可变的 NuGet 包并将语句`using`添加到代码中。 按**解决方案资源管理器**中项目节点上的右指针按钮，然后选择 **"管理 NuGet 包**"。 在 NuGet 管理器中，在搜索框中键入"不可改变"，然后选择"**项目 System. 集合.不可改变"（** 不要选择**Microsoft.Bcl.Immu 可操作**），然后按右侧窗格中的 **"安装**"按钮。 安装包会添加对项目引用的引用。

你仍然看到红色波浪`ImmutableArray`下，所以把插入器放在该标识符，然后按**Ctrl**+**。** （期间）以显示建议的修复菜单并选择添加适当的`using`语句。

**立即保存所有实例并关闭**Visual Studio 的第二个实例，以将您置于干净状态以继续。

## <a name="finish-the-analyzer-using-edit-and-continue"></a>使用编辑完成分析器并继续

在 Visual Studio 的第一个实例中，通过在第一行上`AnalyzeObjectCreation`按**F9**与加斯特一起在方法的开头设置断点。

使用**F5**再次启动分析器，在 Visual Studio 的第二个实例中，重新打开上次创建的控制台应用程序。

返回到断点处 Visual Studio 的第一个实例，因为 Roslyn 编译器看到对象创建表达式并调用到分析器中。

**获取对象创建节点。** 通过按**F10**`objectCreation`和**在"立即窗口**"中计算表达式`"objectCreation.ToString()"`，单步执行设置变量的行。 您可以看到，变量指向的语法节点是代码`"new ImmutableArray<int>()"`，这正是您要查找的代码。

**获取 t\>类型对象<不可改变数组。** 您需要检查正在创建的类型是否为不可改变数组。 首先，获取表示此类型的对象。 使用语义模型检查类型，以确保您拥有完全正确的类型，并且不会比较 中的`ToString()`字符串。 在函数末尾输入以下代码行：

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

在元数据中指定具有回记 （'） 和泛型参数数的泛型类型。 这就是为什么你没有看到"...元数据名称中的不可\<可变数组 T>"。

语义模型有许多有用的东西，允许您询问有关符号、数据流、变量生存期等的问题。由于各种工程原因（性能、建模错误代码等），Roslyn 将语法节点与语义模型分开。 您希望编译模型查找引用中包含的信息，以便进行准确的比较。

您可以在编辑器窗口的左侧拖动黄色执行指针。 将其拖动到设置变量的`objectCreation`行，并使用**F10**跨过新代码行。 如果将鼠标指针悬停在变量`immutableArrayOfType`上，则发现我们在语义模型中找到了确切的类型。

**获取对象创建表达式的类型。** 本文以多种方式使用"Type"，但这意味着如果您有"新 Foo"表达式，则需要获取 Foo 的模型。 您需要获取对象创建表达式的类型，以查看它是不可改变的 Array\<T> 类型。 再次使用语义模型获取对象创建表达式中类型符号（不可改变数组）的符号信息。 在函数末尾输入以下代码行：

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

由于分析器需要处理编辑器缓冲区中不完整或不正确的代码（例如，缺少语句`using`），因此应检查是否`symbolInfo`为`null`。 您需要从符号信息对象中获取命名类型（I命名类型符号）才能完成分析。

**比较类型。** 由于我们要查找的 T 的开放式泛型类型，并且代码中的类型是具体的泛型类型，因此您查询符号信息，了解类型来自什么（开放泛型类型），并将该结果与`immutableArrayOfTType`进行比较。 在方法的末尾输入以下内容：

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**报告诊断。** 报告诊断非常简单。 在初始化方法之前定义的项目模板中，可以使用为您创建的规则。 由于代码中的此情况是错误的，因此您可以将初始化规则替换`DiagnosticSeverity.Warning`的行（绿色波浪）替换为`DiagnosticSeverity.Error`（红色波浪）。 规则的其余部分从演练开头附近编辑的资源初始化。 您还需要报告波浪形的位置，即对象创建表达式的类型规范的位置。 在块中`if`输入此代码：

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

您的函数应如下所示（可能采用不同的格式）：

```csharp
private void AnalyzeObjectCreation(SyntaxNodeAnalysisContext context)
{
    var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
    var immutableArrayOfTType =
        context.SemanticModel
               .Compilation
               .GetTypeByMetadataName(
                   "System.Collections.Immutable.ImmutableArray`1");
    var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as
        INamedTypeSymbol;
    if (symbolInfo != null &&
        symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
    {
        context.ReportDiagnostic(
            Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
    }
}
```

删除断点，以便可以看到分析器工作（并停止返回到 Visual Studio 的第一个实例）。 将执行指针拖动到方法的开头，然后按**F5**继续执行。 当您切换回 Visual Studio 的第二个实例时，编译器将开始再次检查代码，并将调用到分析器中。 您可以在 下`ImmutableType<int>`看到一个波浪形。

## <a name="adding-a-code-fix-for-the-code-issue"></a>为代码问题添加"代码修复"

开始之前，关闭 Visual Studio 的第二个实例，并在 Visual Studio 的第一个实例（您正在开发分析器）中停止调试。

**添加新类。** 在**解决方案资源管理器**中的项目节点上使用快捷方式菜单（右指针按钮），然后选择添加新项。 添加名为`BuildCodeFixProvider`的类。 类`CodeFixProvider`需要派生自 ，并且您需要使用**Ctrl**+**。** （期间）以调用添加正确`using`语句的代码修复程序。 此类还需要使用`ExportCodeFixProvider`属性进行说明，并且需要添加语句`using`来解决`LanguageNames`枚举。 应该有一个包含以下代码的类文件：

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**存出派生成员。** 现在，将编辑器的插入符放在`CodeFixProvider`标识符中，然后按**Ctrl**+**。** （期间）以存根此抽象基类的实现。 这将为您生成属性和方法。

**实现属性。** 使用以下代码`FixableDiagnosticIds`填写属性`get`的正文：

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn 通过匹配这些标识符（只是字符串）来组合诊断和修复。 项目模板为您生成了诊断 ID，您可以自由更改它。 属性中的代码只是从分析器类返回 ID。

**注册代码修复同步方法采用上下文。** 上下文很重要，因为代码修复可以应用于多个诊断，或者代码行上可能有多个问题。 如果键入"上下文"。 在该方法的正文中，IntelliSense 完成列表将显示一些有用的成员。 有一个取消令牌成员，您可以检查，看看是否有东西要取消修复。 有一个 Document 成员，它有许多有用的成员，允许您访问项目和解决方案模型对象。 有一个 Span 成员是报告诊断时指定的代码位置的开始和结束。

**使该方法是异步的。** 您需要做的第一`async`件事是将生成的方法声明固定为方法。 用于存根的抽象类实现的代码修复不包括关键字，`async`即使 方法返回 。 `Task`

**获取语法树的根。** 要修改代码，您需要使用代码修复程序所做的更改生成新的语法树。 您需要`Document`从上下文中调用`GetSyntaxRootAsync`。 这是一个异步方法，因为有未知的工作来获取语法树，可能包括从磁盘获取文件，对其进行解析，并为它构建 Roslyn 代码模型。 Visual Studio UI 应在此期间响应，使用`async`启用。 将方法中的代码行替换为以下内容：

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**查找问题节点。** 在上下文的范围内传递，但找到的节点可能不是必须更改的代码。 报告的诊断仅提供类型标识符（波浪形属于的位置）的跨度，但您需要替换整个对象创建表达式，包括开头的`new`关键字和末尾的括号。 将以下代码添加到方法（并使用**Ctrl**+**。** 为 添加`using``ObjectCreationExpressionSyntax`语句。

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**注册灯泡 UI 的代码修复程序。** 注册代码修复程序时，Roslyn 会自动插入 Visual Studio 灯泡 UI。 最终用户将看到他们可以使用**Ctrl。**+**.** （句点）当分析器切换不良`ImmutableArray<T>`构造函数使用时。 由于代码修复提供程序仅在出现问题时执行，因此可以假定您具有要查找的对象创建表达式。 从上下文参数中，您可以通过将以下代码添加到方法末尾`RegisterCodeFixAsync`来注册新的代码修复：

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

您需要将编辑器的插入符放在标识符`CodeAction`中，然后使用**Ctrl**+**。** （期间）以添加此类型的`using`相应语句。

然后，将编辑器的插入符放在标识符中`ChangeToImmutableArrayEmpty`，并使用**Ctrl**+**。** 再次为您生成此方法存根。

您添加的最后一个代码段通过传递 找到的问题类型的`CodeAction`和 诊断 ID 来注册代码修复。 在此示例中，此代码仅提供一个诊断 ID，因此只需传递诊断 ID 数组的第一个元素即可。 创建 时，`CodeAction`将 传递灯泡 UI 应用作代码修复说明的文本。 您还可以传递一个函数，该函数采用取消令牌并返回新文档。 新文档有一个新的语法树，其中包含调用`ImmutableArray.Empty`的修补代码。 此代码段使用 lambda，以便它可以关闭对象创建节点和上下文的文档。

**构造新的语法树。** 在前面生成`ChangeToImmutableArrayEmpty`存根的方法中，输入代码行： `ImmutableArray<int>.Empty;`。 如果再次查看**语法可视化工具**工具窗口，则可以看到此语法是简单成员访问表达式节点。 这是此方法需要在新的文档中构造和返回的内容。

第一个更改`ChangeToImmutableArrayEmpty`是之前`Task<Document>`添加`async`，因为代码生成器不能假定该方法应该是异步的。

使用以下代码填充正文，以便方法看起来类似于以下内容：

```csharp
private async Task<Document> ChangeToImmutableArrayEmpty(
    ObjectCreationExpressionSyntax objectCreation, Document document,
    CancellationToken c)
{
    var generator = SyntaxGenerator.GetGenerator(document);
    var memberAccess =
        generator.MemberAccessExpression(objectCreation.Type, "Empty");
    var oldRoot = await document.GetSyntaxRootAsync(c);
    var newRoot = oldRoot.ReplaceNode(objectCreation, memberAccess);
    return document.WithSyntaxRoot(newRoot);
}
```

`SyntaxGenerator`您需要将编辑器的插入符放在标识符中并使用**Ctrl**+**。** （期间）以添加此类型的`using`相应语句。

此代码使用`SyntaxGenerator`，这是构建新代码的有用类型。 获取具有代码问题的文档的生成器后，`ChangeToImmutableArrayEmpty`调用`MemberAccessExpression`、传递具有要访问的成员的类型，并将成员的名称作为字符串传递。

接下来，该方法获取文档的根，由于这可能涉及一般情况下的任意工作，因此代码等待此调用并传递取消令牌。 Roslyn 代码模型是不可变的，就像使用 .NET 字符串一样;更新字符串时，您将获得一个新的字符串对象作为回报。 当您调用`ReplaceNode`时，您会返回一个新的根节点。 大多数语法树是共享的（因为它是不可变的），但`objectCreation`节点被`memberAccess`节点以及语法树根的所有父节点替换。

## <a name="try-your-code-fix"></a>尝试代码修复

现在，您可以按**F5**在 Visual Studio 的第二个实例中执行分析器。 打开以前使用的控制台项目。 现在，您应该看到灯泡出现在新对象创建表达式的所在`ImmutableArray<int>`位置。 如果按**Ctrl**+**。** （期间），然后您将看到代码修复程序，并在灯泡 UI 中看到自动生成的代码差异预览。 罗斯林为你创造这个

**专业提示：** 如果启动 Visual Studio 的第二个实例，并且看不到带有代码修复功能的灯泡，则可能需要清除 Visual Studio 组件缓存。 清除缓存将强制 Visual Studio 重新检查组件，因此 Visual Studio 应选取最新的组件。 首先，关闭视觉工作室的第二个实例。 然后，在**Windows 资源管理器**中，导航到 *%LOCALAPPDATA%\微软_VisualStudio_16.0Roslyn\\*。 （使用 Visual Studio 将"16.0"从版本更改为版本。删除子目录*组件模型缓存*。

## <a name="talk-video-and-finish-code-project"></a>谈论视频和完成代码项目

你可以看到这个例子在[本文](https://channel9.msdn.com/events/Build/2015/3-725)中得到进一步开发和讨论。 谈话演示了工作分析器，并引导您完成构建它。

你可以[在这里](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)看到所有完成的代码。 子文件夹 *"不用Immu可寻形收集初始化器**"和"不用不可改变的ArrayCtor"* 各有一个用于查找问题的 C# 文件和一个 C# 文件，用于实现显示在 Visual Studio 灯泡 UI 中的代码修复。 请注意，已完成的代码具有多一点的抽象，以避免一遍又一遍地获取 ImmutableArray\<T>类型对象。 它使用嵌套注册的操作将类型对象保存在执行子操作（分析对象创建和分析集合初始化）时可用的上下文中。

## <a name="see-also"></a>请参阅

* [\\*构建 2015 年谈话](https://channel9.msdn.com/events/Build/2015/3-725)
* [GitHub 上已完成的代码](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [GitHub 的几个示例，分为三种分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [GitHub OSS 网站上的其他文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [在 GitHub 上使用 Roslyn 分析器实现的 FxCop 规则](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
