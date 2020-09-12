---
title: 用于 ImmutableArrays 的 Roslyn 分析器和代码识别库
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: db3ebbd289feb227506d8c188ade9261dfb53da2
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037642"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>用于 ImmutableArrays 的 Roslyn 分析器和代码识别库

[.NET Compiler Platform](https://github.com/dotnet/roslyn) ( "Roslyn" ) 可帮助您生成代码感知库。 代码识别库提供了可用于 (Roslyn 分析器) 的功能，以帮助你以最佳方式使用库或避免错误。 本主题说明如何构建真实的 Roslyn 分析器，以便在使用 system.exception NuGet 包时捕获常见[错误。](https://www.nuget.org/packages/System.Collections.Immutable) 该示例还演示了如何为分析器发现的代码问题提供代码修补程序。 用户可以在 Visual Studio 灯泡 UI 中看到代码修复，并可以自动应用代码修补程序。

## <a name="get-started"></a>入门

若要生成此示例，需要以下各项：

* Visual Studio 2015 (速成版) 或更高版本。 你可以使用免费的 [Visual Studio 社区版](https://visualstudio.microsoft.com/vs/community/)
* [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。 你还可以在安装 Visual Studio 时，查看 "**常用工具**" 下的**VISUAL STUDIO 扩展性工具**同时安装 SDK。 如果你已经安装了 Visual Studio，则还可以通过转到主菜单**文件**"  >  **新建**  >  **项目**"，在左侧导航窗格中选择 " **c #** "，然后选择 "**扩展性**" 来安装此 SDK。 选择 "**安装 Visual Studio 扩展性工具**" 痕迹导航项目模板时，会提示您下载并安装 SDK。
* [.NET Compiler Platform ( "Roslyn" ) SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK)。 还可以通过转到主菜单**文件**"  >  **新建**  >  **项目**"，在左侧导航窗格中选择 " **c #** "，然后选择 "**扩展性**" 来安装此 SDK。 选择 "**下载 .NET COMPILER PLATFORM sdk**" 痕迹导航项目模板时，会提示您下载并安装 sdk。 此 SDK 包括 [Roslyn Syntax Visualizer](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Syntax-Visualizer.md)。 这一有用的工具可帮助你确定应在分析器中查找的代码模型类型。 分析器基础结构针对特定代码模型类型调入您的代码，因此，您的代码仅在必要时才执行，并且只能重点分析相关的代码。

## <a name="whats-the-problem"></a>怎么了？

假设你使用 ImmutableArray 提供了一个库 (例如， <xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>) 支持。 C # 开发人员对 .NET 阵列有很多经验。 然而，由于实现中使用的 ImmutableArrays 和优化技术的性质，c # 开发人员 intuitions 会导致库的用户编写中断的代码，如下所述。 此外，在运行时，用户不会看到其错误，这不是在 Visual Studio 中通过 .NET 使用的质量经验。

用户熟悉编写如下所示的代码：

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

C # 开发人员熟悉如何创建空数组以在后续代码行和使用集合初始值设定项语法的情况下进行填充。 但是，在运行时为 ImmutableArray 崩溃编写相同的代码：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

第一个错误是 ImmutableArray 实现使用结构包装基础数据存储的原因。 结构必须具有无参数的构造函数，以便 `default(T)` 表达式可以返回所有零个或 null 成员的结构。 当代码访问时 `b1.Length` ，会出现运行时空取消引用错误，因为 ImmutableArray 结构中没有基础存储数组。 创建空 ImmutableArray 的正确方法是 `ImmutableArray<int>.Empty` 。

发生集合初始值设定项的错误发生的原因是，在 `ImmutableArray.Add` 每次调用该方法时，该方法返回新的实例。 由于 ImmutableArrays 从不会更改，因此当你添加新元素时，你将获得新的 ImmutableArray 对象 (该对象可能会出于性能原因与先前存在的 ImmutableArray) 共享存储。 由于在 `b2` 调用5次之前指向第一个 ImmutableArray `Add()` ，因此 `b2` 是默认的 ImmutableArray。 它上的调用长度也会因出现空取消引用错误而发生故障。 若要初始化 ImmutableArray 而无需手动调用 Add，请使用 `ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})` 。

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>查找用于触发分析器的相关语法节点类型

 若要开始生成分析器，请首先确定需要查找的 SyntaxNode 类型。 从菜单**Syntax Visualizer** **查看**  >  **其他 Windows**  >  **Roslyn Syntax Visualizer**启动 Syntax Visualizer。

将编辑器的插入符号放置在声明的行上 `b1` 。 你将看到 Syntax Visualizer 显示你处于 `LocalDeclarationStatement` 语法树的节点中。 此节点具有一个 `VariableDeclaration` ，而后者又具有， `VariableDeclarator` `EqualsValueClause` 最后有一个 `ObjectCreationExpression` 。 单击节点的 Syntax Visualizer 树时，编辑器窗口中的语法将突出显示该节点所表示的代码。 SyntaxNode 子类型的名称与 c # 语法中使用的名称相匹配。

## <a name="create-the-analyzer-project"></a>创建分析器项目

从主菜单中，选择 "**文件**" "  >  **新建**  >  **项目**"。 在 " **新建项目** " 对话框中，在左侧导航栏中的 " **c #** 项目" 下，选择 " **扩展性**"，然后在右窗格中选择 " **带有代码修复的分析器** 项目" 模板。 输入名称并确认对话框。

该模板将打开 *DiagnosticAnalyzer.cs* 文件。 选择 "编辑器缓冲区" 选项卡。此文件的分析器类 (从你为该项目提供的名称构成，该项目) 派生自 `DiagnosticAnalyzer` (ROSLYN API 类型) 。 新类具有 `DiagnosticAnalyzerAttribute` 声明分析器与 c # 语言相关的，以便编译器可以发现和加载分析器。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

您可以使用面向 c # 代码的 Visual Basic 来实现分析器，反之亦然。 DiagnosticAnalyzerAttribute 中的更重要的是，选择你的分析器是以一种语言还是同时以两者为目标。 更复杂的需要语言详细建模的分析器只能以一种语言为目标。 例如，如果您的分析器仅检查类型名称或公共成员名称，则可以在 Visual Basic 和 c # 之间使用公共语言模型 Roslyn 提供程序。 例如，FxCop 警告类实现的 <xref:System.Runtime.Serialization.ISerializable> ，但类不具有与 <xref:System.SerializableAttribute> 语言无关的属性，并且适用于 Visual Basic 和 c # 代码。

## <a name="initialize-the-analyzer"></a>初始化分析器

 在类中向下滚动一点 `DiagnosticAnalyzer` 来查看 `Initialize` 方法。 当激活分析器时，编译器将调用此方法。 方法采用一个 `AnalysisContext` 对象，该对象允许分析器获取上下文信息，并为要分析的代码类型注册事件的回调。

```csharp
public override void Initialize(AnalysisContext context) {}
```

在此方法中打开新行，然后键入 "context"。 查看 IntelliSense 完成列表。 在完成列表中可以看到，有许多 `Register...` 方法可处理各种类型的事件。 例如，第一个 `RegisterCodeBlockAction` 代码块返回到代码中的块，这通常是大括号之间的代码。 注册块还会回叫字段的初始值设定项、为属性提供的值或可选参数的值。

作为另一个示例，在 `RegisterCompilationStartAction` 编译开始时回叫代码，这在需要在多个位置收集状态时非常有用。 您可以创建数据结构，例如，收集所有使用的符号，每次为某些语法或符号回调您的分析器时，您可以保存有关数据结构中每个位置的信息。 如果由于编译结束而调用了，则可以分析保存的所有位置，例如，从每个语句报告代码使用的符号 `using` 。

使用 **Syntax Visualizer**，你已了解到要在编译器处理 ObjectCreationExpression 时调用。 使用此代码设置回调：

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

为语法节点注册并仅筛选对象创建语法节点。 按照约定，在注册操作时，分析器作者使用 lambda，这有助于使分析器保持无状态。 你可以使用 Visual Studio 的 " **从使用中生成** " 功能创建 `AnalyzeObjectCreation` 方法。 这也会为您生成正确类型的上下文参数。

## <a name="set-properties-for-users-of-your-analyzer"></a>设置 analyzer 用户的属性

为了使分析器在 Visual Studio UI 中正确显示，请查找并修改以下代码行来识别你的分析器：

```csharp
internal const string Category = "Naming";
```

将 `"Naming"` 更改为 `"API Guidance"`。

接下来，使用**解决方案资源管理器**查找并打开项目中的*资源 .resx*文件。 你可以为你的分析器、标题等提供说明。你现在可以将所有这些值的值都更改为 `"Don't use ImmutableArray<T> constructor"` 。 你可以在字符串中将字符串格式设置参数 ({0} 、等 {1} ) ，然后在调用时 `Diagnostic.Create()` ，可以提供 `params` 要传递的参数数组。

## <a name="analyze-an-object-creation-expression"></a>分析对象创建表达式

`AnalyzeObjectCreation`方法采用代码分析器框架提供的不同类型的上下文。 `Initialize`方法 `AnalysisContext` 允许注册操作回调以设置分析器。 `SyntaxNodeAnalysisContext`例如，具有 `CancellationToken` 可以传递的。 如果用户在编辑器中开始键入内容，Roslyn 将取消正在运行的分析器以节省工作和提高性能。 再如，此上下文有一个节点属性，该属性返回对象创建语法节点。

获取节点，您可以假定该节点是您为其筛选了语法节点操作的类型：

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>首次启动 Visual Studio 和分析器

通过生成并执行分析器来启动 Visual Studio (按 **F5**) 。 由于 **解决方案资源管理器** 中的启动项目是 VSIX 项目，因此运行代码将生成代码和 vsix，然后启动安装了该 Vsix 的 Visual Studio。 以这种方式启动 Visual Studio 时，它会以不同的注册表配置单元启动，这样，在构建分析器时，你的测试实例将不会影响你对 Visual Studio 的主要使用。 第一次启动此方法时，Visual Studio 将执行多次初始化，如首次在安装 Visual Studio 后首次启动 Visual Studio 时。

创建一个控制台项目，然后将该数组代码输入到控制台应用程序的 Main 方法中：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

`ImmutableArray`由于需要获取不可变 NuGet 包并向代码添加语句，因此具有波形曲线的代码行 `using` 。 按 **解决方案资源管理器** 中项目节点上的右指针按钮，然后选择 " **管理 NuGet 包**"。 在 NuGet 管理器中，在 "搜索" 框中键入 "不可变"，然后选择项 " **system.object** (不要在左窗格中) 选择" "，然后按右窗格中的"**安装** **"按钮。** 安装包将添加对项目引用的引用。

在下仍会看到红色波形曲线 `ImmutableArray` ，因此请将插入符号置于该标识符中，然后按**Ctrl**键 + **。**  ("时间段") 以显示建议的 "修复" 菜单，并选择添加相应的 `using` 语句。

**全部保存并关闭** Visual Studio 的第二个实例，以使你处于干净状态以继续。

## <a name="finish-the-analyzer-using-edit-and-continue"></a>使用 "编辑并继续" 完成分析器

在 Visual Studio 的第一个实例中， `AnalyzeObjectCreation` 通过在第一行上按 **F9** 并使用插入符号，在方法的开头设置断点。

用 **F5**再次启动分析器，在 Visual Studio 的第二个实例中，重新打开上次创建的控制台应用程序。

在断点处返回到 Visual Studio 的第一个实例，因为 Roslyn 编译器看到对象创建表达式并将其调用到分析器。

**获取对象创建节点。** `objectCreation`按**F10**，然后在 "**即时" 窗口**中对表达式进行求值 `"objectCreation.ToString()"` 。 您可以看到，变量指向的语法节点是代码 `"new ImmutableArray<int>()"` ，就是您要查找的内容。

**获取 ImmutableArray<T \> 类型对象。** 需要检查正在创建的类型是否为 ImmutableArray。 首先，获取表示此类型的对象。 使用语义模型检查类型以确保具有完全正确的类型，而不是将字符串与进行比较 `ToString()` 。 在函数的末尾输入以下代码行：

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

可在元数据中指定泛型类型，将反撇号 (") 和泛型参数的数目。 这就是为什么看不到 ".。。ImmutableArray \<T> "。

语义模型有许多有用的功能，可让你提出有关符号、数据流、变量生存期等问题。Roslyn 将语义模型中的语法节点与各种工程原因（ (性能、) 错误代码等）分隔开来。 您希望编译模型查找引用中包含的信息以实现精确比较。

您可以将黄色执行指针拖到编辑器窗口的左侧。 将其拖动到 `objectCreation` 使用 **F10**设置变量并单步执行新代码行的行上。 如果将鼠标指针悬停在该变量上 `immutableArrayOfType` ，会看到我们在语义模型中找到了确切的类型。

**获取对象创建表达式的类型。** "Type" 在本文中使用几种方法，但这意味着，如果您有 "new Foo" 表达式，则需要获取 Foo 模型。 你需要获取对象创建表达式的类型，以确定它是否为 ImmutableArray \<T> 类型。 再次使用语义模型，以获取对象创建表达式中的类型符号 (ImmutableArray) 的符号信息。 在函数的末尾输入以下代码行：

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

由于分析器需要在编辑器缓冲区中处理不完整或不正确的代码 (例如， `using`) 缺少语句，因此应检查是否为 `symbolInfo` `null` 。 需要从符号信息对象获取命名类型 (INamedTypeSymbol) ，以完成分析。

**比较类型。** 由于我们要查找的是开放式泛型类型 T，而代码中的类型是具体的泛型类型，因此，你可以从 (开放式泛型类型中查询要构造的类型的符号信息) 并将该结果与进行比较 `immutableArrayOfTType` 。 在方法的末尾输入以下内容：

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**报告诊断。** 报告诊断非常简单。 在项目模板中使用为你创建的规则，该规则在 Initialize 方法之前定义。 因为代码中的这种情况是错误的，您可以更改已初始化规则的行以替换 `DiagnosticSeverity.Warning` (绿色波形曲线) 并 `DiagnosticSeverity.Error` (红色波形曲线) 。 规则的其余部分将从你在演练开头附近编辑的资源中进行初始化。 还需要报告波形曲线的位置，这是对象创建表达式类型规范的位置。 在块中输入以下代码 `if` ：

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

函数应类似于此 (的格式可能不同) ：

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

删除断点，使你可以查看 (的分析器工作，并停止返回到 Visual Studio 的第一个实例) 。 将执行指针拖到方法的开头，并按 **F5** 继续执行。 切换回 Visual Studio 的第二个实例时，编译器将开始再次检查代码，它将调入分析器。 可以在下看到一个波形曲线 `ImmutableType<int>` 。

## <a name="adding-a-code-fix-for-the-code-issue"></a>为代码问题添加 "代码修复"

在开始之前，请关闭 Visual Studio 的第二个实例，并在 Visual Studio (的第一个实例中停止调试，) 在其中开发分析器。

**添加新类。** 使用快捷菜单 (鼠标右键在 **解决方案资源管理器** 项目节点上) ，然后选择 "添加新项"。 添加一个名为的类 `BuildCodeFixProvider` 。 此类需要从派生 `CodeFixProvider` ，并且您需要使用**Ctrl** + **。**  (period) 调用添加正确语句的代码修补程序 `using` 。 此类还需要使用特性进行批注 `ExportCodeFixProvider` ，你将需要添加 `using` 语句来解析 `LanguageNames` 枚举。 应具有一个类文件，其中包含以下代码：

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**存根派生成员。** 现在，将编辑器的插入符号放置在标识符中， `CodeFixProvider` 然后按**Ctrl**键 + **。**  (period) 为此抽象基类的实现提供存根。 这会为您生成一个属性和一个方法。

**实现属性。** `FixableDiagnosticIds` `get` 用以下代码填充属性的主体：

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn 通过将这些标识符（仅是字符串）进行匹配来汇集诊断和修复。 项目模板为你生成了诊断 ID，你可以随时对其进行更改。 属性中的代码只是从 analyzer 类返回 ID。

**RegisterCodeFixAsync 方法使用上下文。** 上下文非常重要，因为代码修补程序可以应用于多个诊断，或者一个代码行中可能存在多个问题。 如果键入 "context"。 在方法的主体中，IntelliSense 完成列表会显示一些有用的成员。 有一个 CancellationToken 成员，你可以检查是否有要取消修复的内容。 有一个文档成员，其中包含许多有用的成员，并允许您访问项目和解决方案模型对象。 有一个范围成员，该成员是你报告诊断时指定的代码位置的开头和结尾。

**使方法是异步的。** 需要做的第一件事是将生成的方法声明修复为 `async` 方法。 即使该方法返回，用作存根的代码修补程序也不会包含 `async` 关键字，即使该方法返回 `Task` 。

**获取语法树的根。** 若要修改代码，你需要生成新的语法树，其中包含你的代码修复所做的更改。 需要 `Document` 从上下文调用 `GetSyntaxRootAsync` 。 这是一个异步方法，因为有未知的工作要获取语法树，其中可能包括从磁盘获取文件、对其进行分析，并为其生成 Roslyn 代码模型。 在此期间，Visual Studio UI 应是响应的，使用 `async` 启用。 将方法中的代码行替换为以下代码：

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**查找有问题的节点。** 你传入了上下文的范围，但你找到的节点可能不是必须更改的代码。 报告的诊断仅提供了曲线) 的的类型标识符 (范围，但是需要替换整个对象创建表达式，包括 `new` 开头的关键字和末尾的括号。 将以下代码添加到 (方法，并使用**Ctrl** + **。** 为) 添加 `using` 语句 `ObjectCreationExpressionSyntax` ：

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**注册灯泡 UI 的代码修复。** 注册代码修补程序时，Roslyn 会自动插入到 Visual Studio 灯泡 UI 中。 最终用户将看到他们可以使用**Ctrl** + **。** 当分析器波形曲线不正确的构造函数时，)  (时间段 `ImmutableArray<T>` 。 由于你的代码修复提供程序仅在出现问题时才会执行，因此你可以假设你有要查找的对象创建表达式。 在上下文参数中，可以通过将以下代码添加到方法的末尾来注册新的代码修复 `RegisterCodeFixAsync` ：

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

需要将编辑器的插入符号放在标识符中， `CodeAction` 然后使用**Ctrl 键** + **。** 为此类型添加适当语句)  (时间段 `using` 。

然后，将编辑器的插入符号放置在 `ChangeToImmutableArrayEmpty` 标识符中，并使用**Ctrl 键** + **。** 再次为你生成此方法存根。

最后添加的代码片段通过为 `CodeAction` 找到的问题类型传递和诊断 ID 来注册代码修补程序。 在此示例中，此代码仅提供了一个诊断 ID，因此，你可以只传递诊断 Id 数组的第一个元素。 当你创建时 `CodeAction` ，会传入灯泡 UI 应将其用作代码修补说明的文本。 还会传入一个函数，该函数采用 CancellationToken 并返回新文档。 新文档有一个新的语法树，其中包含所调用的已修复代码 `ImmutableArray.Empty` 。 此代码片段使用 lambda，以便它可以在 objectCreation 节点和上下文的文档中关闭。

**构造新的语法树。** 在 `ChangeToImmutableArrayEmpty` 之前生成的存根的方法中，输入代码行： `ImmutableArray<int>.Empty;` 。 如果再次查看 " **Syntax Visualizer** 工具" 窗口，则可以看到此语法是 SimpleMemberAccessExpression 节点。 这就是此方法需要在新文档中构造和返回的内容。

第一次更改 `ChangeToImmutableArrayEmpty` 是 `async` 在之前添加， `Task<Document>` 因为代码生成器不能假定方法应为 async。

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

需要将编辑器的插入符号放在 `SyntaxGenerator` 标识符中，并使用**Ctrl 键** + **。** 为此类型添加适当语句)  (时间段 `using` 。

此代码使用 `SyntaxGenerator` ，这是用于构造新代码的有用类型。 获取具有代码问题的文档的生成器后， `ChangeToImmutableArrayEmpty` 调用 `MemberAccessExpression` ，传递包含要访问的成员的类型，并将成员的名称作为字符串传递。

接下来，该方法提取文档的根目录，因为这可能涉及一般情况下的任意工作，代码会等待此调用并传递取消标记。 Roslyn 代码模型是不可变的，如使用 .NET 字符串;更新字符串时，将在返回中获取新的字符串对象。 调用时 `ReplaceNode` ，将返回一个新的根节点。 大多数语法树是 (共享的，因为它是不可变的) ，但 `objectCreation` 节点被替换为 `memberAccess` 节点，以及所有父节点（直到语法树根）。

## <a name="try-your-code-fix"></a>尝试代码修复

你现在可以按 **F5** 在 Visual Studio 的第二个实例中执行 analyzer。 打开之前使用的控制台项目。 现在应会看到灯泡出现在新对象创建表达式的位置 `ImmutableArray<int>` 。 按 Ctrl 键**Ctrl** + **。** )  (期间，你将看到你的代码修复，你会在灯泡 UI 中看到自动生成的代码差异预览。 Roslyn 会为你创建此。

**Pro 提示：** 如果启动 Visual Studio 的第二个实例，但未看到带有代码修补程序的灯泡，则可能需要清除 Visual Studio 组件缓存。 清除缓存会强制 Visual Studio 重新检查组件，因此 Visual Studio 应选取最新的组件。 首先，关闭 Visual Studio 的第二个实例。 然后，在**Windows 资源管理器**中，导航到 *%LOCALAPPDATA%\Microsoft\VisualStudio\16.0Roslyn \\ *。  ("16.0" 从版本更改为版本和 Visual Studio。 ) 删除子目录 *ComponentModelCache*。

## <a name="talk-video-and-finish-code-project"></a>讨论视频和完成代码项目

你可以看到本 [示例中开发和讨论的此](https://channel9.msdn.com/events/Build/2015/3-725)示例。 此对话演示了工作分析器，并引导您完成构建。

可在 [此处](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)查看全部完成的代码。 子文件夹 *DoNotUseImmutableArrayCollectionInitializer* 和 *DoNotUseImmutableArrayCtor* 各有一个 c # 文件，用于查找问题和一个 c # 文件，用于实现在 Visual Studio 灯泡 UI 中显示的代码修复。 请注意，已完成的代码具有更多抽象，以避免反复获取 ImmutableArray \<T> 类型对象。 它使用嵌套注册操作将类型对象保存在上下文中，每当子操作 (分析对象创建和分析) 执行的集合初始化时可用。

## <a name="see-also"></a>另请参阅

* [\\\Build 2015 交谈](https://channel9.msdn.com/events/Build/2015/3-725)
* [GitHub 上的已完成代码](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [GitHub 上的几个示例，分为三类分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [GitHub OSS 站点上的其他文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [GitHub 上的 Roslyn 分析器实现的 FxCop 规则](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
