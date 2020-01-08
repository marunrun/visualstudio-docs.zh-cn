---
title: “项目设计器”->“生成”页 (C#)
ms.date: 06/20/2017
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuild
helpviewer_keywords:
- Build options [C#]
- Project Designer, Build page
ms.assetid: 77ff1bfc-d633-4634-ba29-9afdb6d7e362
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 619840f417c922b4019bafffca8d66c9b1c939e2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596861"
---
# <a name="build-page-project-designer-c"></a>“项目设计器”->“生成”页 (C#)

使用“项目设计器”  的“生成”  页指定项目的生成配置属性。 此页仅适用于 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目。

若要访问“生成”  页，请在“解决方案资源管理器”  中选择项目节点（而非“解决方案”  节点）。 然后依次在菜单上选择“查看”、“属性页”   。 “项目设计器”出现后，选择“生成”选项卡  。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="configuration-and-platform"></a>配置和平台

通过以下选项，可选择要显示或修改的配置和平台。

> [!NOTE]
> 使用简化的生成配置，项目系统可确定是生成调试版本还是发行版本。 因此，不会显示这些选项。 有关详细信息，请参阅[如何：设置调试和发布配置](../../debugger/how-to-set-debug-and-release-configurations.md)。

**配置**

指定要显示或修改的配置设置。 设置可以是“活动(调试)”  （默认设置）、“调试”  、“发布”  或“所有配置”  。

**平台**

指定要显示或修改的平台设置。 默认设置是“活动(任意 CPU)”  。 可使用“配置管理器”  更改活动平台。 有关详细信息，请参阅[如何：创建和编辑配置](../../ide/how-to-create-and-edit-configurations.md)。

## <a name="general"></a>常规

通过以下选项，可配置多个 C# 编译器设置。

“条件编译符”**号**

指定要在其上执行条件编译的符号。 用分号 (“;”) 分隔符号。 有关详细信息，请参阅 [/define（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/define-compiler-option)。

“定义 DEBUG 常量” 

将 DEBUG 定义为应用中所有源代码文件中的符号。 选择此选项相当于使用 `/define:DEBUG` 命令行选项。

“定义 TRACE 常量” 

将 TRACE 定义为应用中所有源代码文件中的符号。 选择此选项相当于使用 `/define:TRACE` 命令行选项。

目标平台 

指定将作为输出文件目标的处理器。 对于任何 32 位 Intel 兼容处理器，请选择“x86”  ；对于任何 64 位 Intel 兼容处理器，请选择“x64”  ；对于 ARM 处理器，请选择“ARM”  ；或选择“任何 CPU”  指定可接受任何处理器。 “任何 CPU”  是项目的默认值，因为这允许在最广泛的硬件上运行应用程序。

有关详细信息，请参阅 [/platform（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option)。

**首选 32 位**

如果选中了“首选 32 位”  复选框，则应用程序可在 32 位和 64 位版本的 Windows 上作为 32 位应用程序运行。 如果清除了该复选框，则应用程序在 32 位版的 Windows 上作为 32 位应用程序运行，而在 64 位版的 Windows 上作为 64 位应用程序运行。

如果将应用程序作为 64 位应用程序运行，则指针大小将加倍，并且会出现与其他独占式 32 位库的兼容性问题。 仅在需要 4 GB 以上内存或 64 位指令可带来显著性能改善的情况下，运行 64 位应用程序才会非常有用。

仅在以下条件都为 true 的情况下，才可使用此复选框：

- 在“生成”  页上，“平台目标”  列表设置为“任何 CPU”  。

- 在“应用程序”  页上，“输出类型”  列表指定项目是应用程序。

- 在“应用程序”  页上，“目标框架”  列表指定 .NET Framework 4.5。

**允许不安全代码**

允许使用[不安全](/dotnet/csharp/language-reference/keywords/unsafe)关键字进行编译的代码。 有关详细信息，请参阅 [/unsafe（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/unsafe-compiler-option)。

**优化代码**

启用或禁用编译器执行的优化，使输出文件更小、更快、更有效。 有关详细信息，请参阅 [/optimize（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/optimize-compiler-option)。

## <a name="errors-and-warnings"></a>错误和警告

以下设置用于配置生成过程的错误和警告选项。

“警告等级” 

指定编译器警告的显示等级。 有关详细信息，请参阅 [/warn（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/warn-compiler-option)。

“禁止显示警告” 

阻止编译器生成一个或多个警告的能力。 使用逗号或分号分隔多个警告编号。 有关详细信息，请参阅 [/nowarn（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/nowarn-compiler-option)。

## <a name="treat-warnings-as-errors"></a>将警告视为错误

以下设置用于指定视为错误的警告。 选择下列选项之一，指示生成遇到警告时，返回错误的条件。 有关详细信息，请参阅 [/warnaserror（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)。

**无** - 不将任何警告视为错误。

**所有** - 将所有警告视为错误。

**特定警告** - 将特定警告视为错误。 使用逗号或分号分隔多个警告编号。

> [!TIP]
> 如果不希望将代码分析警告视为错误，请参阅[代码分析常见问题解答](../../code-quality/analyzers-faq.md#treat-warnings-as-errors)。

## <a name="output"></a>Output

以下设置用于配置生成过程的输出选项。

“输出路径” 

指定该项目配置的输出文件的位置。 在此框中输入生成输出的路径，或选择“浏览”  按钮指定路径。 该路径是相对的；如果输入绝对路径，将保存为相对路径。 默认路径为 bin\Debug 或 bin\Release\\。

使用简化的生成配置，项目系统可确定是生成调试版本还是发行版本。 使用“调试”  菜单 (F5) 中的“生成”  命令，会将生成放置在调试位置中（无论指定的“输出路径”  为何）。 但是，“生成”  菜单上的“生成”  命令会将其放在指定的位置。 有关详细信息，请参阅[了解生成配置](../../ide/understanding-build-configurations.md)。

“XML 文档文件” 

指定要在其中处理文档注释的文件名称。 有关详细信息，请参阅 [/doc（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/doc-compiler-option)。

“注册 COM 互操作” 

指示托管应用程序将公开一个允许 COM 对象与托管应用程序进行交互的 COM 对象（COM 可调用包装器）。 必须在此应用程序的“项目设计器”  的[应用程序页](../../ide/reference/application-page-project-designer-visual-basic.md)中，将“输出类型”  属性设置为“类库”  ，才能使用“注册 COM 互操作”  属性。 若要了解可能会包含在 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 应用程序中，且将作为 COM 对象公开的类示例，请参阅 [COM 类示例](/dotnet/csharp/programming-guide/interop/example-com-class)。

“生成序列化程序集” 

指定编译器是否将使用 XML 序列化程序生成器工具 (Sgen.exe) 创建 XML 序列化程序集。 序列化程序集可以提高 <xref:System.Xml.Serialization.XmlSerializer> 的启动性能（如果已使用该类序列化代码中的类型）。 默认情况下，此选项设置为“自动”，用于指定仅在已使用 <xref:System.Xml.Serialization.XmlSerializer> 将代码中的类型编码为 XML 的情况下，才会生成序列化程序集  。 若设置为“关闭”，则指定永远不会生成序列化程序集，无论代码是否使用 <xref:System.Xml.Serialization.XmlSerializer>  。 若设置为“打开”  ，则指定始终会生成序列化程序集。 序列化程序集命名为 `TypeName`.XmlSerializers.dll。 有关详细信息，请参阅 [XML 序列化程序生成器工具 (Sgen.exe)](/dotnet/framework/serialization/xml-serializer-generator-tool-sgen-exe)。

**高级**

单击以显示[“高级生成设置”对话框 (C#)](../../ide/reference/advanced-build-settings-dialog-box-csharp.md)。

## <a name="see-also"></a>请参阅

- [项目属性引用](../../ide/reference/project-properties-reference.md)
- [C# 编译器选项](/dotnet/csharp/language-reference/compiler-options/index)
