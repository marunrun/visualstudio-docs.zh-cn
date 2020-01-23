---
title: 代码覆盖率测试
ms.date: 07/23/2019
ms.topic: conceptual
helpviewer_keywords:
- code coverage
dev_langs:
- CSharp
- VB
- CPP
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6dd6dde83720c6e6f37bd6827bb5d97526202aa7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585595"
---
# <a name="use-code-coverage-to-determine-how-much-code-is-being-tested"></a>使用代码覆盖率确定所测试的代码量

若要确定正在由编码的测试（例如单元测试）实际进行测试的项目代码的比例，则可以使用 Visual Studio 的代码覆盖率功能。 若要有效防止 Bug，测试应作用于或“覆盖”你的大部分代码。

可将代码覆盖率分析应用于托管 (CLI) 和非托管（本机）代码。

代码覆盖率是使用测试资源管理器运行测试方法时的一个选项。 结果表将显示在各个程序集、类和方法中运行的代码的百分比。 此外，源代码编辑器会显示已测试的代码。

::: moniker range="vs-2017"

![着色的代码覆盖率结果](../test/media/codecoverage1.png)

::: moniker-end

## <a name="requirements"></a>要求

代码覆盖率功能仅在 Visual Studio Enterprise 版本中可用。

## <a name="analyze-code-coverage"></a>分析代码覆盖率

::: moniker range="vs-2017"

1. 在“测试”  菜单上，选择“分析代码覆盖率”  。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在“测试”  菜单中，选择“分析所有测试的代码覆盖率”  。

   ![在 VS 2019 中分析代码覆盖率](../test/media/vs-2019/analyze-code-coverage.png)

   你还可以从“测试资源管理器”工具窗口中运行代码覆盖率。

::: moniker-end

2. 测试运行后，若要查看已运行的行，请选择“代码覆盖率结果”  窗口中的![显示代码覆盖率着色图标](../test/media/codecoverage-showcoloringicon.png)“显示代码覆盖率着色”  。 默认情况下，测试覆盖的代码以浅蓝色突出显示。

   > [!TIP]
   > 要更改颜色或使用加粗，请选择“工具” > “选项” > “环境” > “字体和颜色” > “显示其设置:      文本编辑器”。 在“显示项”下，调整“覆盖率”项的设置，例如“覆盖率未涉及的区域”   。
   >
   > ![代码覆盖率字体和颜色](media/vs-2019/coverage-fonts-and-colors.png)

3. 如果结果显示覆盖率较低，请调查代码的哪些部分没有执行测试，并编写更多测试来覆盖它们。 开发团队通常以大约 80% 的代码覆盖率为目标。 在某些情况下，较低的覆盖率是可接受的。 例如，当某代码是从标准模板生成时，可接受较低的覆盖率。

> [!TIP]
> - 关闭编译器优化
> - 如果要处理非托管（本机）代码，请使用调试版本
> - 为每个程序集生成 .pdb（符号）文件

如果没有获得预期的结果，请参阅[代码覆盖率疑难解答](../test/troubleshooting-code-coverage.md)。

不要忘记在更新代码后再次运行代码覆盖率。 在修改代码后或运行测试时，覆盖率结果和代码着色不会自动更新。

## <a name="report-in-blocks-or-lines"></a>按块或行报告

代码覆盖率将以  块为单位计数。 块是恰好有一个入口点和出口点的一段代码。  在测试运行期间，如果程序的控制流通过某个块，则将该块计为“已覆盖”。 块的使用次数对结果没有影响。

还可以通过在表标题中选择“添加/移除列”  来按行显示结果。 某些用户更喜欢行计数，因为百分比与你在源代码中看到的段的大小更为对应。 一个很长的计算块即使占用多行，也将计为一行。

> [!TIP]
> 一个代码行可包含多个代码块。 如果是这种情况，并且测试运行执行行中的所有代码块，则将该代码行计为一行。 如果执行行中的某些代码块（但不是所有代码块），则将其计算为部分行。

## <a name="manage-code-coverage-results"></a>管理代码覆盖率结果

“代码覆盖率结果”窗口通常显示最新运行的结果  。 如果更改了测试数据或每次只运行一部分测试，结果将会变化。

“代码覆盖率”窗口也可用来查看以前的结果或在其他计算机上获取的结果。

你可以合并多个运行的结果，例如来自使用不同的测试数据的运行的结果。

- **若要查看以前的结果集**，请从下拉菜单中选择它。 该菜单将会显示一个临时列表。打开新的解决方案时，将会清除该列表。

- **要查看以前会话中的结果**，请选择“导入代码覆盖率结果”，导航到解决方案中的 TestResults 文件夹，然后导入 .coverage 文件    。

   如果源代码自 .coverage 文件生成之后已发生更改，则覆盖率着色可能不正确  。

- **若要使结果可作为文本读取**，请选择“导出代码覆盖率结果”  。 这将生成可使用其他工具处理或在邮件中轻松发送的可读 .coveragexml 文件  。

- **要将结果发送给其他人**，请发送 .coverage 文件或导出的 .coveragexml 文件   。 他们随后可以导入该文件。 如果他们具有相同版本的源代码，还可以看到覆盖率着色。

## <a name="merge-results-from-different-runs"></a>合并不同运行的结果

在某些情况下，将根据测试数据来使用代码中的不同块。 因此，你可能需要组合来自不同的测试运行的结果。

例如，假设你在运行某个测试（输入为“2”）时发现某个特定函数已被覆盖了 50%。 当你第二次运行该测试（输入为“-2”）时，你在覆盖着色视图中发现该函数的另外 50% 也被覆盖。 现在，你合并来自这两个测试运行的结果，报告和覆盖率着色视图显示该函数已经 100% 被覆盖。

为此，请使用![“代码覆盖率”窗口中“合并”按钮的图标](../test/media/codecoverage-mergeicon.png)合并代码覆盖率结果  。 你可以选择最近的运行或导入的结果的任意组合。 如果要组合导出的结果，则必须先将其导入。

使用“导出代码覆盖率结果”  可保存合并操作的结果。

### <a name="limitations-in-merging"></a>有关合并的限制

- 如果你合并不同版本的代码中的覆盖率数据，结果将单独显示，但不会合并。 若要获取完全合并的结果，请使用相同的代码生成，并且仅更改测试数据。

- 如果你合并一个先导出然后导入的结果文件，则只能按行查看结果，而不能按块查看结果。 使用“添加/移除列”  命令可显示行数据。

- 如果你合并来自 ASP.NET 项目的测试的结果，则将显示各个测试的结果，而不是合并的测试的结果。 这只适用于 ASP.NET 项目本身：任何其他程序集的结果都将合并。

## <a name="exclude-elements-from-the-code-coverage-results"></a>从代码覆盖率结果中排除元素

例如，如果代码是从文本模板生成的，则你可能希望从覆盖率分数中排除代码中的特定元素。 将特性 <xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute?displayProperty=fullName> 添加到以下任一代码元素：类、结构、方法、属性、属性 setter 或 getter、事件。

> [!TIP]
> 排除某个类并不会排除它的派生类。

例如：

```csharp
using System.Diagnostics.CodeAnalysis;
...
public class ExampleClass1
{
    [ExcludeFromCodeCoverage]
    void ExampleMethod() {...}

    [ExcludeFromCodeCoverage] // exclude property
    int ExampleProperty1
    { get {...} set{...}}

    int ExampleProperty2
    {
        get
        {
            ...
        }
        [ExcludeFromCodeCoverage] // exclude setter
        set
        {
            ...
        }
    }

}
[ExcludeFromCodeCoverage]
class ExampleClass2 { ... }
```

```vb
Imports System.Diagnostics.CodeAnalysis

Class ExampleClass1
    <ExcludeFromCodeCoverage()>
    Public Sub ExampleSub1()
        ...
    End Sub

    ' Exclude property
    < ExcludeFromCodeCoverage()>
    Property ExampleProperty1 As Integer
        ...
    End Property

    ' Exclude setter
    Property ExampleProperty2 As Integer
        Get
            ...
        End Get
        <ExcludeFromCodeCoverage()>
        Set(ByVal value As Integer)
            ...
        End Set
    End Property
End Class

<ExcludeFromCodeCoverage()>
Class ExampleClass2
...
End Class
```

```cpp
// A .cpp file compiled as managed (CLI) code.
using namespace System::Diagnostics::CodeAnalysis;
...
public ref class ExampleClass1
{
  public:
    [ExcludeFromCodeCoverage]
    void ExampleFunction1() { ... }

    [ExcludeFromCodeCoverage]
    property int ExampleProperty2 {...}

    property int ExampleProperty2 {
      int get() { ... }
     [ExcludeFromCodeCoverage]
      void set(int value) { ...  }
   }
}

[ExcludeFromCodeCoverage]
public ref class ExampleClass2
{ ... }
```

### <a name="exclude-elements-in-native-c-code"></a>排除本机 C++ 代码中的元素

若要排除 C++ 代码中的非托管（本机）元素：

```cpp
#include <CodeCoverage\CodeCoverage.h>
...

// Exclusions must be compiled as unmanaged (native):
#pragma managed(push, off)

// Exclude a particular function:
ExcludeFromCodeCoverage(Exclusion1, L"MyNamespace::MyClass::MyFunction");

// Exclude all the functions in a particular class:
ExcludeFromCodeCoverage(Exclusion2, L"MyNamespace::MyClass2::*");

// Exclude all the functions generated from a particular template:
ExcludeFromCodeCoverage(Exclusion3, L"*::MyFunction<*>");

// Exclude all the code from a particular .cpp file:
ExcludeSourceFromCodeCoverage(Exclusion4, L"*\\unittest1.cpp");

// After setting exclusions, restore the previous managed/unmanaged state:
#pragma managed(pop)
```

使用以下宏：

`ExcludeFromCodeCoverage(` ExclusionName  `, L"` FunctionName  `");`

`ExcludeSourceFromCodeCoverage(` ExclusionName  `, L"` SourceFilePath  `");`

- *ExclusionName* 是唯一名称。

- *FunctionName* 是完全限定的函数名。 它可能包含通配符。 例如，若要排除某个类的所有函数，应编写 `MyNamespace::MyClass::*`

- *SourceFilePath* 是 .cpp 文件的本地或 UNC 路径。 它可能包含通配符。 以下示例将排除特定目录中的所有文件：`\\MyComputer\Source\UnitTests\*.cpp`

- `#include <CodeCoverage\CodeCoverage.h>`

- 将对排除宏的调用放在全局命名空间中，而不是放在任何命名空间或类中。

- 你可以将排除放在单元测试代码文件或应用程序代码文件中。

- 必须通过设置编译器选项或使用 `#pragma managed(off)` 将排除编译为非托管（本机）代码。

> [!NOTE]
> 若要排除 C++/CLI 代码中的函数，应对函数应用特性 `[System::Diagnostics::CodeAnalysis::ExcludeFromCodeCoverage]`。 这与 C# 中的做法相同。

### <a name="include-or-exclude-additional-elements"></a>包括或排除其他元素

仅对已加载并且在 .dll 或 .exe 文件所在相同目录中有可用的 .pdb 文件的程序集执行代码覆盖率分析    。 因此，在某些情况下，可以通过获取适当的 .pdb 文件的副本来扩展包含的一组程序集  。

可通过编写 .runsettings 文件来加强控制为代码覆盖率分析选择哪些程序集和元素  。 例如，你可以排除特定类型的程序集，而不必向它们的类添加特性。 有关详细信息，请参阅[自定义代码覆盖率分析](../test/customizing-code-coverage-analysis.md)。

## <a name="analyze-code-coverage-in-azure-pipelines"></a>分析 Azure Pipelines 中的代码覆盖率

签入代码时，你的测试以及其他团队成员的测试将在生成服务器中运行。 这对分析 Azure Pipelines 中的代码覆盖率很有用，以提供整个项目中最新、最全面的覆盖率信息。 它还包含用户不常在开发计算机上运行的自动系统测试和其他编码的测试。 有关详细信息，请参阅[使用你的生成运行单元测试](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts)。

## <a name="analyze-code-coverage-from-the-command-line"></a>从命令行分析代码覆盖率

若要从命令行运行测试，请使用 vstest.console.exe。  代码覆盖率是 vstest.console.exe 实用工具的一个选项  。

1. 启动“Visual Studio 开发人员命令提示”：

   ::: moniker range="vs-2017"

   在 Windows“启动”  菜单中，选择“Visual Studio 2017”  >“VS 2017 的开发人员命令提示”  。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   在 Windows“启动”  菜单中，选择“Visual Studio 2019”  >“VS 2019 的开发人员命令提示”  。

   ::: moniker-end

2. 在命令提示符下，运行下列命令：

   ```shell
   vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage
   ```

有关详细信息，请参阅 [VSTest.Console.exe 命令行选项](vstest-console-options.md)。

## <a name="troubleshoot"></a>疑难解答

如果看不到代码覆盖率结果，[代码覆盖率疑难解答](../test/troubleshooting-code-coverage.md)一文可能有所帮助。

## <a name="see-also"></a>请参阅

- [自定义代码覆盖率分析](../test/customizing-code-coverage-analysis.md)
- [代码覆盖率疑难解答](../test/troubleshooting-code-coverage.md)
- [单元测试代码](../test/unit-test-your-code.md)
