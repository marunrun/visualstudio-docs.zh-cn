---
title: 用于 ImmutableArrays 的 Roslyn 分析器和代码识别库 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8665a37e4afd387ff4f77a8bdb5da430d773ae1d
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848719"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>用于 ImmutableArrays 的 Roslyn 分析器和代码识别库

[.NET Compiler Platform](https://github.com/dotnet/roslyn) （"Roslyn"）可帮助你构建代码感知库。 代码识别库提供了你可以使用的功能和工具（Roslyn 分析器）来帮助你以最佳方式使用库或避免错误。 本主题说明如何构建真实的 Roslyn 分析器，以便在使用 system.exception NuGet 包时捕获常见[错误。](https://www.nuget.org/packages/System.Collections.Immutable) 该示例还演示了如何为分析器发现的代码问题提供代码修补程序。 用户可以在 Visual Studio 灯泡 UI 中看到代码修复，并可以自动应用代码修补程序。

## <a name="get-started"></a>入门

若要生成此示例，需要以下各项：

* Visual Studio 2015 （非 Express Edition）或更高版本。 你可以使用免费的[Visual Studio 社区版](https://visualstudio.microsoft.com/vs/community/)
* [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。 你还可以在安装 Visual Studio 时，查看 "**常用工具**" 下的**VISUAL STUDIO 扩展性工具**同时安装 SDK。 如果你已经安装了 Visual Studio，则还可以通过转到主菜单**文件**来安装此 SDK > **新建** > **项目**，在**C#** 左侧导航窗格中选择，然后选择 "**扩展性**"。 选择 "**安装 Visual Studio 扩展性工具**" 痕迹导航项目模板时，会提示您下载并安装 SDK。
* [.NET Compiler Platform （"Roslyn"） SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK)。 你还可以通过转到主菜单**文件**来安装此 SDK > **新建** > **项目**，在**C#** 左侧导航窗格中选择，然后选择 "**扩展性**"。 选择 "**下载 .NET COMPILER PLATFORM sdk**" 痕迹导航项目模板时，会提示您下载并安装 sdk。 此 SDK 包括[Roslyn Syntax Visualizer](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer)。 这一有用的工具可帮助你确定应在分析器中查找的代码模型类型。 分析器基础结构针对特定代码模型类型调入您的代码，因此，您的代码仅在必要时才执行，并且只能重点分析相关的代码。

## <a name="whats-the-problem"></a>怎么了？

假设您提供了一个库，其中包含 ImmutableArray （例如 <xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>）支持。 C#开发人员对 .NET 阵列有很多经验。 然而，由于实现中使用的 ImmutableArrays 和优化技术的性质， C#开发人员 intuitions 会导致库用户编写破坏的代码，如下所述。 此外，在运行时，用户不会看到其错误，这不是在 Visual Studio 中通过 .NET 使用的质量经验。

用户熟悉编写如下所示的代码：

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

C#开发人员熟悉如何创建空数组以在后续代码行和使用集合初始值设定项语法的情况下进行填充。 但是，在运行时为 ImmutableArray 崩溃编写相同的代码：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

第一个错误是 ImmutableArray 实现使用结构包装基础数据存储的原因。 结构必须具有无参数的构造函数，以便 `default(T)` 表达式可以返回所有零个或 null 成员的结构。 当代码访问 `b1.Length`时，会出现运行时 null 取消引用错误，因为 ImmutableArray 结构中没有基础存储数组。 `ImmutableArray<int>.Empty`创建空的 ImmutableArray 的正确方法。

发生集合初始值设定项的错误发生的原因是 `ImmutableArray.Add` 方法每次调用该方法时都会返回新实例。 由于 ImmutableArrays 从不会更改，因此当你添加新元素时，你会获得一个新的 ImmutableArray 对象（该对象可能会出于性能原因而共享存储，因为以前存在的 ImmutableArray）。 由于 `b2` 在调用 `Add()` 五次之前指向第一个 ImmutableArray，因此 `b2` 是默认的 ImmutableArray。 它上的调用长度也会因出现空取消引用错误而发生故障。 若要初始化 ImmutableArray 而不手动调用 Add，正确的方法是使用 `ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})`。

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>查找用于触发分析器的相关语法节点类型

 若要开始生成分析器，请首先确定需要查找的 SyntaxNode 类型。 从菜单**视图**启动**Syntax Visualizer** > **其他 Windows** > **Roslyn Syntax Visualizer**。

将编辑器的插入符号放置在声明 `b1`的行上。 你将看到 Syntax Visualizer 显示你处于语法树的 `LocalDeclarationStatement` 节点中。 此节点具有一个 `VariableDeclaration`，后者又具有一个 `VariableDeclarator`，而后者又具有一个 `EqualsValueClause`，最后还有一个 `ObjectCreationExpression`。 单击节点的 Syntax Visualizer 树时，编辑器窗口中的语法将突出显示该节点所表示的代码。 SyntaxNode 子类型的名称与C#语法中使用的名称相匹配。

## <a name="create-the-analyzer-project"></a>创建分析器项目

从主菜单中，选择 "**文件**" > **新建** > **项目**"。 在 "**新建项目**" 对话框中**C#** ，在左侧导航栏中的 "项目" 下，选择 "**扩展性**"，然后在右窗格中选择 "**带有代码修复的分析器**项目" 模板。 输入名称并确认对话框。

该模板将打开*DiagnosticAnalyzer.cs*文件。 选择 "编辑器缓冲区" 选项卡。此文件具有派生自 `DiagnosticAnalyzer` （Roslyn API 类型）的 analyzer 类（格式为你为项目提供的名称）。 新类有一个 `DiagnosticAnalyzerAttribute` 声明 analyzer 与C#语言相关，以便编译器发现和加载分析器。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

您可以使用面向C#代码的 Visual Basic 来实现分析器，反之亦然。 DiagnosticAnalyzerAttribute 中的更重要的是，选择你的分析器是以一种语言还是同时以两者为目标。 更复杂的需要语言详细建模的分析器只能以一种语言为目标。 例如，如果您的分析器仅检查类型名称或公共成员名称，则可以使用公共语言模型 Roslyn 提供的跨 Visual Basic 和C#。 例如，FxCop 警告某个类实现 <xref:System.Runtime.Serialization.ISerializable>，但该类不具有与语言无关的 <xref:System.SerializableAttribute> 属性，适用于 Visual Basic 和C#代码。

## <a name="initialize-the-analyzer"></a>初始化分析器

 在 `DiagnosticAnalyzer` 类中向下滚动一点，以查看 `Initialize` 方法。 当激活分析器时，编译器将调用此方法。 方法采用一个 `AnalysisContext` 对象，该对象允许分析器获取上下文信息，并为要分析的代码类型注册事件的回调。

```csharp
public override void Initialize(AnalysisContext context) {}
```

在此方法中打开新行，然后键入 "context"。 查看 IntelliSense 完成列表。 在完成列表中，可以看到许多 `Register...` 方法来处理各种事件。 例如，第一个 `RegisterCodeBlockAction`为块调用代码，这通常是括在大括号之间的代码。 注册块还会回叫字段的初始值设定项、为属性提供的值或可选参数的值。

作为另一个示例，`RegisterCompilationStartAction`，在编译开始时回叫代码，这在需要在多个位置收集状态时非常有用。 您可以创建数据结构，例如，收集所有使用的符号，每次为某些语法或符号回调您的分析器时，您可以保存有关数据结构中每个位置的信息。 如果由于编译结束而调用了，则可以分析保存的所有位置，例如，从每个 `using` 语句报告代码使用的符号。

使用**Syntax Visualizer**，你已了解到要在编译器处理 ObjectCreationExpression 时调用。 使用此代码设置回调：

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

为语法节点注册并仅筛选对象创建语法节点。 按照约定，在注册操作时，分析器作者使用 lambda，这有助于使分析器保持无状态。 你可以使用 Visual Studio 功能 "**从使用中生成**" 来创建 `AnalyzeObjectCreation` 方法。 这也会为您生成正确类型的上下文参数。

## <a name="set-properties-for-users-of-your-analyzer"></a>设置 analyzer 用户的属性

为了使分析器在 Visual Studio UI 中正确显示，请查找并修改以下代码行来识别你的分析器：

```csharp
internal const string Category = "Naming";
```

更改`"Naming"`到`"API Guidance"`。

接下来，使用**解决方案资源管理器**查找并打开项目中的*资源 .resx*文件。 你可以为你的分析器、标题等提供说明。现在可以将所有这些值的值更改为 `"Don't use ImmutableArray<T> constructor"`。 你可以在字符串中（{0}、{1}等）中放置字符串格式参数，然后在调用 `Diagnostic.Create()`时，可以提供要传递的 `params` 参数数组。

## <a name="analyze-an-object-creation-expression"></a>分析对象创建表达式

`AnalyzeObjectCreation` 方法采用代码分析器框架提供的不同类型的上下文。 `Initialize` 方法的 `AnalysisContext` 允许注册操作回调以设置 analyzer。 例如，`SyntaxNodeAnalysisContext`具有可传递的 `CancellationToken`。 如果用户在编辑器中开始键入内容，Roslyn 将取消正在运行的分析器以节省工作和提高性能。 再如，此上下文有一个节点属性，该属性返回对象创建语法节点。

获取节点，您可以假定该节点是您为其筛选了语法节点操作的类型：

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>首次启动 Visual Studio 和分析器

通过生成并执行分析器来启动 Visual Studio （按**F5**）。 由于**解决方案资源管理器**中的启动项目是 VSIX 项目，因此运行代码将生成代码和 vsix，然后启动安装了该 Vsix 的 Visual Studio。 以这种方式启动 Visual Studio 时，它会以不同的注册表配置单元启动，这样，在构建分析器时，你的测试实例将不会影响你对 Visual Studio 的主要使用。 第一次启动此方法时，Visual Studio 将执行多次初始化，如首次在安装 Visual Studio 后首次启动 Visual Studio 时。

创建一个控制台项目，然后将该数组代码输入到控制台应用程序的 Main 方法中：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

`ImmutableArray` 的代码行具有波形曲线，因为需要获取不可变的 NuGet 包，并将 `using` 语句添加到代码中。 按**解决方案资源管理器**中项目节点上的右指针按钮，然后选择 "**管理 NuGet 包**"。 在 NuGet 管理器中，在 "搜索" 框中键入 "不可变"，然后在左窗格中选择 ""，然后在右窗格中按 "**安装**"**按钮。** 安装包将添加对项目引用的引用。

`ImmutableArray`下仍会出现红色的波形曲线，因此请将插入符号放入该标识符，然后按**Ctrl**+ **。** （period）以显示建议的 "修复" 菜单，并选择添加适当的 `using` 语句。

**全部保存并关闭**Visual Studio 的第二个实例，以使你处于干净状态以继续。

## <a name="finish-the-analyzer-using-edit-and-continue"></a>使用 "编辑并继续" 完成分析器

在 Visual Studio 的第一个实例中，通过在第一行上按**F9** ，在 `AnalyzeObjectCreation` 方法的开头设置断点。

用**F5**再次启动分析器，在 Visual Studio 的第二个实例中，重新打开上次创建的控制台应用程序。

在断点处返回到 Visual Studio 的第一个实例，因为 Roslyn 编译器看到对象创建表达式并将其调用到分析器。

**获取对象创建节点。** 按**F10**来逐过程设置 `objectCreation` 变量的行，并在 "即时"**窗口**中计算表达式 `"objectCreation.ToString()"`。 你会看到变量指向的语法节点是 `"new ImmutableArray<int>()"`的代码，就是你要查找的内容。

**获取 ImmutableArray < T\> 类型对象。** 需要检查正在创建的类型是否为 ImmutableArray。 首先，获取表示此类型的对象。 使用语义模型检查类型以确保具有完全正确的类型，并且不会将字符串与 `ToString()`进行比较。 在函数的末尾输入以下代码行：

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

可在元数据中将泛型类型指定为反撇号（'）和泛型参数的数目。 这就是为什么看不到 ".。。ImmutableArray 在元数据名称中\<T > "。

语义模型有许多有用的功能，可让你提出有关符号、数据流、变量生存期等问题。Roslyn 将语法节点与语义模型分隔开来，以实现多种工程原因（性能、对错误代码进行建模等）。 您希望编译模型查找引用中包含的信息以实现精确比较。

您可以将黄色执行指针拖到编辑器窗口的左侧。 将其拖到设置 `objectCreation` 变量的行上，并使用**F10**逐过程执行新代码行。 如果将鼠标指针悬停在变量 `immutableArrayOfType`上，您将看到在语义模型中找到了精确的类型。

**获取对象创建表达式的类型。** "Type" 在本文中使用几种方法，但这意味着，如果您有 "new Foo" 表达式，则需要获取 Foo 模型。 需要获取对象创建表达式的类型，以查看它是否是 ImmutableArray\<T > 类型。 再次使用语义模型，以获取对象创建表达式中类型符号（ImmutableArray）的符号信息。 在函数的末尾输入以下代码行：

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

由于您的分析器需要在编辑器缓冲区中处理不完整或不正确的代码（例如，缺少 `using` 语句），因此应检查是否 `null``symbolInfo`。 需要从符号信息对象获取命名类型（INamedTypeSymbol）才能完成分析。

**比较类型。** 由于我们要查找的是开放式泛型类型 T，而代码中的类型是具体的泛型类型，因此，你可以在符号信息中查询该类型的构造对象（开放式泛型类型），并将该结果与 `immutableArrayOfTType`进行比较。 在方法的末尾输入以下内容：

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**报告诊断。** 报告诊断非常简单。 在项目模板中使用为你创建的规则，该规则在 Initialize 方法之前定义。 因为代码中的这种情况是错误的，您可以更改已初始化规则的行，以将 `DiagnosticSeverity.Warning` （绿色波形曲线）替换为 `DiagnosticSeverity.Error` （红色波形曲线）。 规则的其余部分将从你在演练开头附近编辑的资源中进行初始化。 还需要报告波形曲线的位置，这是对象创建表达式类型规范的位置。 在 `if` 块中输入以下代码：

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

函数应如下所示（格式可能不同）：

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

删除断点，以便您可以看到您的分析器工作（并停止返回到 Visual Studio 的第一个实例）。 将执行指针拖到方法的开头，并按**F5**继续执行。 切换回 Visual Studio 的第二个实例时，编译器将开始再次检查代码，它将调入分析器。 `ImmutableType<int>`下可以看到波形曲线。

## <a name="adding-a-code-fix-for-the-code-issue"></a>为代码问题添加 "代码修复"

在开始之前，请关闭 Visual Studio 的第二个实例，并在 Visual Studio 的第一个实例（在其中开发分析器）中停止调试。

**添加新类。** 使用**解决方案资源管理器**中的项目节点上的快捷菜单，然后选择 "添加新项"。 添加一个名为 `BuildCodeFixProvider`的类。 此类需要从 `CodeFixProvider`派生，你将需要使用**Ctrl**+ **。** （period）以调用添加正确的 `using` 语句的代码修补程序。 此类还需要使用 `ExportCodeFixProvider` 属性进行批注，你将需要添加 `using` 语句来解析 `LanguageNames` 枚举。 应具有一个类文件，其中包含以下代码：

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**存根派生成员。** 现在，将编辑器的插入符号置于标识符 `CodeFixProvider` 中，然后按**Ctrl**+ **。** （period）将此抽象基类的实现存根。 这会为您生成一个属性和一个方法。

**实现属性。** 用以下代码填写 `FixableDiagnosticIds` 属性的 `get` 正文：

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn 通过将这些标识符（仅是字符串）进行匹配来汇集诊断和修复。 项目模板为你生成了诊断 ID，你可以随时对其进行更改。 属性中的代码只是从 analyzer 类返回 ID。

**RegisterCodeFixAsync 方法使用上下文。** 上下文非常重要，因为代码修补程序可以应用于多个诊断，或者一个代码行中可能存在多个问题。 如果键入 "context"。 在方法的主体中，IntelliSense 完成列表会显示一些有用的成员。 有一个 CancellationToken 成员，你可以检查是否有要取消修复的内容。 有一个文档成员，其中包含许多有用的成员，并允许您访问项目和解决方案模型对象。 有一个范围成员，该成员是你报告诊断时指定的代码位置的开头和结尾。

**使方法是异步的。** 需要做的第一件事是将生成的方法声明修复为 `async` 方法。 即使该方法返回 `Task`，用作存根的代码修补程序也不会包含 `async` 关键字。

**获取语法树的根。** 若要修改代码，你需要生成新的语法树，其中包含你的代码修复所做的更改。 需要上下文中的 `Document` 来调用 `GetSyntaxRootAsync`。 这是一个异步方法，因为有未知的工作要获取语法树，其中可能包括从磁盘获取文件、对其进行分析，并为其生成 Roslyn 代码模型。 在此期间，Visual Studio UI 应是响应的，使用 `async` 会启用此功能。 将方法中的代码行替换为以下代码：

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**查找有问题的节点。** 你传入了上下文的范围，但你找到的节点可能不是必须更改的代码。 报告的诊断仅提供类型标识符（曲线所属于的）的跨度，但您需要替换整个对象创建表达式，包括开头的 `new` 关键字和末尾的括号。 将以下代码添加到方法（并使用**Ctrl**+ **。** 添加 `ObjectCreationExpressionSyntax`的 `using` 语句）：

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**注册灯泡 UI 的代码修复。** 注册代码修补程序时，Roslyn 会自动插入到 Visual Studio 灯泡 UI 中。 最终用户将看到可以使用**Ctrl**+ **。** （period）当分析器波形曲线错误 `ImmutableArray<T>` 构造函数使用时。 由于你的代码修复提供程序仅在出现问题时才会执行，因此你可以假设你有要查找的对象创建表达式。 通过上下文参数，你可以通过将以下代码添加到 `RegisterCodeFixAsync` 方法的末尾来注册新的代码修复：

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

需要将编辑器的插入符号放在标识符中，`CodeAction`，然后使用**Ctrl**+ **。** （period）为此类型添加适当的 `using` 语句。

然后，将编辑器的插入符号置于 `ChangeToImmutableArrayEmpty` 标识符中，并使用**Ctrl**+ **。** 再次为你生成此方法存根。

你添加的最后一个代码片段通过传递 `CodeAction` 和发现的问题类型的诊断 ID 来注册代码修补程序。 在此示例中，此代码仅提供了一个诊断 ID，因此，你可以只传递诊断 Id 数组的第一个元素。 创建 `CodeAction`时，会传入灯泡 UI 应将其用作代码修补说明的文本。 还会传入一个函数，该函数采用 CancellationToken 并返回新文档。 新文档有一个新的语法树，其中包含调用 `ImmutableArray.Empty`的已修复代码。 此代码片段使用 lambda，以便它可以在 objectCreation 节点和上下文的文档中关闭。

**构造新的语法树。** 在之前生成的存根 `ChangeToImmutableArrayEmpty` 方法中，输入代码行： `ImmutableArray<int>.Empty;`。 如果再次查看 " **Syntax Visualizer**工具" 窗口，则可以看到此语法是 SimpleMemberAccessExpression 节点。 这就是此方法需要在新文档中构造和返回的内容。

`ChangeToImmutableArrayEmpty` 的第一次更改是在 `Task<Document>` 之前添加 `async`，因为代码生成器不能假定方法应为 async。

填写包含以下代码的正文，使方法类似于以下代码：

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

需要将编辑器的插入符号放在 `SyntaxGenerator` 标识符中，并使用**Ctrl**+ **。** （period）为此类型添加适当的 `using` 语句。

此代码使用 `SyntaxGenerator`，这是用于构造新代码的有用类型。 获取具有代码问题的文档的生成器后，`ChangeToImmutableArrayEmpty` 调用 `MemberAccessExpression`，同时传递包含要访问的成员的类型，并将该成员的名称作为字符串传递。

接下来，该方法提取文档的根目录，因为这可能涉及一般情况下的任意工作，代码会等待此调用并传递取消标记。 Roslyn 代码模型是不可变的，如使用 .NET 字符串;更新字符串时，将在返回中获取新的字符串对象。 调用 `ReplaceNode`时，将返回一个新的根节点。 大多数语法树都是共享的（因为它是不可变的），但 `objectCreation` 节点会替换为 `memberAccess` 节点，以及所有父节点（直到语法树根）。

## <a name="try-your-code-fix"></a>尝试代码修复

你现在可以按**F5**在 Visual Studio 的第二个实例中执行 analyzer。 打开之前使用的控制台项目。 现在，应会看到灯泡出现在新对象创建表达式用于 `ImmutableArray<int>`的位置。 如果按下**Ctrl**+ **。** （句点）后，你将看到你的代码修复，你会在灯泡 UI 中看到自动生成的代码差异预览。 Roslyn 会为你创建此。

**Pro 提示：** 如果启动 Visual Studio 的第二个实例，但未看到带有代码修补程序的灯泡，则可能需要清除 Visual Studio 组件缓存。 清除缓存会强制 Visual Studio 重新检查组件，因此 Visual Studio 应选取最新的组件。 首先，关闭 Visual Studio 的第二个实例。 然后，在**Windows 资源管理器**中，导航到 *%LOCALAPPDATA%\Microsoft\VisualStudio\16.0Roslyn\\* 。 （"16.0" 从版本更改为版本和 Visual Studio。）删除子目录*ComponentModelCache*。

## <a name="talk-video-and-finish-code-project"></a>讨论视频和完成代码项目

你可以看到本[示例中开发和讨论的此](https://channel9.msdn.com/events/Build/2015/3-725)示例。 此对话演示了工作分析器，并引导您完成构建。

可在[此处](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)查看全部完成的代码。 子文件夹*DoNotUseImmutableArrayCollectionInitializer*和*DoNotUseImmutableArrayCtor*各有一个C#查找问题的文件，以及一个C#实现在 Visual Studio 灯泡 UI 中显示的代码修复的文件。 请注意，完成的代码具有更多的抽象，以避免 ImmutableArray\<T > 类型对象反复提取。 它使用嵌套注册操作将类型对象保存在每次执行 sub 操作（分析对象创建和分析集合初始化）时可用的上下文中。

## <a name="see-also"></a>另请参阅

* [\\\Build 2015 交谈](https://channel9.msdn.com/events/Build/2015/3-725)
* [GitHub 上的已完成代码](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [GitHub 上的几个示例，分为三类分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [GitHub OSS 站点上的其他文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [GitHub 上的 Roslyn 分析器实现的 FxCop 规则](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
