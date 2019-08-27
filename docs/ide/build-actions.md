---
title: 文件生成操作
ms.date: 11/19/2018
ms.technology: vs-ide-compile
ms.topic: reference
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eac31e0fe12d703e11d286b629e7e690f641f4e3
ms.sourcegitcommit: 6b0503ed8d25454d6e39a8e606910b3fa58cf1d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2019
ms.locfileid: "68981097"
---
# <a name="build-actions"></a>生成操作

Visual Studio 项目中的所有文件都具有生成操作。 生成操作控制编译项目时文件发生的情况。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中的生成操作](/visualstudio/mac/build-actions)。

## <a name="set-a-build-action"></a>设置生成操作

若要设置文件的生成操作，通过选择“解决方案资源管理器”中的文件并按 Alt+Enter，在“属性”窗口中打开文件的属性     。 或者，右键单击“解决方案资源管理器”中的文件，然后选择“属性”   。 在“属性”窗口的“高级”部分下，使用“生成操作”旁边的下拉列表为文件设置生成操作    。

![Visual Studio 中的文件生成操作](media/build-actions.png)

## <a name="build-action-values"></a>生成操作值

C# 和 Visual Basic 项目文件的一些更常见的生成操作如下所示：

|生成操作 | 项目类型 | 说明 |
|-|-|
| **AdditionalFiles** | C#, Visual Basic | 作为输入传递给 C# 或 Visual Basic 编译器的非源文本文件。 此生成操作主要用于向[分析器](../code-quality/roslyn-analyzers-overview.md)提供输入，项目引用这些分析器来验证代码质量。 有关详细信息，请参阅[使用其他文件](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Using%20Additional%20Files.md)。|
| **ApplicationDefinition** | WPF | 定义应用程序的文件。 首次创建项目时，这是 App.xaml  。 |
| **CodeAnalysisDictionary** | .NET | 自定义单词字典，代码分析使用该字典进行拼写检查。 请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)|
| **编译** | 任何 | 文件被传递到编译器作为源文件。|
| **内容** | .NET | 标记为“内容”  的文件可以通过调用 <xref:System.Windows.Application.GetContentStream%2A?displayProperty=nameWithType> 作为流进行检索。 对于 ASP.NET 项目，在部署站点时包含这些文件，作为站点的一部分。|
| **DesignData** | WPF | 用于 XAML ViewModel 文件，允许在设计时使用虚拟类型和示例数据查看用户控件。 |
| **DesignDataWithDesignTimeCreateable** | WPF | 与 DesignData  类似，但具有实际类型。  |
| **嵌入式资源** | .NET | 文件被传递到 C# 编译器作为嵌入程序集中的资源。 可以调用 <xref:System.Reflection.Assembly.GetManifestResourceStream%2A?displayProperty=fullName> 从程序集中读取文件。|
| **EntityDeploy** | .NET | 用于指定 EF 项目部署的实体框架 (EF) .edmx 文件。 |
| **Fakes** | .NET | 用于 Microsoft Fakes 测试框架。 请参阅 [使用 Microsoft Fakes 隔离受测代码](../test/isolating-code-under-test-with-microsoft-fakes.md) |
| **无** | 任何 | 文件不以任何方式生成。 例如，此值可用于文档文件，例如“ReadMe”文件。|
| **页** | WPF | 将 XAML 文件编译为二进制 .baml 文件，以便在运行时提升加载速度。 |
| **资源** | WPF | 指定将文件嵌入到扩展名为 .g.resources  的程序集清单资源文件中。 |
| **阴影** | .NET | 用于包含生成的程序集文件名列表的 .accessor 文件，每行一个。 对于列表中的每个程序集，生成名称为 `ClassName_Accessor` 的公共类，这些类与原始类类似，但具有公共方法，而不是私有方法。 用于单元测试。 |
| **初始屏幕** | WPF | 指定应用启动时在运行时显示的图像文件。 |
| **XamlAppDef** | Windows Workflow Foundation | 指示生成操作将工作流 XAML 文件生成为具有嵌入式工作流的程序集。 |

> [!NOTE]
> 可以为特定项目类型定义其他生成操作，因此，生成操作列表取决于项目类型，可能出现不在此列表中的值。

## <a name="see-also"></a>请参阅

- [C# 编译器选项](/dotnet/csharp/language-reference/compiler-options/listed-alphabetically)
- [Visual Basic 编译器选项](/dotnet/visual-basic/reference/command-line-compiler/compiler-options-listed-alphabetically)
- [生成操作 (Visual Studio for Mac)](/visualstudio/mac/build-actions)
