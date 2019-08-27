---
title: Vbc 任务 | Microsoft Docs
ms.date: 04/12/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Vbc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Vbc task [MSBuild]
- MSBuild, Vbc task
ms.assetid: 595278b1-2782-4577-b1ba-b4b5ab5625a3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 247d7c5a204418fdddf41e906a12ef2ef1fb232f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62577767"
---
# <a name="vbc-task"></a>Vbc 任务
包装可生成可执行文件 (.exe)、动态链接库 (.dll) 或代码模块 (.netmodule) 的 vbc.exe。 有关 vbc.exe 的详细信息，请参阅 [Visual Basic 命令行编译器](/dotnet/visual-basic/reference/command-line-compiler/index)。

## <a name="parameters"></a>参数
 下表描述了 `Vbc` 任务的参数。

| 参数 | 说明 |
|------------------------------| - |
| `AdditionalLibPaths` | 可选 `String[]` 参数。<br /><br /> 指定要在其中查找 References 属性中指定的程序集的其他文件夹。 |
| `AddModules` | 可选 `String[]` 参数。<br /><br /> 使编译器让指定文件中的所有类型信息可供当前正在编译的项目使用。 此参数对应于 vbc.exe 编译器的 [-addmodule](/dotnet/visual-basic/reference/command-line-compiler/addmodule) 开关。 |
| `BaseAddress` | 可选 `String` 参数。<br /><br /> 指定 DLL 的基址。 此参数对应于 vbc.exe 编译器的 [-baseaddress](/dotnet/visual-basic/reference/command-line-compiler/baseaddress) 开关。 |
| `CodePage` | 可选 `Int32` 参数。<br /><br /> 指定要用于编译中所有源代码文件的代码页。 此参数对应于 vbc.exe 编译器的 [-codepage](/dotnet/visual-basic/reference/command-line-compiler/codepage) 开关。 |
| `DebugType` | 可选 `String[]` 参数。<br /><br /> 让编译器生成调试信息。 此参数可以具有下列值：<br /><br /> -   `full`<br />-   `pdbonly`<br /><br /> 默认值为 `full`，该值允许将调试器附加到正在运行的程序。 `pdbonly` 的值允许在调试器中启动程序时进行源代码调试，但仅在正在运行的程序附加到调试器时才显示汇编语言代码。 有关详细信息，请参阅 [-debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug)。 |
| `DefineConstants` | 可选 `String[]` 参数。<br /><br /> 定义条件编译器常数。 符号/值对是使用下面的语法指定的，并且彼此之间用分号分隔：<br /><br /> 符号 1 `=` 值 1 `;` 符号 2 `=` 值 2<br /><br /> 此参数对应于 vbc.exe 编译器的 [-define](/dotnet/visual-basic/reference/command-line-compiler/define) 开关。 |
| `DelaySign` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，任务会将公钥放在程序集中。 如果为 `false`，任务会充分为程序集签名。 默认值为 `false`。除非与 `KeyFile` 参数或 `KeyContainer` 参数一起使用，否则此参数无效。 此参数对应于 vbc.exe 编译器的 [-delaysign](/dotnet/visual-basic/reference/command-line-compiler/delaysign) 开关。 |
| `Deterministic` | 可选 `Boolean` 参数。<br/><br/> 如果为 `true`，则会导致编译器输出的程序集的二进制内容在整个编译中相同（如果输入相同）。<br/><br/>有关详细信息，请参阅 [-deterministic](/dotnet/visual-basic/reference/command-line-compiler/deterministic)。 |
| `DisabledWarnings` | 可选 `String` 参数。<br /><br /> 禁止显示指定的警告。 只需指定警告标识符的数值部分。 多个警告之间用分号分隔。 此参数对应于 vbc.exe 编译器的 [-nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) 开关。 |
| `DocumentationFile` | 可选 `String` 参数。<br /><br /> 将文档注释处理到指定的 XML 文件中。 此参数替代 `GenerateDocumentation` 属性。 有关详细信息，请参阅 [-doc](/dotnet/visual-basic/reference/command-line-compiler/doc)。 |
| `EmitDebugInformation` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务生成调试信息并将它放置在 .pdb 文件中。 有关详细信息，请参阅 [-debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug)。 |
| `ErrorReport` | 可选 `String` 参数。<br /><br /> 指定任务报告内部编译器错误的方式。 此参数可以具有下列值：<br /><br /> -   `prompt`<br />-   `send`<br />-   `none`<br /><br /> 如果指定了 `prompt`，且发生内部编译器错误，则会提示用户选择是否将错误数据发送给 Microsoft。<br /><br /> 如果指定了 `send`，且发生内部编译器错误，则该任务会向 Microsoft 发送错误数据。<br /><br /> 默认值是 `none`，它仅在文本输出中报告错误。<br /><br /> 此参数对应于 vbc.exe 编译器的 [-errorreport](/dotnet/visual-basic/reference/command-line-compiler/errorreport) 开关。 |
| `FileAlignment` | 可选 `Int32` 参数。<br /><br /> 指定输出文件各部分的对齐位置，以字节为单位。 此参数可以具有下列值：<br /><br /> -   `512`<br />-   `1024`<br />-   `2048`<br />-   `4096`<br />-   `8192`<br /><br /> 此参数对应于 vbc.exe 编译器的 [-filealign](/dotnet/visual-basic/reference/command-line-compiler/filealign) 开关。 |
| `GenerateDocumentation` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会生成文档信息，并将此信息与任务创建的可执行文件或库的名称一同放置在 XML 文件中。 有关详细信息，请参阅 [-doc](/dotnet/visual-basic/reference/command-line-compiler/doc)。 |
| `Imports` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 从指定项集合导入命名空间。 此参数对应于 vbc.exe 编译器的 [-imports](/dotnet/visual-basic/reference/command-line-compiler/imports) 开关。 |
| `KeyContainer` | 可选 `String` 参数。<br /><br /> 指定加密密钥容器的名称。 此参数对应于 vbc.exe 编译器的 [-keycontainer](/dotnet/visual-basic/reference/command-line-compiler/keycontainer) 开关。 |
| `KeyFile` | 可选 `String` 参数。<br /><br /> 指定含有加密密钥的文件名。 有关详细信息，请参阅 [-keyfile](/dotnet/visual-basic/reference/command-line-compiler/keyfile)。 |
| `LangVersion` | 可选 <xref:System.String?displayProperty=fullName> 参数。<br /><br /> 指定[语言版本](/dotnet/visual-basic/language-reference/configure-language-version)，如“15.5”。 |
| `LinkResources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 创建指向输出文件中的 .NET Framework 资源的链接；资源文件不会放入输出文件中。 此参数对应于 vbc.exe 编译器的 [-linkresource](/dotnet/visual-basic/reference/command-line-compiler/linkresource) 开关。 |
| `MainEntryPoint` | 可选 `String` 参数。<br /><br /> 指定包含 `Sub Main` 过程的类或模块。 此参数对应于 vbc.exe 编译器的 [-main](/dotnet/visual-basic/reference/command-line-compiler/main) 开关。 |
| `ModuleAssemblyName` | 可选 `String` 参数。<br /><br /> 指定此模块所属程序集。 |
| `NoConfig` | 可选 `Boolean` 参数。<br /><br /> 指定编译器不应使用 vbc.rsp 文件。 此参数对应于 vbc.exe 编译器的 [-noconfig](/dotnet/visual-basic/reference/command-line-compiler/noconfig) 参数。 |
| `NoLogo` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则禁止显示编译器横幅信息。 此参数对应于 vbc.exe 编译器的 [-nologo](/dotnet/visual-basic/reference/command-line-compiler/nologo) 开关。 |
| `NoStandardLib` | 可选 `Boolean` 参数。<br /><br /> 导致编译器不引用标准库。 此参数对应于 vbc.exe 编译器的 [-nostdlib](/dotnet/visual-basic/reference/command-line-compiler/nostdlib) 开关。 |
| `NoVBRuntimeReference` | 可选 `Boolean` 参数。<br /><br /> 仅限内部使用。 如果为 true，则会阻止自动引用 Microsoft.VisualBasic.dll。 |
| `NoWarnings` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，任务会禁止所有警告。 有关详细信息，请参阅 [-nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn)。 |
| `Optimize` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会启用编译器优化。 此参数对应于 vbc.exe 编译器的 [-optimize](/dotnet/visual-basic/reference/command-line-compiler/optimize) 开关。 |
| `OptionCompare` | 可选 `String` 参数。<br /><br /> 指定如何进行字符串比较。 此参数可以具有下列值：<br /><br /> -   `binary`<br />-   `text`<br /><br /> 值 `binary` 指定该任务使用二进制字符串比较。 值 `text` 指定该任务使用文本字符串比较。 此参数的默认值为 `binary`。 此参数对应于 vbc.exe 编译器的 [-optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare) 开关。 |
| `OptionExplicit` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则要求显式声明变量。 此参数对应于 vbc.exe 编译器的 [-optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit) 开关。 |
| `OptionInfer` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则允许对变量进行类型推理。 |
| `OptionStrict` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则任务强制执行严格类型语义，限制隐式类型转换。 此参数对应于 vbc.exe 编译器的 [-optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) 开关。 |
| `OptionStrictType` | 可选 `String` 参数。<br /><br /> 指定生成警告的严格类型语义。 当前仅支持“custom”。 此参数对应于 vbc.exe 编译器的 [-optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) 开关。 |
| `OutputAssembly` | 可选 `String` 输出参数。<br /><br /> 指定输出文件的名称。 此参数对应于 vbc.exe 编译器的 [-out](/dotnet/visual-basic/reference/command-line-compiler/out) 开关。 |
| `Platform` | 可选 `String` 参数。<br /><br /> 指定将作为输出文件目标的处理器平台。 此参数可以具有 `x86`、 `x64``Itanium` 或 `anycpu` 的值。 默认值为 `anycpu`。 此参数对应于 vbc.exe 编译器的 [-platform](/dotnet/visual-basic/reference/command-line-compiler/platform) 开关。 |
| `References` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 促使该任务将公共类型信息从指定项导入到当前项目中。 此参数对应于 vbc.exe 编译器的 [-reference](/dotnet/visual-basic/reference/command-line-compiler/reference) 开关。 |
| `RemoveIntegerChecks` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则禁用整数溢出错误检查。 默认值为 `false`。 此参数对应于 vbc.exe 编译器的 [-removeintchecks](/dotnet/visual-basic/reference/command-line-compiler/removeintchecks) 开关。 |
| `Resources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 将 .NET Framework 资源嵌入到输出文件。 此参数对应于 vbc.exe 编译器的 [-resource](/dotnet/visual-basic/reference/command-line-compiler/resource) 开关。 |
| `ResponseFiles` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定包含此任务命令的响应文件。 此参数对应于 vbc.exe 编译器的 [@ (指定响应文件)](/dotnet/visual-basic/reference/command-line-compiler/specify-response-file)选项。 |
| `RootNamespace` | 可选 `String` 参数。<br /><br /> 指定所有类型声明的根命名空间。 此参数对应于 vbc.exe 编译器的 [-rootnamespace](/dotnet/visual-basic/reference/command-line-compiler/rootnamespace) 开关。 |
| `SdkPath` | 可选 `String` 参数。<br /><br /> 指定 mscorlib.dll 和 microsoft.visualbasic.dll 的位置。 此参数对应于 vbc.exe 编译器的 [-sdkpath](/dotnet/visual-basic/reference/command-line-compiler/sdkpath) 开关。 |
| `Sources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个或多个 Visual Basic 源文件。 |
| `TargetCompactFramework` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则任务面向 [!INCLUDE[Compact](../extensibility/includes/compact_md.md)]。 此参数对应于 vbc.exe 编译器的 [-netcf](/dotnet/visual-basic/reference/command-line-compiler/netcf) 开关。 |
| `TargetType` | 可选 `String` 参数。<br /><br /> 指定输出文件的文件格式。 此参数可以具有 `library` 或 `winexe` 的值，前者将创建代码库 `exe`，代码库将创建控制台应用程序 `module`，应用程序将创建一个模块，后者将创建 Windows 程序。 默认值为 `library`。 此参数对应于 vbc.exe 编译器的 [-target](/dotnet/visual-basic/reference/command-line-compiler/target) 开关。 |
| `Timeout` | 可选 `Int32` 参数。<br /><br /> 指定终止任务可执行文件之前的时间量（以毫秒为单位）。 默认值是 `Int.MaxValue`，指示没有超时期限。 |
| `ToolPath` | 可选 `String` 参数。<br /><br /> 指定任务从何处加载基础可执行文件 (vbc.exe)。 如果未指定此参数，则任务会使用与运行 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 的框架版本对应的 SDK 安装路径。 |
| `TreatWarningsAsErrors` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则会将所有警告视为错误。 有关详细信息，请参阅 [-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)。 |
| `UseHostCompilerIfAvailable` | 可选 `Boolean` 参数。<br /><br /> 指示该任务使用进程内编译器对象（如果可用）。 仅由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 使用。 |
| `Utf8Output` | 可选 `Boolean` 参数。<br /><br /> 记录使用 UTF-8 编码的编译器输出。 此参数对应于 vbc.exe 编译器的 [-utf8output](/dotnet/visual-basic/reference/command-line-compiler/utf8output) 开关。 |
| `Verbosity` | 可选 `String` 参数。<br /><br /> 指定编译器输出的详细级别。 详细级别可以为 `Quiet`、`Normal`（默认）或 `Verbose`。 |
| `WarningsAsErrors` | 可选 `String` 参数。<br /><br /> 指定将被视为错误的警告的列表。 有关详细信息，请参阅 [-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)。<br /><br /> 此参数替代 `TreatWarningsAsErrors` 参数。 |
| `WarningsNotAsErrors` | 可选 `String` 参数。<br /><br /> 指定不被视为错误的警告的列表。 有关详细信息，请参阅 [-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)。<br /><br /> 只有 `TreatWarningsAsErrors` 参数设置为 `true` 时，此参数才有用。 |
| `Win32Icon` | 可选 `String` 参数。<br /><br /> 在程序集中插入 .ico 文件，为输出文件赋予其在“文件资源管理器”中所需的外观。 此参数对应于 vbc.exe 编译器的 [-win32icon](/dotnet/visual-basic/reference/command-line-compiler/win32icon) 开关。 |
| `Win32Resources` | 可选 `String` 参数。<br /><br /> 在输出文件中插入 Win32 资源 (.res) 文件。 此参数对应于 vbc.exe 编译器的 [-win32resource](/dotnet/visual-basic/reference/command-line-compiler/win32resource) 开关。 |

## <a name="remarks"></a>备注
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类。 有关这些其他参数的列表及其说明，请参阅 [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)。

## <a name="example"></a>示例
 以下示例编译 Visual Basic 项目。

```xml
<VBC
   Sources="@(sources)"
   Resources="strings.resources"
   Optimize="true"
   OutputAssembly="out.exe"/>
```

## <a name="see-also"></a>请参阅
- [Visual Basic 命令行编译器](/dotnet/visual-basic/reference/command-line-compiler/index)
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
