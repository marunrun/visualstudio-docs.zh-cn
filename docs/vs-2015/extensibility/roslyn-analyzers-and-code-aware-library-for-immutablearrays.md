---
title: Roslyn 分析器和 immutablearrays 的代码识别库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 44cb171594a6d595652b3c013505927bd82f947e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685245"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>Roslyn 分析器和 ImmutableArrays 的代码识别库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[.NET 编译器平台](https://github.com/dotnet/roslyn)("Roslyn") 可帮助您生成可识别代码的库。 代码识别库提供了可以使用的功能和工具 （Roslyn 分析器），以帮助你使用库以最佳方式，或若要避免错误。 本主题说明如何构建真实世界 Roslyn 分析器来捕获常见的错误时使用[NIB:不可变集合](https://msdn.microsoft.com/library/33f4449d-7078-450a-8d60-d9229f66bbca)NuGet 包。 该示例还演示如何为分析器发现的代码问题提供代码修补程序。 用户看到在 Visual Studio 灯泡 UI 中的代码修补程序，并可以自动应用代码修复。

## <a name="getting-started"></a>入门
需要以下内容以生成此示例中：

- Visual Studio 2015 (非 Express Edition) 或更高版本。 您可以使用免费[Visual Studio Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs)

- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。 您还可以在安装 Visual Studio 中，检查在常见的工具在同一时间安装 SDK 的 Visual Studio 扩展性工具。 如果已安装 Visual Studio，还可以通过转到主菜单中安装此 SDK**文件&#124;新建&#124;项目...**，在左侧的导航窗格中，选择 C#，然后选择可扩展性。 当你选择"**安装 Visual Studio 扩展性工具**"痕迹导航项目模板，它会提示你下载并安装 SDK。

- [.NET 编译器平台 ("Roslyn") SDK](https://aka.ms/roslynsdktemplates)。 此外可以安装此 SDK，通过转到主菜单**文件&#124;新建&#124;项目...**，选择**C#** 中的左侧的导航窗格中，和然后选择**扩展性**。 当你选择"**下载.NET Compiler Platform SDK**"痕迹导航项目模板，它会提示你下载并安装 SDK。 此 SDK 包括[Roslyn 语法可视化工具](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer)。 找出哪些代码模型类型这非常有用的工具可以帮助您应查找在您的分析器。 对于特定的代码模型类型，因此你的代码仅在必要时执行，并可以专注于仅分析相关的代码在代码分析工具基础结构调用。

## <a name="whats-the-problem"></a>怎么了？
假设一个库提供 ImmutableArray (例如， <xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>) 支持。 C# 开发人员有很多的经验.NET 数组。 但是，由于在实现中使用 ImmutableArrays 和优化技术的特性，C# 开发人员 intuitions 会导致你的库的用户编写断开的代码，如下所述。 此外，用户不会看到其错误到运行时，这并不到 Visual Studio 中通过.NET 使用高质量体验。

用户熟悉编写如下代码：

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);

```

创建空的数组进行填充后续行代码和使用集合初始值设定项语法是 C# 开发人员非常熟悉。 但是，编写相同在运行时崩溃 ImmutableArray 的代码：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);

```

第一个错误是由于 ImmutableArray 实现使用结构来包装基础数据存储。 结构必须具有无参数构造函数，以便`default(T)`表达式可以返回所有的结构为零或 null 的成员。 代码访问时`b1.Length`，没有运行的时为 null 取消引用错误，因为没有基础的存储阵列没有 ImmutableArray 结构中。 若要创建空的 ImmutableArray 的正确方式是`ImmutableArray<int>.Empty`。

 集合初始值设定项的错误是因为 ImmutableArray.Add 方法将返回新的实例每次调用它。 因为永远不会更改 ImmutableArrays，添加新元素时，你获得新的 ImmutableArray 对象 （这可能会与先前存在的 ImmutableArray 共享存储，出于性能原因）。 因为`b2`指向第一个然后再调用 ImmutableArray`Add()`五次，`b2`是默认值 ImmutableArray。 长度上调用它还具有空的崩溃取消引用错误。 初始化 ImmutableArray 不用的情况下手动调用添加要使用的正确方法`ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})`。

## <a name="finding-relevant-syntax-node-types-to-trigger-your-analyzer"></a>查找相关的语法节点类型，以触发您的分析器
若要开始生成分析器，首先找出您需要查找哪种类型的 SyntaxNode。   启动菜单中，语法可视化工具**视图&#124;其他 Windows &#124; Roslyn 语法可视化工具**。

将编辑器插入点放在声明的行`b1`。 你将看到语法可视化工具显示在`LocalDeclarationStatement`语法树的节点。 此节点有`VariableDeclaration`，进而拥有`VariableDeclarator`，该子元素又具有`EqualsValueClause`，最后是`ObjectCreationExpression`。 单击在语法可视化工具树中的节点时，在编辑器窗口中的语法突出显示了以显示该节点表示的代码。 SyntaxNode 子类型的名称匹配的 C# 语法中使用的名称。

## <a name="creating-the-analyzer-project"></a>创建分析器项目
从主菜单中选择**文件&#124;新建&#124;项目...**. 在中**新的项目**对话框下**C#** 项目在左侧的导航栏中，选择可扩展性，然后在右窗格中选择**分析器与代码修复**项目模板。 输入的名称和确认对话框。

该模板打开 DiagnosticAnalyzer.cs 文件。 选择该编辑器缓冲区选项卡。此文件具有一个分析器类 (格式为项目指定的名称) 派生`DiagnosticAnalyzer`（Roslyn API 类型）。 你的新类`DiagnosticAnalyzerAttribute`声明您的分析器是与 C# 语言，以便编译器发现并加载您的分析器。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

您可以实现使用以 C# 代码中，为目标的 Visual Basic 的分析器，反之亦然。 它是 DiagnosticAnalyzerAttribute 选择您的分析器以目标和 / 或一种语言中，更重要。 更复杂的分析器，需要详细的建模语言的仅可具有一种语言。 如果您的分析器，例如，仅会检查类型名称或公共成员的名称，它可能可以使用 Roslyn，在 Visual Basic 和 C# 提供通用的语言模型。 例如，FxCop 会警告类将实现<xref:System.Runtime.Serialization.ISerializable>，但类没有<xref:System.SerializableAttribute>属性独立于语言的且适用于 Visual Basic 和 C# 代码。

## <a name="initalizing-the-analyzer"></a>初始化分析器
向下滚动一点`DiagnosticAnalyzer`类来了解`Initialize`方法。 激活分析器时，编译器将调用此方法。 该方法采用`AnalysisContext`对象，它使您的分析器以获取上下文信息并注册回调的事件的类型的你想要分析的代码。

```csharp
public override void Initialize(AnalysisContext context) {}
```

打开一个新行方法和类型"在此上下文中。" 若要查看的 Intellisense 完成列表。 您可以看到在完成列表中有许多`Register…`方法来处理各种类型的事件。 例如，第一个`RegisterCodeBlockAction`，回调到您的代码块，这通常是大括号之间的代码。 注册为块还调用返回到你的代码字段，提供给属性的值或可选参数的值的初始值设定项。

另举一例， `RegisterCompilationStartAction`，返回到你的代码开头的编译时，这很有用，当您需要通过多个位置收集状态时调用。 您可以创建一个数据结构，即收集所有符号，并每次您的分析器的某些语法或符号，调用时返回可以将有关每个位置的信息保存在您的数据结构。 您正在调用时返回由于编译结束，可以分析您保存，例如，若要报告的代码使用从每个符号的所有位置`using`语句。

使用**语法可视化工具**，您学习了你想要在编译器处理 ObjectCreationExpression 时调用。 此代码用于设置回调：

```csharp

context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

注册了语法节点和仅对象创建语法节点的筛选器。 按照约定，分析器作者使用的 lambda 时注册操作，这有助于保护分析器无状态。 可以使用 Visual Studio 功能**根据使用情况生成**若要创建`AnalyzeObjectCreation`方法。 这也为你将生成上下文参数的正确的类型。

## <a name="setting-properties-for-users-of-your-analyzer"></a>您的分析器的用户设置属性
以便在您的分析器在 Visual Studio UI 中相应地，查找并修改以下一行代码，以确定您的分析器：

```csharp
internal const string Category = "Naming";
```

更改`"Naming"`到`"API Guidance"`。

接下来找到并打开 Resources.resx 文件在你项目中使用**解决方案资源管理器**。 您可以为您的分析器、 标题等设置说明。所有这些对象可以更改值`“Don’t use ImmutableArray<T> constructor”`现在。 可以将字符串格式设置字符串中的参数 ({0}，{1}等)，并在调用时，更高版本`Diagnostic.Create()`，可以提供要传递的参数的参数数组。

## <a name="analyzing-an-object-creation-expression"></a>分析对象创建表达式
`AnalyzeObjectCreation`方法采用不同类型的代码分析器框架所提供的上下文。 Initialize 方法`AnalysisContext`允许注册操作回调以设置您的分析器。 `SyntaxNodeAnalysisContext`，例如，具有`CancellationToken`，可以传递。 如果用户开始在编辑器中键入，Roslyn 将取消正在运行的分析器保存工作并提高性能。 作为另一个示例中，此上下文中的返回对象创建语法节点的节点属性。

获取节点，可以假定是为其筛选语法节点操作的类型：

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launching-visual-studio-with-your-analyzer-the-first-time"></a>启动 Visual Studio 中使用您的分析器第一次
通过构建和执行您的分析器，启动 Visual Studio (按**F5**)。 因为在项目启动**解决方案资源管理器**是 VSIX 项目，你的代码和 VSIX，运行你的代码生成，并启动 Visual Studio 中使用该 VSIX 安装。 以这种方式启动 Visual Studio，以便主要使用的 Visual Studio 将不会影响你的测试实例在构建分析器时它将启动具有独特的注册表配置单元中。 首次启动这样一来，Visual Studio 执行类似于当您首次启动 Visual Studio 安装完成后的几个初始化。

 创建控制台项目，然后在控制台应用程序的 Main 方法中输入数组代码：

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);

```

代码行`ImmutableArray`具有波形曲线，因为您需要获取不可变的 NuGet 包并添加`using`到你的代码语句。 中的项目节点上按右指针按钮**解决方案资源管理器**，然后选择**管理 NuGet 包...**. 在 NuGet 管理器中，到搜索框中，键入"不可变"并选择项"System.Collections.Immutable"（不选择"Microsoft.Bcl.Immutable"） 中的左的窗格和按右窗格中安装按钮。 安装包添加到你的项目引用的引用。

你仍看到下的红色波形曲线`ImmutableArray`，因此将光标置于该标识符和按**CTRL +。** （句点），以便显示建议的修复方法菜单并选择以添加适当`using`语句。

**全部保存并关闭**Visual Studio 现在处于干净状态，以便继续将您的第二个实例。

## <a name="finishing-the-analyzer-using-edit-and-continue"></a>完成分析器使用编辑并继续
在 Visual Studio 的第一个实例，设置断点的开头你`AnalyzeObjectCreation`方法通过按**F9**和脱字号的第一行上。

启动您的分析器使用再次**F5**，并在 Visual Studio 的第二个实例中，重新打开控制台应用程序创建最后一次。

因为 Roslyn 编译器看到对象创建表达式和到您的分析器调用，返回到 Visual Studio 的第一个实例在断点处。

**获取对象创建节点。** 单步跳过设置的行`objectCreation`按变量**F10**，然后在**即时窗口**计算表达式`“objectCreation.ToString()”`。 您看到变量指向的语法节点是代码`"new ImmutableArray<int>()"`，只你要查找的内容。

**获取 ImmutableArray\<T > 类型对象。** 您需要检查是否正在创建的类型为 ImmutableArray。 首先，获取表示此类型的对象。 检查类型使用语义模型来确保已完全正确的类型，并且不比较 tostring （） 中的字符串。 输入在函数末尾的代码的以下行：

```csharp

var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");

```

将指定泛型类型中具有 backquotes （'） 的元数据和泛型参数的数目。 这就是为什么你看不到"...ImmutableArray\<T >"中的元数据名称。

语义模型具有许多有用的操作对其允许您提出有关符号、 数据流、 变量的生存期，等等的问题。Roslyn 出于各种工程原因 （性能，建模错误代码，等等） 将与语义模型的语法节点。 你想要查找的精确比较引用中包含的信息的编译模型。

您可以在编辑器窗口的左侧拖动黄色执行指针。 将它设置的行向上拖动`objectCreation`变量和单步跳过的代码使用你新行**F10**。 如果鼠标指针悬停在变量`immutableArrayOfType`，您看到我们在语义模型中找到的确切类型。

**获取对象创建表达式的类型。** 在本文中，通过多种方式使用"类型"，但这意味着如果您具有"新 Foo"表达式中，您需要先获取 Foo 的模型。 您需要获取其类型的对象创建表达式，以查看它是否 ImmutableArray\<T > 类型。 再次使用语义模型对象创建表达式中获取类型符号 (ImmutableArray) 的符号信息。 输入在函数末尾的代码的以下行：

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type) as INamedTypeSymbol;

```

因为您的分析器需要处理不完整或不正确的代码编辑器缓冲区中 (例如，缺少`using`语句)，应检查`symbolInfo`正在`null`。 您需要先获取一个已命名的类型 (INamedTypeSymbol) 从符号信息对象来完成分析。

**比较类型。** 因为我们正在寻找，T 的开放式泛型类型，并且在代码中的类型是一个具体的泛型类型，您将查询从 （开放式泛型类型） 构造的类型的符号信息和比较该结果与`immutableArrayOfTType`。 输入以下内容的方法的末尾：

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**报告诊断。** 报告诊断是相当容易。 使用在之前的初始化方法定义的项目模板中为你创建的规则。 由于这种情况下在代码中时出现错误，您可以更改初始化规则要替换的行`DiagnosticSeverity.Warning`（绿色波浪线） 与`DiagnosticSeverity.Error`（红色波形曲线）。 该规则的其余部分初始化从本演练的开始编辑的资源。 您还需要报告波浪线，对象创建表达式的类型规范的位置的位置。 输入此代码`if`块：

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

你的函数应如下所示 （以不同的方式可能是格式）：

```csharp
private void AnalyzeObjectCreation(SyntaxNodeAnalysisContext context)
{
    var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
    var immutableArrayOfTType =
        context.SemanticModel
               .Compilation
               .GetTypeByMetadataName(
                   "System.Collections.Immutable.ImmutableArray`1");
    var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type) as
        INamedTypeSymbol;
    if (symbolInfo != null &&
        symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
    {
        context.ReportDiagnostic(
            Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
    }
}

```

删除断点，以便你可以查看您的分析器运行 （和停止返回到 Visual Studio 的第一个实例）。 将执行指针拖到开头的方法，并按**F5**继续执行。 在切换回 Visual Studio 的第二个实例时，编译器将开始再次检查的代码，它将调用您的分析器。 您可以看到波浪线下的`ImmutableType<int>`。

## <a name="adding-a-code-fix-for-the-code-issue"></a>将"代码修补程序"添加代码问题
在开始之前，关闭 Visual Studio 的第二个实例，并停止在 Visual Studio （其中正在开发分析器） 的第一个实例中进行调试。

**添加新类。** 在解决方案资源管理器中的项目节点上使用的快捷菜单 （右指针按钮） 并选择以添加新项。 添加一个名为类`BuildCodeFixProvider`。 此类必须派生自`CodeFixProvider`，并将需要使用**CTRL +。** （句点） 来调用将添加正确的代码修复`using`语句。 此类还需要使用批注`ExportCodeFixProvider`特性，并且你将需要添加`using`语句，以解决`LanguageNames`枚举。 您应该使用以下代码在其中一个类文件：

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}

```

**去掉派生的成员。** 现在，将编辑器插入点放在标识符中`CodeFixProvider`按**CTRL +。** （句点） 以派生出此抽象基类的实现。 这将为您生成的属性和方法。

**实现的属性。** 填写`FixableDiagnosticIds`属性的`get`正文使用以下代码：

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn 汇集了诊断和修复的匹配这些都是字符串的标识符。 项目模板生成诊断 ID，并可随意对其进行更改。 在属性中的代码只需从分析器类返回的 ID。

**RegisterCodeFixAsync 方法采用上下文。** 上下文非常重要，因为代码修补程序，可以将应用于多个诊断，或在代码行上可能有多个问题。 如果键入"上下文。" 在该方法的正文中，Intellisense 完成列表将演示一些有用的成员。 没有可以检查以查看的内容是否想取消解决方法的 CancellationToken 成员。 没有文档成员有很多有用的成员并使你能够获取对项目和解决方案模型对象。 S p a n 成员开头并且末尾的代码位置指定将报告诊断。

**将此方法是异步的。** 需要执行的第一件事是修复生成的方法声明为`async`方法。 不包括抽象类的实现将用作存根的代码修复`async`关键字，即使该方法将返回`Task`。

**获取语法树的根。** 若要修改的代码生成新的语法树的更改所需代码修补程序使。 所需`Document`要调用的上下文从`GetSyntaxRootAsync`。 这是异步方法，因为没有未知的操作来获取语法树中，可能包括从磁盘中获取文件、 分析，以及为其生成 Roslyn 代码模型。 在 Visual Studio UI 应在此期间，哪些使用快速地响应`async`启用。 使用以下内容替换方法中的代码行：

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**查找具有此问题的节点。** 传入的上下文范围内，但您发现可能需要更改的代码的节点。 报告的诊断的范围仅用于 （在波形曲线上属于其中） 的类型标识符，但你需要更换整个对象创建表达式，其中包括`new`keywoard 在开头和结尾的括号。 将以下代码添加到你的方法 (并使用**CTRL +。** 若要添加`using`语句`ObjectCreationExpressionSyntax`):

```csharp

var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

 **注册灯泡 UI 将代码修补程序。** 注册您的代码修复程序时，Roslyn 插入到 Visual Studio 灯泡图标 UI 自动。 最终用户将看到，他们可以将**CTRL +。** （句点），当您的分析器错误的波形曲线`ImmutableArray<T>`构造函数使用。 由于代码修复提供程序仅执行时出现问题，可以假定您有要查找的对象创建表达式。 从上下文参数，可以注册新的代码修补程序，通过将以下代码添加到末尾的`RegisterCodeFixAsync`方法：

```csharp

context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

您需要将编辑器插入点放在标识符中`CodeAction`，然后使用**CTRL +。** （句点） 来添加适当`using`此类型的语句。

然后将放在编辑器中的插入符号`ChangeToImmutableArrayEmpty`标识符和使用**CTRL +。** 同样，若要为您生成此方法存根 （stub）。

添加此最后一个代码片段表示通过注册的代码修复`CodeAction`和找到的问题种类的诊断 ID。 在此示例中，存在只是一个诊断 ID，此代码提供修补程序，因此只需传递诊断 Id 数组的第一个元素。 当你创建`CodeAction`，灯泡图标中 UI 应使用作为代码修补程序的说明文本中传递。 你还采用 CancellationToken 并返回一个新的文档的函数中传递。 新的文档具有新的语法树包含修补的代码中调用`ImmutableArray.Empty`。 此代码片段，以便它可以关闭对 objectCreation 节点和上下文的文档使用 lambda。

**构造新的语法树。** 在中`ChangeToImmutableArrayEmpty`方法之前，生成的存根 （stub） 输入的代码行： `ImmutableArray<int>.Empty;`。 如果您再次查看语法可视化工具窗口，可以看到此语法是 SimpleMemberAccessExpression 节点。 这是此方法需要构造并返回新的文档中。

对第一个更改`ChangeToImmutableArrayEmpty`是添加`async`之前`Task<Document>`因为代码生成器不能假定该方法应为异步。

填写用下面的代码正文，以便你的方法看起来类似于以下：

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

将需要将编辑器插入点放在`SyntaxGenerator`标识符和使用**CTRL +。** （句点） 来添加适当`using`此类型的语句。

此代码使用`SyntaxGenerator`，用于构造新的代码是非常有用的类型。 获取文档的生成器具有代码问题后`ChangeToImmutableArrayEmpty`调用`MemberAccessExpression`、 传递具有我们想要访问的成员的类型和字符串形式传递的成员的名称。

接下来，方法提取文档的根，因为这可能涉及任意工作一般情况下的，该代码等待此调用，并将传递的取消标记。 Roslyn 代码模型是固定不变，如使用.NET 字符串;更新的字符串，可以获取新的字符串对象返回。 当您调用`ReplaceNode`，得到新的根节点。 大部分语法树共享的 （因为它是不可变），但`objectCreation`替换为节点`memberAccess`节点，以及最多语法树的根的所有父节点。

## <a name="trying-your-code-fix"></a>尝试代码修补程序
现在，可以按**F5**在 Visual Studio 的第二个实例中执行您的分析器。 打开之前使用的控制台项目。 现在，会看到灯泡图标中显示新的对象创建表达式为`ImmutableArray<int>`。 如果按**CTRL +。** （句点），则会看到解决问题，请在代码，将看到在灯泡 UI 中的自动生成的代码差异预览。 Roslyn 为你创建此操作。

Pro 提示：如果启动 Visual Studio 中，第二个实例，并且看不到灯泡图标中使用代码修补程序，您可能需要清除 Visual Studio 组件缓存。 清除缓存将强制 Visual Studio 以重新检查这些组件，因此 Visual Studio 应选取最新组件。 首先，关闭 Visual Studio 的第二个实例。 然后在 Windows 资源管理器，转到你的用户目录 (c:\users\\< userid\>) 并找到 AppData\Local\Microsoft\VisualStudio\14.0Roslyn\\。 在此目录中删除的 ComponentModelCache 子目录。 "14"的更改版本的 Visual studio 中。

## <a name="talk-video-and-finish-code-project"></a>访谈视频和完成的代码项目
您可以看到开发和讨论了此示例中进一步[本次讨论](http://channel9.msdn.com/events/Build/2015/3-725)。 讨论演示工作分析器，并指导您生成它。

可以看到所有已完成的代码[此处](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)。 子文件夹 DoNotUseImmutableArrayCollectionInitializer 和 DoNotUseImmutableArrayCtor 每个具有 C# 文件中查找问题和实现在 Visual Studio 灯泡 UI 中显示的代码修补程序的 C# 文件。 请注意，完成的代码有一些更多的抽象来避免提取 ImmutableArray\<T > 遍又一遍地键入对象。 它使用嵌套的已注册的操作类型对象保存在可用的上下文中时的子操作 （分析对象创建和分析集合初始化） 执行。

## <a name="see-also"></a>请参阅
[\\\Build 2015 talk](http://channel9.msdn.com/events/Build/2015/3-725)
[完成 GitHub 上的代码](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers) 
[GitHub 上的几个示例分为三种类型的分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md) 
 [OSS GitHub 站点上的其他 docs](https://github.com/dotnet/roslyn/tree/master/docs/analyzers) 
[FxCop 规则实现通过 GitHub 上的 Roslyn 分析器](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
