---
title: C++核心准则警告
ms.date: 10/16/2019
ms.topic: conceptual
ms.assetid: 7c83814a-f21d-4323-ad5f-13bac40d3e38
author: corob
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 4bcd32d633c2b88bba53aa79b670a59bda1ebef3
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271393"
---
# <a name="using-the-c-core-guidelines-checkers"></a>使用 C++ 核心准则检查程序

C++核心指导原则是有关C++专家和设计人员所C++创建的编码的一组可移植指导原则、规则和最佳实践。 Visual Studio 当前支持将这些规则作为的代码分析工具的一部分C++。 默认情况下，在 Visual Studio 2017 和 Visual Studio 2019 中安装核心准则检查程序，它们[可用作 Visual studio 2015 的 NuGet 包](#vs2015_corecheck)。

## <a name="the-c-core-guidelines-project"></a>C++核心准则项目

由 Bjarne Stroustrup 和其他人创建， C++核心准则是使用新式C++安全有效的指南。 这些指南强调了静态类型安全和资源安全性。 它们确定了消除或最小化语言中最容易出错的部分的方法，并建议如何以可靠的方式使代码更简单、更具性能。 这些准则由标准C++基础维护。 若要了解详细信息，请参阅[GitHub](https://github.com/isocpp/CppCoreGuidelines)上的文档、 [ C++核心准则](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)和访问C++核心准则文档项目文件。

## <a name="enable-the-c-core-check-guidelines-in-code-analysis"></a>启用代码C++分析中的核心检查指南

可以通过在项目的 "**属性页**" 对话框的 "**代码分析**" 部分中选择 "**生成时启用代码分析**" 复选框，对项目启用代码分析。

![代码分析常规设置的属性页](../code-quality/media/cppcorecheck_codeanalysis_general.png)

C++核心检查规则是启用代码分析时运行的默认规则集的扩展。 由于C++核心检查规则正在开发中，某些规则已经好建立，某些规则可能无法在所有代码上使用，但可能仍有信息。 这些规则分为两个组：已发布和实验性。 你可以选择是在项目的属性中运行已发布规则还是实验性规则。

![代码分析扩展插件设置的属性页](../code-quality/media/cppcorecheck_codeanalysis_extensions.png)

若要启用或禁用C++核心检查规则集，请打开项目的 "**属性页**" 对话框。 在 "**配置属性**" 下，展开 "**代码分析**" 和 "**扩展**"。 在 "**启用C++核心检查（已发布）** " 或 "  **C++启用核心检查（实验）** " 旁边的下拉列表中，选择 **"是" 或 "** **否**"。 选择 **"确定" 或 "** **应用**" 保存更改。

## <a name="examples"></a>示例

下面是C++核心检查规则可以发现的一些问题的示例：

```cpp
// CoreCheckExample.cpp
// Add CppCoreCheck package and enable code analysis in build for warnings.

int main()
{
    int arr[10];           // warning C26494
    int* p = arr;          // warning C26485

    [[gsl::suppress(bounds.1)]] // This attribute suppresses Bounds rule #1
    {
        int* q = p + 1;    // warning C26481 (suppressed)
        p = q++;           // warning C26481 (suppressed)
    }

    return 0;
}
```

此示例演示C++核心检查规则可以发现的几个警告：

- C26494 是规则类型。5：始终初始化对象。

- C26485 是规则界限。3：没有数组到指针的衰减。

- C26481 是规则界限。1：不要使用指针算法。 请改用 `span`。

如果编译C++此代码时安装并启用了核心检查代码分析规则集，则会输出前两个警告，但会禁止显示第三个警告。 下面是示例代码的生成输出：

```Output
1>------ Build started: Project: CoreCheckExample, Configuration: Debug Win32 ------
1>  CoreCheckExample.cpp
1>  CoreCheckExample.vcxproj -> C:\Users\username\documents\visual studio 2015\Projects\CoreCheckExample\Debug\CoreCheckExample.exe
1>  CoreCheckExample.vcxproj -> C:\Users\username\documents\visual studio 2015\Projects\CoreCheckExample\Debug\CoreCheckExample.pdb (Full PDB)
c:\users\username\documents\visual studio 2015\projects\corecheckexample\corecheckexample\corecheckexample.cpp(6): warning C26494: Variable 'arr' is uninitialized. Always initialize an object. (type.5: http://go.microsoft.com/fwlink/p/?LinkID=620421)
c:\users\username\documents\visual studio 2015\projects\corecheckexample\corecheckexample\corecheckexample.cpp(7): warning C26485: Expression 'arr': No array to pointer decay. (bounds.3: http://go.microsoft.com/fwlink/p/?LinkID=620415)
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

C++核心准则可帮助您编写更好和更安全的代码。 但是，如果你有一个不应应用规则或配置文件的实例，则可以轻松地直接在代码中将其取消。 你可以使用 `gsl::suppress` 特性来防止C++核心检查检测和报告以下代码块中的任何规则冲突。 您可以标记各个语句以禁止显示特定规则。 甚至可以通过编写 `[[gsl::suppress(bounds)]]` 来禁止整个边界配置文件，而无需包含特定的规则号。

## <a name="supported-rule-sets"></a>支持的规则集

将新规则添加到C++核心准则检查器时，为预先存在的代码生成的警告数可能会增加。 您可以使用预定义的规则集来筛选要启用的规则类型。 在 Visual Studio 2017 版本15.3 中，支持的规则集包括：

- **所有者指针规则**强制执行与[从核心准则中的 Owner\<t > 相关C++的资源管理检查](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#r-resource-management)。

- **Const 规则**强制实施[来自C++核心准则的 const 相关检查](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con-constants-and-immutability)。

- **原始指针规则**强制执行[与核心准则中的C++原始指针相关的资源管理检查](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#r-resource-management)。

- **唯一的指针规则**强制执行与[ C++核心准则中具有唯一指针语义的类型相关的资源管理检查](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#r-resource-management)。

- **边界规则**强制实施[ C++核心准则的边界配置文件](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)。

- **类型规则**强制实施[ C++核心准则的类型配置文件](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#prosafety-type-safety-profile)。

可以选择将警告仅限制为一个或多个组。 除了其他 PREfast 检查，**本机的最小**和**本机建议**规则集还包括C++核心检查规则。 若要查看可用的规则集，请打开 "项目属性" 对话框，选择 "**代码 Analysis\General**"，打开 "**规则集**" 组合框中的下拉列表，然后**选择 "选择多个规则集**"。 有关在 Visual Studio 中使用规则集的详细信息，请参阅[使用规则集对代码分析规则进行分组](using-rule-sets-to-group-code-analysis-rules.md)。

## <a name="macros"></a>宏

C++核心指导原则检查器附带了标头文件，该文件定义了宏，使您可以更轻松地在代码中禁止显示所有类别的警告：

```cpp
ALL_CPPCORECHECK_WARNINGS
CPPCORECHECK_TYPE_WARNINGS
CPPCORECHECK_RAW_POINTER_WARNINGS
CPPCORECHECK_CONST_WARNINGS
CPPCORECHECK_OWNER_POINTER_WARNINGS
CPPCORECHECK_UNIQUE_POINTER_WARNINGS
CPPCORECHECK_BOUNDS_WARNINGS
```

这些宏对应于规则集，并将其扩展到以空格分隔的警告数字列表。 使用适当的杂注构造，可以配置对项目或代码段感兴趣的有效规则集。 在下面的示例中，代码分析仅对缺少的常量修饰符发出警告：

```cpp
#include <CppCoreCheck\Warnings.h>
#pragma warning(disable: ALL_CPPCORECHECK_WARNINGS)
#pragma warning(default: CPPCORECHECK_CONST_WARNINGS)
```

## <a name="attributes"></a>属性

Microsoft C++编译器对 GSL 禁止显示属性的支持有限。 它可用于禁止在函数内的 expression 和 block 语句上出现警告。

```cpp
// Suppress only warnings from the 'r.11' rule in expression.
[[gsl::suppress(r.11)]] new int;

// Suppress all warnings from the 'r' rule group (resource management) in block.
[[gsl::suppress(r)]]
{
    new int;
}

// Suppress only one specific warning number.
// For declarations, you may need to use the surrounding block.
// Macros are not expanded inside of attributes.
// Use plain numbers instead of macros from the warnings.h.
[[gsl::suppress(26400)]]
{
    int *p = new int;
}
```

## <a name="suppressing-analysis-by-using-command-line-options"></a>使用命令行选项禁止分析

您可以在文件的属性页中使用命令行选项来禁止显示项目或单个文件的警告，而不是 #pragmas。 例如，禁用文件的警告26400：

1. 右键单击中的文件**解决方案资源管理器**

2. 选择**属性 |C/C++|命令行**

3. 在 "**其他选项**" 窗口中，添加 `/wd26400`。

通过指定 `/analyze-`，可以使用命令行选项来暂时禁用文件的所有代码分析。 这将生成*D9025 使用 "/analyze-" 替代 "/analyze*" 的警告，这将提醒你稍后重新启用代码分析。

## <a name="corecheck_per_file"></a>启用特定C++项目文件的核心准则检查器

有时，执行焦点代码分析并仍利用 Visual Studio IDE 可能会很有用。 下面是一个示例方案，可用于大项目以节省生成时间，并使其更易于筛选结果。

1. 在命令外壳中，设置 `esp.extension` 和 `esp.annotationbuildlevel` 环境变量。
2. 从命令行界面打开 Visual Studio 以继承这些变量。
3. 加载项目并打开其属性。
4. 启用代码分析，选取适当的规则集，但不要启用代码分析扩展。
5. 在C++核心准则检查器中转到要分析的文件，然后打开其属性。
6. 选择 " **CC++/\Command Line 选项**" 并添加 `/analyze:plugin EspXEngine.dll`
7. 禁用预编译头（**C/C++\Precompiled 标**头）的使用。 这是必需的，因为扩展引擎可能会尝试从预编译标头读取其内部信息，如果后者是用默认项目选项编译的，则它将是不兼容的。
8. 重新生成项目。 常见的 PREFast 检查应在所有文件上运行。 由于C++核心准则检查器默认情况下未启用，因此它只应在配置为使用它的文件上运行。

## <a name="how-to-use-the-c-core-guidelines-checker-outside-of-visual-studio"></a>如何在C++ Visual Studio 外部使用核心准则检查器
可以在自动生成C++中使用核心准则检查。

### <a name="msbuild"></a>MSBuild

本机代码分析检查器（PREfast）通过自定义目标文件集成到 MSBuild 环境中。 你可以使用项目属性来启用它，并添加C++核心准则检查器（基于 PREfast）：

```xml
<PropertyGroup>
  <EnableCppCoreCheck>true</EnableCppCoreCheck>
  <CodeAnalysisRuleSet>CppCoreCheckRules.ruleset</CodeAnalysisRuleSet>¬¬
  <RunCodeAnalysis>true</RunCodeAnalysis>
</PropertyGroup>
```

请确保在导入 Microsoft .Cpp 文件之前添加这些属性。 您可以选择特定规则集或创建自定义规则集，或使用包括其他 PREfast 检查的默认规则集。

您可以使用C++ [前面所述](#corecheck_per_file)的相同方法仅对指定文件运行核心检查程序，但使用 MSBuild 文件。 可以通过使用 `BuildMacro` 项来设置环境变量：

```xml
<ItemGroup>
    <BuildMacro Include="Esp_AnnotationBuildLevel">
      <EnvironmentVariable>true</EnvironmentVariable>
      <Value>Ignore</Value>
    </BuildMacro>
    <BuildMacro Include="Esp_Extensions">
      <EnvironmentVariable>true</EnvironmentVariable>
      <ValueCppCoreCheck.dll</Value>
    </BuildMacro>
</ItemGroup>
```

如果不想修改项目文件，则可以在命令行上传递属性：

```cmd
msbuild /p:EnableCppCoreCheck=true /p:RunCodeAnalysis=true /p:CodeAnalysisRuleSet=CppCoreCheckRules.ruleset ...
```

### <a name="non-msbuild-projects"></a>非 MSBuild 项目
如果你使用的生成系统不依赖于 MSBuild，你仍可以运行检查器，但你将需要熟悉代码分析引擎配置的某些内部机制（这在将来不保证受支持）。

你将需要设置几个环境变量并为编译器使用适当的命令行选项。 最好在 "本机工具命令提示" 环境下工作，这样您就不必搜索编译器的特定路径、包括目录等。

1. **环境变量**
   - `set esp.extensions=cppcorecheck.dll` 这将告知引擎加载C++核心准则模块。
   - `set esp.annotationbuildlevel=ignore` 这将禁用处理 SAL 批注的逻辑。 批注不会影响C++核心准则检查器中的代码分析，但其处理过程会耗费时间（有时很长时间）。 此设置是可选的，但强烈建议使用此设置。
   - `set caexcludepath=%include%` 强烈建议您禁用在标准标头上触发的警告。 你可以在此处添加更多路径，例如项目中的公共标头的路径。
2. **命令行选项**
   - `/analyze` 启用代码分析（还应考虑使用/analyze： only 和/analyze： quiet）。
   - `/analyze:plugin EspXEngine.dll` 此选项将代码分析扩展引擎加载到 PREfast 中。 此引擎反过来会加载C++核心准则检查器。

## <a name="use-the-guideline-support-library"></a>使用准则支持库

准则支持库旨在帮助你遵循核心准则。 GSL 包括一些定义，使你可以用更安全的替代方法替换容易出错的构造。 例如，您可以使用 `span<T>` 类型替换 `T*, length` 参数对。 [http://www.nuget.org/packages/Microsoft.Gsl](https://www.nuget.org/packages/Microsoft.Gsl)提供了 GSL。 库是开源的，因此可以查看源、进行注释或做出贡献。 可在[https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL)中找到该项目。

## <a name="vs2015_corecheck"></a>使用 Visual C++ Studio 2015 项目中的核心检查指南

如果使用 Visual Studio 2015，则C++默认情况下不会安装核心检查代码分析规则集。 必须执行一些附加步骤，然后才能在 Visual Studio C++ 2015 中启用核心检查代码分析工具。 Microsoft 通过使用 Nuget 包为 Visual Studio 2015 项目提供支持。 此包的名称为 CppCoreCheck，可[http://www.nuget.org/packages/Microsoft.CppCoreCheck](https://www.nuget.org/packages/Microsoft.CppCoreCheck)。 此程序包需要至少安装了 Visual Studio 2015 Update 1。

该包还会安装另一个包作为依赖项，即仅标头的准则支持库（GSL）。 [https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL)上还提供了 GitHub 上的 GSL。

由于代码分析规则的加载方式，你必须将 CppCoreCheck NuGet 包安装到要在 Visual Studio 2015 中C++检查的每个项目。

### <a name="to-add-the-microsoftcppcorecheck-package-to-your-project-in-visual-studio-2015"></a>将 CppCoreCheck 包添加到 Visual Studio 2015 中的项目

1. 在**解决方案资源管理器**中，右键单击以打开要将包添加到的解决方案中项目的上下文菜单。 选择 "**管理 Nuget 包**"，打开**NuGet 包管理器**。

2. 在 " **NuGet 包管理器**" 窗口中，搜索 CppCoreCheck。

    !["Nuget 包管理器" 窗口显示 CppCoreCheck 包](../code-quality/media/cppcorecheck_nuget_window.png)

3. 选择 CppCoreCheck 包，然后选择 "**安装**" 按钮，将规则添加到项目。

   在项目中启用代码分析后，NuGet 包会向项目添加一个附加的 MSBuild 文件。 此 .targets 文件将C++核心检查规则作为附加扩展添加到 Visual Studio 代码分析工具。 安装包后，可以使用 "属性页" 对话框启用或禁用已发布和实验性规则。
