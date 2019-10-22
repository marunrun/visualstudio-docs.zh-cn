---
title: Csc 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Csc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Csc task [MSBuild]
- MSBuild, Csc task
ms.assetid: d8c19b36-f5ca-484b-afa6-8ff3b90e103a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9df54befff79b82703cb363fea92536285c68232
ms.sourcegitcommit: 4dfe098ac0df294aad63e6b384d6575980798ca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70888025"
---
# <a name="csc-task"></a>Csc 任务
包装 csc.exe，生成可执行 (.exe) 文件、动态链接库（.dll 文件）或者代码模块（.netmodule 文件）     。 有关 csc.exe 的详细信息，请参阅 [C# 编译器选项](/dotnet/csharp/language-reference/compiler-options/index)  。

## <a name="parameters"></a>参数
下表描述了 `Csc` 任务的参数。

| 参数 | 说明 |
|------------------------------| - |
| `AdditionalLibPaths` | 可选 `String[]` 参数。<br /><br /> 指定要在其中搜索引用的其他目录。 有关详细信息，请参阅 [-lib（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/lib-compiler-option)。 |
| `AddModules` | 可选 `String` 参数。<br /><br /> 指定将构成程序集一部分的一个或多个模块。 有关详细信息，请参阅 [（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/addmodule-compiler-option)。 |
| `AllowUnsafeBlocks` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则编译使用 [unsafe](/dotnet/csharp/language-reference/keywords/unsafe) 关键字的代码。 有关详细信息，请参阅 [-unsafe（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/unsafe-compiler-option)。 |
| `ApplicationConfiguration` | 可选 `String` 参数。<br /><br /> 指定包含程序集绑定设置的应用程序配置文件。 |
| `BaseAddress` | 可选 `String` 参数。<br /><br /> 指定要加载 DLL 的首选基址。 DLL 的默认基址由 .NET Framework 公共语言运行时设置。 有关详细信息，请参阅 [-baseaddress（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option)。 |
| `CheckForOverflowUnderflow` | 可选 `Boolean` 参数。<br /><br /> 指定溢出数据类型边界的整数算法是否导致运行时异常。 有关详细信息，请参阅 [-checked（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option)。 |
| `CodePage` | 可选 `Int32` 参数。<br /><br /> 指定要用于编译中所有源代码文件的代码页。 有关详细信息，请参阅 [-codepage（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/codepage-compiler-option)。 |
| `DebugType` | 可选 `String` 参数。<br /><br /> 指定调试类型。 `DebugType` 可以是 `full` 或 `pdbonly`。 默认值是 `full`，这使得调试程序能够附加到正在运行的程序中。 指定在调试程序中启动该程序时，`pdbonly` 启用源代码调试，但正在运行的程序附加到调试程序时，只显示汇编程序。<br /><br /> 此参数替代 `EmitDebugInformation` 参数。<br /><br /> 有关详细信息，请参阅 [-debug（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)。 |
| `DefineConstants` | 可选 `String` 参数。<br /><br /> 定义预处理器符号。 有关详细信息，请参阅 [-define（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/define-compiler-option)。 |
| `DelaySign` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定仅需要将公钥放在程序集中。 如果为 `false`，则指定需要完全签名的程序集<br /><br /> 此参数无任何效果，除非与 `KeyFile` 或 `KeyContainer` 参数配合使用。<br /><br /> 有关详细信息，请参阅 [-delaysign（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/delaysign-compiler-option)。 |
| `Deterministic` | 可选 `Boolean` 参数。<br/><br/> 如果为 `true`，则会导致编译器输出的程序集的二进制内容在整个编译中相同（如果输入相同）。<br/><br/>有关详细信息，请参阅 [（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option)。 |
| `DisabledWarnings` | 可选 `String` 参数。<br /><br /> 指定要禁用的警告的列表。 有关详细信息，请参阅 [nowarn（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/nowarn-compiler-option)。 |
| `DocumentationFile` | 可选 `String` 参数。<br /><br /> 将文档注释处理到一个 XML 文件中。 有关详细信息，请参阅 [doc（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/doc-compiler-option)。 |
| `EmitDebugInformation` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务生成调试信息并将它放置在程序数据库 (pdb) 文件中。 如果为 `false`，则此任务不发出任何调试信息。 默认值为 `false`。 有关详细信息，请参阅 [-debug（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)。 |
| `ErrorReport` | 可选 `String` 参数。<br /><br /> 提供向 Microsoft 报告 C# 内部错误的简便方法。 此参数可以具有 `prompt`、`send` 或 `none` 的值。 如果该参数设置为 `prompt`，则内部编译器错误发生时，你将收到一条提示。 该提示让你将一个 Bug 报告以电子方式发送给 Microsoft。 如果该参数设置为 `send`，则系统将自动发送 Bug 报告。 如果该参数设置为 `none`，则仅在编译器的文本输出中报告错误。 默认值为 `none`。 有关详细信息，请参阅 [-errorreport（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option)。 |
| `FileAlignment` | 可选 `Int32` 参数。<br /><br /> 指定输出文件中各节的大小。 有关详细信息，请参阅 [-filealign（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option)。 |
| `GenerateFullPaths` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定编译器输出中文件的绝对路径。 如果为 `false`，则指定文件的名称。 默认值为 `false`。 有关详细信息，请参阅 [-fullpaths（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/fullpaths-compiler-option)。 |
| `KeyContainer` | 可选 `String` 参数。<br /><br /> 指定加密密钥容器的名称。 有关详细信息，请参阅 [-keycontainer（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/keycontainer-compiler-option)。 |
| `KeyFile` | 可选 `String` 参数。<br /><br /> 指定含有加密密钥的文件名。 有关详细信息，请参阅 [-keyfile（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/keyfile-compiler-option)。 |
| `LangVersion` | 可选 `String` 参数。<br /><br /> 指定要使用的语言版本。 有关详细信息，请参阅 [-langversion（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option)。 |
| `LinkResources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 创建指向输出文件中的 .NET Framework 资源的链接；资源文件不会放入输出文件中。<br /><br /> 传递到此参数的项可以具有名为 `LogicalName` 和 `Access` 的可选元数据条目。 `LogicalName` 对应于 `/linkresource` 开关的 `identifier` 参数，`Access` 对应于 `accessibility-modifier` 参数。 有关详细信息，请参阅 [-linkresource（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/linkresource-compiler-option)。 |
| `MainEntryPoint` | 可选 `String` 参数。<br /><br /> 指定 `Main` 方法的位置。 有关详细信息，请参阅 [-main（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/main-compiler-option)。 |
| `ModuleAssemblyName` | 可选 `String` 参数。<br /><br /> 指定此模块所属程序集的名称。 |
| `NoConfig` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则告知编译器不使用 csc.rsp 文件进行编译  。 有关详细信息，请参阅 [-noconfig（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/noconfig-compiler-option)。 |
| `NoLogo` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则禁止显示编译器横幅信息。 有关详细信息，请参阅 [-nologo（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/nologo-compiler-option)。 |
| `NoStandardLib` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则防止导入 mscorlib.dll，这定义了整个 System 命名空间。  如果你想要定义或创建自己的 System 命名空间和对象，请使用此参数。 有关详细信息，请参阅 [-nostdlib（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option)。 |
| `NoWin32Manifest` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则不包括默认的 Win32 清单。 |
| `Optimize` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则启用优化。 如果为 `false`，则禁用优化。 有关详细信息，请参阅 [-optimize（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/optimize-compiler-option)。 |
| `OutputAssembly` | 可选 `String` 输出参数。<br /><br /> 指定输出文件的名称。 有关详细信息，请参阅 [-out（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/out-compiler-option)。 |
| `OutputRefAssembly` | 可选 `String` 参数。<br /><br /> 指定输出引用程序集文件的名称。 有关详细信息，请参阅 [-refout （C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/refout-compiler-option)。 |
| `PdbFile` | 可选 `String` 参数。<br /><br /> 指定调试信息文件名。 默认名称是扩展名为 .pdb 的输出文件名。  |
| `Platform` | 可选 `String` 参数。<br /><br /> 指定将作为输出文件目标的处理器平台。 此参数可以具有 `x86`、`x64` 或 `anycpu` 的值。 默认值为 `anycpu`。 有关详细信息，请参阅 [-platform（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option)。 |
| `References` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 促使该任务将公共类型信息从指定项导入到当前项目中。 有关详细信息，请参阅 [-reference（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/reference-compiler-option)。<br /><br /> 你可以通过将元数据 `Aliases` 添加到原始的“参考”项，在 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 文件中指定 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 引用别名。 例如，在以下 Csc 命令行中设置别名“LS1”：<br /><br /> `CSC /r:LS1=MyCodeLibrary.dll /r:LS2=MyCodeLibrary2.dll *.cs`<br /><br /> 将使用：<br /><br /> `<Reference Include="MyCodeLibrary"> <Aliases>LS1</Aliases> </Reference>` |
| `Resources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 将 .NET Framework 资源嵌入到输出文件。<br /><br /> 传递到此参数的项可以具有名为 `LogicalName` 和 `Access` 的可选元数据条目。 `LogicalName` 对应于 `/resource` 开关的 `identifier` 参数，`Access` 对应于 `accessibility-modifier` 参数。 有关详细信息，请参阅 [-resource（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/resource-compiler-option)。 |
| `ResponseFiles` | 可选 `String` 参数。<br /><br /> 指定包含此任务命令的响应文件。 有关详细信息，请参阅 [@（指定响应文件）](/dotnet/csharp/language-reference/compiler-options/response-file-compiler-option)。 |
| `Sources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个或多个 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 源文件。 |
| `TargetType` | 可选 `String` 参数。<br /><br /> 指定输出文件的文件格式。 此参数可以具有 `library` 或 `winexe` 的值，前者将创建代码库 `exe`，代码库将创建控制台应用程序 `module`，应用程序将创建一个模块，后者将创建 Windows 程序。 默认值为 `library`。 有关详细信息，请参阅 [-target（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/target-compiler-option)。 |
| `TreatWarningsAsErrors` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则将所有警告视为错误。 有关详细信息，请参阅 [-warnaserror（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)。 |
| `UseHostCompilerIfAvailable` | 可选 `Boolean` 参数。<br /><br /> 指示该任务使用进程内编译器对象（如果可用）。 仅由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 使用。 |
| `Utf8Output` | 可选 `Boolean` 参数。<br /><br /> 记录使用 UTF-8 编码的编译器输出。 有关详细信息，请参阅 [-utf8output（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/utf8output-compiler-option)。 |
| `WarningLevel` | 可选 `Int32` 参数。<br /><br /> 指定编译器显示的警告级别。 有关详细信息，请参阅 [-warn（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/warn-compiler-option)。 |
| `WarningsAsErrors` | 可选 `String` 参数。<br /><br /> 指定将被视为错误的警告的列表。 有关详细信息，请参阅 [-warnaserror（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)。<br /><br /> 此参数替代 `TreatWarningsAsErrors` 参数。 |
| `WarningsNotAsErrors` | 可选 `String` 参数。<br /><br /> 指定不被视为错误的警告的列表。 有关详细信息，请参阅 [-warnaserror（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)。<br /><br /> 只有 `TreatWarningsAsErrors` 参数设置为 `true` 时，此参数才有用。 |
| `Win32Icon` | 可选 `String` 参数。<br /><br /> 在程序集中插入 .ico 文件，为输出文件赋予其在“文件资源管理器”中所需的外观  。  有关详细信息，请参阅 [-win32icon（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)。 |
| `Win32Manifest` | 可选 `String` 参数。<br /><br /> 指定要包含的 Win32 清单。 |
| `Win32Resource` | 可选 `String` 参数。<br /><br /> 在输出文件中插入 Win32 资源 (.res) 文件  。 有关详细信息，请参阅 [-win32res（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/win32res-compiler-option)。 |

## <a name="remarks"></a>备注
除上面列出的参数外，此任务还从 `Microsoft.Build.Tasks.ManagedCompiler` 类继承参数，该类继承自 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类（它自身继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类）。 有关这些其他参数的列表及其说明，请参阅 [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)。

## <a name="example"></a>示例
以下示例使用 `Csc` 任务来编译 `Compile` 项集合的源文件中的可执行文件。

```xml
<CSC
    Sources="@(Compile)"
    OutputAssembly="$(AppName).exe"
    EmitDebugInformation="true" />
```

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
