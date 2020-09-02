---
title: “编译”页, 项目设计器 (Visual Basic)
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesCompile
helpviewer_keywords:
- compilation, Visual Basic projects
- compilation, options [Visual Basic]
- compilers, Visual Basic options
- compilation, instructions [Visual Basic]
- compiler options, Visual Basic
- Project Designer, Compile page
- Compile page in Project Designer
ms.assetid: b2a80230-906e-4e85-b3e0-fcd9c40426e1
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d9ffdfe4abbef5701cc060171ecbc379ae3a9215
ms.sourcegitcommit: 26178b116cbf7353fee6ca989b8d872114f7b405
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284312"
---
# <a name="compile-page-project-designer-visual-basic"></a>“编译”页, 项目设计器 (Visual Basic)

使用项目设计器的“编译”页来指定编译指令  。 此外，还可在此页上指定高级编译器选项以及预先生成或后期生成的事件。

若要访问“编译”页，请在“解决方案资源管理器”中选择项目节点（而非“解决方案”节点）。 然后在菜单栏上依次选择“项目”  、“属性”  。 “项目设计器”出现时，单击“编译”选项卡  。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="configuration-and-platform"></a>配置和平台

通过以下设置，可选择要显示或修改的配置和平台。

> [!NOTE]
> 使用简化的生成配置，项目系统可确定是生成调试版本还是发行版本。 因此，不会显示“配置”和“平台”列表   。

**配置**

指定要显示或修改的配置设置。 这些设置为“调试”（默认）、“发布”或“所有配置”    。 有关详细信息，请参阅[了解生成配置](../../ide/understanding-build-configurations.md)以及[如何：创建和编辑配置](../../ide/how-to-create-and-edit-configurations.md)。

**平台**

指定要显示或修改的平台设置。 可指定“任何 CPU”（默认）、“x64”或“x86”    。

## <a name="compiler-configuration-options"></a>编译器配置选项

通过以下设置，可设置编译器配置选项。

**生成输出路径**

指定该项目配置的输出文件的位置。 在此框中键入生成输出的路径，或单击“浏览”  按钮选择路径。 请注意，该路径是相对的；如果输入绝对路径，将保存为相对路径。 默认路径为 bin\Debug 或 bin\Release\\。

使用简化的生成配置，项目系统可确定是生成调试版本还是发行版本。 使用“调试”菜单 (F5) 中的“生成”命令，会将生成放置在调试位置中（无论指定的“输出路径”为何）。 但是，“生成”菜单上的“生成”命令会将其放在指定的位置。

Option Explicit 

指定是否允许隐式声明变量。 选择“开启”，允许显式声明变量  。 如果变量在使用之前未被声明，该设置会导致编译器报告错误。 选择“关闭”，允许隐式声明变量  。

此设置对应于 [/optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit) 编译器选项。

如果源代码文件包含 [Option Explicit 语句](/dotnet/visual-basic/language-reference/statements/option-explicit-statement)，则语句中的 `On` 或 `Off` 值会替代“编译”页上的“Option Explicit”设置   。

创建新项目时，将“编译”页上的“Option Explicit”设置设置为“选项”对话框中的“Option Explicit”设置     。 若要查看或更改此对话框中的设置，请单击“工具”菜单上的“选项”   。 在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”    。 “VB 默认值”中的“Option Explicit”初始默认设置为“开启”    。

通常不建议将“Option Explicit”设置为 `Off`。 在一个或多个位置拼错变量名称，将会在程序运行时导致意想不到的结果。

Option strict 

指定是否强制执行严格类型语义。 “Option Strict”为“开启”时   ，以下情况会导致编译时错误：

- 隐式收缩转换

- 后期绑定

- 隐式键入会导致 `Object` 类型

隐式数据类型转换为收缩转换时，将发生隐式收缩转换错误。 有关详细信息，请参阅 [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)[隐式转换和显式转换](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions)以及[扩大转换和收缩转换](/dotnet/visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions)。

如果将对象分配给声明为 `Object` 类型的变量，则该对象为晚期绑定。 有关详细信息，请参阅 [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)以及[早期绑定和晚期绑定](/dotnet/visual-basic/programming-guide/language-features/early-late-binding)。

如果无法为已声明的变量推断出合适的类型，则会发生隐式对象类型错误，因此 `Object` 类型是推断出来的。 这主要是在未使用 `As` 子句的情况下使用 `Dim` 语句声明变量，且 `Option Infer` 为关闭时发生的。 有关详细信息，请参阅 [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)、[Option Infer 语句](/dotnet/visual-basic/language-reference/statements/option-infer-statement)和 [Visual Basic 语言规范](/dotnet/visual-basic/reference/language-specification)。

“Option Strict”设置对应于 [/optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) 编译器选项。

如果源代码文件包含 [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)，则语句中的 `On` 或 `Off` 值会替代“编译”页上的“Option Strict”设置   。

创建项目时，将“编译”页上的“Option Strict”设置设置为“选项”对话框中的“Option Strict”设置     。 若要查看或更改此对话框中的设置，请单击“工具”菜单上的“选项”   。 在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”    。 “VB 默认值”中的“Option Strict”初始默认设置为“关闭”    。

**Option Strict 各个警告**

“编译”页的“警告配置”部分具有与 `Option Strict` 开启时引起编译时错误的三种情况相对应的设置。 这些设置如下：

- 隐式转换 

- 晚期绑定；调用可能在运行时失败 

- 隐式类型；假定为对象 

“Option Strict”设置为“开启”时，所有这三个警告配置设置都将被设置为“错误”    。 “Option Strict”设置为“关闭”时，所有这三个设置都将被设置为“无”    。

可单独将各个警告配置设置更改为“无”、“警告”或“错误”    。 如果三个警告配置都设置为“错误”  ，则 `On` 会出现在 `Option strict` 框中。 如果三个都设置为“无”，则 `Off` 会出现在此框中。 对于这些配置的任何其他组合，显示“(自定义)”  。

Option compare 

指定要使用的字符串比较的类型。 选择“二进制”可指示编译器使用二进制的、区分大小写的字符串比较  。 选择“文本”则使用特定于区域设置的、不区分大小写的文本字符串比较  。

此设置对应于 [/optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare) 编译器选项。

如果源代码文件包含 [Option Compare](/dotnet/visual-basic/language-reference/statements/option-compare-statement) 语句，则语句中 `Binary` 或 `Text` 值将替代“编译”页上的“Option Compare”设置   。

创建项目时，将“编译”页上的“Option Compare”设置设置为“选项”对话框中的“Option Compare”设置的值     。 若要查看或更改此对话框中的设置，请单击“工具”菜单上的“选项”   。 在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”    。 “VB 默认值”中的“Option Compare”初始默认设置为“二进制”    。

Option infer 

指定是否允许使用变量声明中的本地类型推断。 选择“开启”，允许使用本地类型推断  。 选择“关闭”，阻止本地类型推断  。

此设置对应于 [/optioninfer](/dotnet/visual-basic/reference/command-line-compiler/optioninfer) 编译器选项。

如果源代码文件包含 [Option Infer 语句](/dotnet/visual-basic/language-reference/statements/option-infer-statement)，则语句中的 `On` 或 `Off` 值会替代“编译”页上的“Option Infer”设置   。

创建项目时，将“编译”页上的“Option Infer”设置设置为“选项”对话框中的“Option Infer”设置的值     。 若要查看或更改此对话框中的设置，请单击“工具”菜单上的“选项”   。 在“选项”对话框中，展开“项目和解决方案”，然后单击“VB 默认值”    。 “VB 默认值”中的“Option Infer”初始默认设置为“开启”    。

**目标 CPU**

指定将作为输出文件目标的处理器。 对于任何 32 位 Intel 兼容处理器，请指定“x86”  ；对于任何 64 位 Intel 兼容处理器，请指定“x64”  ；对于任何 ARM 处理器，请指定“ARM”  ；选择“任何 CPU”，指定可接受任何处理器  。 “任何 CPU”  是新项目的默认值，因为它允许在最广泛的各类硬件上运行应用程序。

有关详细信息，请参阅 [/platform (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/platform)。

**首选 32 位**

如果选中了“首选 32 位”  复选框，则应用程序可在 32 位和 64 位版本的 Windows 上作为 32 位应用程序运行。 否则，应用程序在 32 位版本的 Windows 上作为 32 位应用程序运行，而在 64 位版本的 Windows 上作为 64 位应用程序运行。

作为 64 位应用程序运行，会使指针大小增加一倍，并且可能会导致 32 位专用库的兼容性问题。 只有运行速度明显加快或需要超过 4 GB 的内存时，才能将应用程序作为 64 位运行。

仅在以下条件都为 true 的情况下，才可使用此复选框：

- 在“编译”页上，“目标 CPU”列表被设置为“任何 CPU”    。

- 在“应用程序”页上，“应用程序类型”列表指定项目为应用程序   。

- 在“应用程序”  页上，“目标框架”  列表指定 .NET Framework 4.5。

**警告配置**

此表列出了生成条件以及对应于每个条件的通知级别（“无”、“警告”或“错误”）    。

默认情况下，所有编译器警告都在编译期间添加到任务列表中。 选择“禁用所有警告”，指示编译器不发布警告或错误  。 如果希望编译器将警告视为必须修复的错误，请选择“将所有警告视为错误”  。

**禁用所有警告**

指定是否允许编译器按照此文档中前面所述的“条件和通知”表中的说明发布通知  。 默认情况下清除此复选框。 选中此复选框，指示编译器不发布警告或错误。

此设置对应于 [/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) 编译器选项。

**将所有警告视为错误**

指定如何处理警告。 默认情况下清除此复选框，以便所有警告通知仍设置为“警告”  。 选中此复选框，将所有警告通知更改为“错误”  。

此选项只有在清除“禁用所有警告”时才可用  。

**生成 XML 文档文件**

指定是否生成文档信息。 默认情况下，此复选框处于选中状态，指示编译器生成文档信息并将这些信息包含在一个 XML 文件中。 清除此复选框，指示编译器不创建任何文档。

此设置对应于 [/doc](/dotnet/visual-basic/reference/command-line-compiler/doc) 编译器选项。

“注册 COM 互操作” 

指定托管应用程序是否将公开一个 COM 对象（可调用 COM 的包装），以使 COM 对象可以与托管应用程序进行交互。

默认情况下清除此复选框，以指定应用程序不允许 COM 互操作。 选中此复选框，允许 COM 互操作。

此选项对于“Windows 应用程序”或“控制台应用程序”项目不可用。

**生成事件**

单击此按钮，访问“生成事件”对话框  。 使用此对话框为指定项目的预先生成和后期生成配置说明。 此对话框仅适用于 Visual Basic 项目。 有关详细信息，请参阅[“生成事件”对话框 (Visual Basic)](../../ide/reference/build-events-dialog-box-visual-basic.md)。

**高级编译选项**

单击此按钮，访问“高级编译器设置”对话框  。 使用“高级编译器设置”对话框，指定项目的高级生成配置属性  。 此对话框仅适用于 Visual Basic 项目。 有关详细信息，请参阅[“高级编译器设置”对话框 (Visual Basic)](../../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)。

## <a name="see-also"></a>请参阅

- [如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [Visual Basic 命令行编译器](/dotnet/visual-basic/reference/command-line-compiler/index)
- [如何：创建和编辑配置](../../ide/how-to-create-and-edit-configurations.md)
