---
title: C# 编辑器格式设置选项
ms.date: 08/14/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Spacing
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.NewLines
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Indentation
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Wrapping
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.Code_Style.Formatting.General
helpviewer_keywords:
- formatting options [C#]
- Text editor Options dialog box, formatting
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1176232eb3354a9b425e9432eb83037367ee7706
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89312530"
---
# <a name="options-dialog-box-text-editor--c--code-style--formatting"></a>“选项”对话框：文本编辑器 \> C# \> 代码样式 \> 格式设置

在代码编辑器中使用“格式设置”选项页及其子页（[“缩进”](#indentation-page)、“新行”、“间距”和“换行”）为格式设置代码设置选项      。

要访问此选项页，请从菜单栏选择“工具” > 选项”   。 在“选项”对话框中，选择“文本编辑器” > “C#” > “代码样式” > “格式设置”      。

> [!TIP]
> “缩进”、“新行”、“间距”和“换行”子页均在底部显示一个预览窗口，其中显示每个选项的效果     。 若要使用预览窗口，请选择一个格式设置选项。 预览窗口显示选定选项的示例。 通过选择单选按钮或复选框更改设置时，会更新预览窗口，使其显示出新设置的效果。

## <a name="formatting-general-page"></a>“格式设置(常规)”页

### <a name="general-settings"></a>常规设置

这些设置将影响代码编辑器向代码应用格式设置选项的时间  。

|Label|描述|
|-----------|-----------------|
|键入时自动格式化 |取消选择时，禁用“format statement on ;”和“format block  on }”选项   。|
|输入 ; 时自动设置语句格式 |如果选中此项，会根据为编辑器选择的格式设置选项在完成时对语句进行格式设置。|
|在 } 后自动格式化程序块 |如果选中此项，完成代码块后，立即根据为编辑器选择的格式设置选项设置代码块的格式。|
|返回时自动格式化 |如果选中此项，将在按 Enter 时设置文本的格式，使其与为编辑器选择的格式设置选项一致  。|
|粘贴时自动设置格式 |如果选中此项，设置粘贴到编辑器中的文本的格式，使其与为编辑器选择的格式设置选项一致。|

::: moniker range="vs-2019"

如果之前在 Visual Studio 2017 中使用“设置文档格式”命令为 C# 文件应用代码样式设置，则该功能现作为[“代码清理”](../code-styles-and-code-cleanup.md#apply-code-styles)提供   。

::: moniker-end

::: moniker range="vs-2017"

### <a name="format-document-settings"></a>“设置文档格式”设置

这些设置配置“设置文档格式”命令以对文件执行其他代码清理  。 有关如何应用这些设置的详细信息，请参阅[“设置文档格式”命令](../code-styles-and-code-cleanup.md#apply-code-styles)。

|Label|描述|相应的 EditorConfig 和工具 > 选项规则|
|-----------|-----------------|-----------------|-----------------|
|**应用所有 C# 格式规则（缩进、换行、间距）**|“设置文档格式”命令始终修复格式问题  。 此设置不可更改。| [Core EditorConfig 选项](../../ide/create-portable-custom-editor-options.md)<br/>[.NET EditorConfig 格式设置选项](../../ide/editorconfig-formatting-conventions.md)<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “格式设置”> [“缩进”、“新行”、“间距”或“换行”]         |
|**在格式设置期间执行额外的代码清理**|选中后，在 Edit.FormatDocument 命令上应用以下指定规则的修复程序  。| 不可用 |
|**删除不必要的 Using**|选中后，触发 Edit.FormatDocument 时删除不必要的 `using` 指令  。| 不可用 |
|**对 Using 排序**|选中后，触发 Edit.FormatDocument 时对 `using` 指令排序  。| dotnet_sort_system_directives_first<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “高级” > [对 using 排序时将“System”指令排在第一位]       |
|**为单行控制语句添加/删除大括号**|选中后，触发 Edit.FormatDocument 时，在单行控制语句中添加或删除大括号  。| csharp_prefer_braces<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “代码块首选项” > “首选大括号”        |
|**添加可访问性修饰符**|选中后，在触发 Edit.FormatDocument 时添加缺少的可访问性修饰符  。| dotnet_style_require_accessibility_modifiers |
|**对可访问性修饰符排序**|选中后，在触发 Edit.FormatDocument 时对可访问性修饰符排序  。| csharp_preferred_modifier_order<br/>visual_basic_preferred_modifier_order |
|**应用表达式/程序块主体首选项**|选中后，触发 Edit.FormatDocument 时将 expression-bodied 成员转换为程序块主体，反之亦然  。| [Expression-bodied 成员 EditorConfig 选项](../../ide/editorconfig-language-conventions.md#expression-bodied-members)<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “表达式首选项” > “将表达式主体用于方法、构造函数等”        。 |
|**应用隐式/显式类型首选项**|选中后，触发 Edit.FormatDocument 时将 `var` 转换为显式类型，反之亦然  。| [显式类型 EditorConfig 选项](../../ide/editorconfig-language-conventions.md#implicit-and-explicit-types)<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > [“var”首选项]       |
|**应用内联“out”变量首选项**|选中后，触发 Edit.FormatDocument 时尽可能内联 `out` 变量  。| csharp_style_inlined_variable_declaration<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “变量首选项” > “首选内联变量声明”        |
|**应用语言/框架类型首选项**|选中后，触发 Edit.FormatDocument 时将语言类型转换为框架类型，反之亦然  。| dotnet_style_predefined_type_for_locals_parameters_members<br/>dotnet_style_predefined_type_for_member_access<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “预定义类型首选项”       |
|**应用对象/集合初始化首选项**|选中后，触发 Edit.FormatDocument 时尽可能使用对象和集合初始值设定项  。| dotnet_style_object_initializer<br/>dotnet_style_collection_initializer<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “表达式首选项” > “首选对象初始值设定项”或“首选集合初始值设定项”         |
|**应用“this”限定首选项**|选中后，触发 Edit.FormatDocument 时应用 `this.` 首选项  。| [this. 限定 EditorConfig 选项](../../ide/editorconfig-language-conventions.md#this-and-me)<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > [“this.”首选项]       |
|**尽可能将私有字段设为只读**|选中后，触发 Edit.FormatDocument 时尽可能将私有字段设为 `readonly`  。| dotnet_style_readonly_field<br/><br/>“工具” > “选项” > “文本编辑器” > “C#” > “代码样式” > “字段首选项” > “首选只读”        |
|**删除不必要的强制转换**|选中后，触发 Edit.FormatDocument 时尽可能删除不必要的强制转换  。| 不可用 |
|**删除未使用的变量**|选中后，触发 Edit.FormatDocument 时删除未使用的变量  。| 不可用 |

![Visual Studio 中 C# 的代码清理设置](media/format-document-settings.png)

::: moniker-end

## <a name="indentation-page"></a>“缩进”页

自动设置代码的格式时，将应用此页上的“缩进”选项。 自动设置代码格式的一个示例情形是，在选中“粘贴时自动设置格式”的情况下将代码粘贴到文件中时  。 （“粘贴时自动设置格式”选项位于“格式设置” > “常规”下    。）

![Visual Studio 中的 C# 文本编辑器缩进选项](media/csharp-indentation-options.png)

> [!TIP]
> 此外，在“文本编辑器” > “C#” > “选项卡”选项页上还有缩进选项    。 这些选项仅确定你在行尾按 Enter 时，代码编辑器将光标置于何处  。
>
> ![Visual Studio 中的 C# 文本编辑器选项卡选项](media/csharp-tabs-options.png)

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
