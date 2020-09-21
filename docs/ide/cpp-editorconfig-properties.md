---
title: C++ EditorConfig 格式设置约定
titleSuffix: ''
description: 了解如何使用 EditorConfig 进行 Visual Studio C++ 代码格式设置。
ms.date: 9/14/2020
author: jureid
ms.author: jureid
manager: jillfra
dev_langs:
- CPP
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: reference
ms.workload:
- cplusplus
monikerRange: vs-2019
ms.openlocfilehash: 31a7db73a4487267c2a74fe628d28b577d339aba
ms.sourcegitcommit: 14637be49401f56341c93043eab560a4ff6b57f6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078979"
---
# <a name="c-editorconfig-formatting-conventions"></a>C++ EditorConfig 格式设置约定

Visual Studio C++ 格式化程序具有一组丰富的可全局应用的可配置设置。 若要为特定工作区设置 C++ 格式设置，请使用 [clangformat](https://clang.llvm.org/docs/ClangFormat.html) 或 [EditorConfig](https://editorconfig.org/)。 Visual Studio 和 Visual Studio Code 具有对每个全局 Visual Studio C++ 格式设置的内置 EditorConfig 支持，其中 EditorConfig 设置优先。 这意味着，可以将 EditorConfig 文件添加到你的工作区，以便在更精细的级别配置 C++ 格式设置，并为参与项目的每个人强制实施一致的代码样式。

## <a name="c-formatting-conventions"></a>C++ 格式设置约定

C++ 格式设置 EditorConfig 设置以 `_cpp__` 为前缀。 下面是 EditorConfig 文件的类似内容的示例：

```ini
[\*.{c++,cc,cpp,cxx,h,h++,hh,hpp,hxx,inl,ipp,tlh,tli}]

cpp_indent_case_contents_when_block = true
cpp_new_line_before_open_brace_namespace = same_line
```

本文档的其余部分列出了 Visual Studio 和 VS Code 支持的所有 EditorConfig C++ 格式设置。

### <a name="indentation-settings"></a>缩进设置

缩进大括号

- 名称：`cpp_indent_braces`
- 值：`true`、`false`

相对该对象缩进各行

- 名称：`cpp_indent_multi_line_relative_to`
- 值：
  - `outermost_parenthesis` - 键入新行时，它会相对最外侧的左括号缩进。
  - `innermost_parenthesis` - 键入新行时，它会相对最内侧的左括号缩进。
  - `statement_begin` - 键入新行时，它会相对当前语句的开头缩进。

在圆括号内部输入新行时进行对齐

- 名称：`cpp_indent_within_parentheses`
- 值：
  - `align_to_parenthesis` - 将内容与左圆括号对齐。
  - `indent` - 缩进新行。

在现有代码中，不要使用圆括号中的新行的对齐设置

- 名称：`cpp_indent_preserve_within_parentheses`
- 值：`true`、`false`

缩进 case 内容

- 名称：`cpp_indent_case_contents`
- 值：`true`、`false`

缩进 case 标签

- 名称：`cpp_indent_case_labels`
- 值：`true`、`false`

缩进 case 语句后面的大括号

- 名称：`cpp_indent_case_contents_when_block`
- 值：`true`、`false`

缩进用作参数的 lambda 的大括号

- 名称：`cpp_indent_lambda_braces_when_parameter`
- 值：`true`、`false`

goto 标签的位置

- 名称：`cpp_indent_goto_labels`
- 值：
  - `one_left` - 向左缩进一次
  - `leftmost_column` - 移到最左侧的列
  - `none` - 保留缩进

预处理器指令的位置

- 名称：`cpp_indent_preprocessor`
- 值：
  - `one_left` - 向左缩进一次
  - `leftmost_column` - 移到最左侧的列
  - `none` - 保留缩进

缩进访问说明符

- 名称：`cpp_indent_access_specifiers`
- 值：`true`、`false`

缩进命名空间内容

- 名称：`cpp_indent_namespace_contents`
- 值：`true`、`false`

保留注释的缩进

- 名称：`cpp_indent_preserve_comments`
- 值：`true`、`false`

### <a name="newline-settings"></a>换行符设置

命名空间的左大括号的位置

- 名称：`cpp_new_line_before_open_brace_namespace`
- 值：
  - `new_line` - 移动到新行
  - `same_line` - 保持在同一行上，但在前面添加一个空格
  - `ignore` - 不要自动重新定位

类型的左大括号的位置

- 名称：`cpp_new_line_before_open_brace_type`
- 值：
  - `new_line` - 移动到新行
  - `same_line` - 保持在同一行上，但在前面添加一个空格
  - `ignore` - 不要自动重新定位

函数的左大括号的位置

- 名称：`cpp_new_line_before_open_brace_function`
- 值：
  - `new_line` - 移动到新行
  - `same_line` - 保持在同一行上，但在前面添加一个空格
  - `ignore` - 不要自动重新定位

控制块的左大括号的位置

- 名称：`cpp_new_line_before_open_brace_block`
- 值：
  - `new_line` - 移动到新行
  - `same_line` - 保持在同一行上，但在前面添加一个空格
  - `ignore` - 不要自动重新定位

lambda 的左大括号的位置

- 名称：`cpp_new_line_before_open_brace_lambda`
- 值：
  - `new_line` - 移动到新行
  - `same_line` - 保持在同一行上，但在前面添加一个空格
  - `ignore` - 不要自动重新定位
 
将范围大括号放到单独的行上

- 名称：`cpp_new_line_scope_braces_on_separate_lines`
- 值：`true`、`false`

对于空类型，将右大括号移动到左大括号所在的同一行

- 名称：`cpp_new_line_close_brace_same_line_empty_type`
- 值：`true`、`false`

对于空的函数体，将右大括号移动到左大括号所在的同一行

- 名称：`cpp_new_line_close_brace_same_line_empty_function`
- 值：`true`、`false`

将“catch”和相似的关键字放在新行上

- 名称：`cpp_new_line_before_catch`
- 值：`true`、`false`

将“else”放在新行上

- 名称：`cpp_new_line_before_else`
- 值：`true`、`false`

将 do-while 循环中的“while”放在新行上

- 名称：`cpp_new_line_before_while_in_do_while`
- 值：`true`、`false`

### <a name="spacing-settings"></a>间距设置

在函数名称与参数列表的左括号之间插入空格

- 名称：`cpp_space_before_function_open_parenthesis`
- 值：
  - `insert` - 插入空格
  - `remove` - 移除空格
  - `ignore` - 请勿更改空格

在参数列表的圆括号中插入空格

- 名称 `cpp_space_within_parameter_list_parentheses` 值：`true`、`false`

当参数列表为空时在圆括号之间插入空格

- 名称：`cpp_space_between_empty_parameter_list_parentheses`
- 值：`true`、`false`

在关键字与控制流语句中的左圆括号之间插入空格

- 名称：`cpp_space_after_keywords_in_control_flow_statements`
- 值：`true`、`false`

在控制语句的圆括号中插入空格

- 名称：`cpp_space_within_control_flow_statement_parentheses`
- 值：`true`、`false`

在 lambda 参数列表的左圆括号前面插入空格

- 名称：`cpp_space_before_lambda_open_parenthesis`
- 值：`true`、`false`

在 C 样式强制转换的圆括号中插入空格

- 名称：`cpp_space_within_cast_parentheses`
- 值：`true`、`false`

在 C 样式强制转换的右圆括号后面插入空格

- 名称：`cpp_space_after_cast_close_parenthesis`
- 值：`true`、`false`

在带圆括号的表达式的圆括号中插入空格

- 名称：`cpp_space_within_expression_parentheses`
- 值：`true`、`false`

在块的左大括号前插入空格

- 名称：`cpp_space_before_block_open_brace`
- 值：`true`、`false`

在空大括号之间插入空格

- 名称：`cpp_space_between_empty_braces`
- 值：`true`、`false`

在统一初始化和初始值设定项列表的左大括号前插入空格

- 名称：`cpp_space_before_initializer_list_open_brace`
- 值：`true`、`false`

在统一初始化和初始值设定项列表中插入空格

- 名称：`cpp_space_within_initializer_list_braces`
- 值：`true`、`false`

保留统一初始化和初始值设定项列表内的空格

- 名称：`cpp_space_preserve_in_initializer_list`
- 值：`true`、`false`

在左方括号前插入空格

- 名称：`cpp_space_before_open_square_bracket`
- 值：`true`、`false`

在方括号中插入空格

- 名称：`cpp_space_within_square_brackets`
- 值：`true`、`false`

在空方括号前插入空格

- 名称：`cpp_space_before_empty_square_brackets`
- 值：`true`、`false`

在空方括号之间插入空格

- 名称：`cpp_space_between_empty_square_brackets`
- 值：`true`、`false`

将多维数组的方括号组合在一起

- 名称：`cpp_space_group_square_brackets`
- 值：`true`、`false`

在 lambda 的方括号中插入空格

- 名称：`cpp_space_within_lambda_brackets`
- 值：`true`、`false`

SpaceBetweenEmptyLambdaBrackets

- 名称：`cpp_space_between_empty_lambda_brackets`
- 值：`true`、`false`

在逗号前插入空格

- 名称：`cpp_space_before_comma`
- 值：`true`、`false`

在逗号后面插入空格

- 名称：`cpp_space_after_comma`
- 值：`true`、`false`

移除成员运算符前后的空格

- 名称：`cpp_space_remove_around_member_operators`
- 值：`true`、`false`

在类型声明中的 base 的冒号前插入空格

- 名称：`cpp_space_before_inheritance_colon`
- 值：`true`、`false`

在构造函数中的冒号前插入空格

- 名称：`cpp_space_before_constructor_colon`
- 值：`true`、`false`

移除分号前的空格

- 名称：`cpp_space_remove_before_semicolon`
- 值：`true`、`false`

在分号后面插入空格

- 名称：`cpp_space_after_semicolon`
- 值：`true`、`false`

移除一元运算符和其操作数之间的空格

- 名称：`cpp_space_remove_around_unary_operator`
- 值：`true`、`false`

二元运算符的间距

- 名称：`cpp_space_around_binary_operator`
- 值：
  - `insert` - 在二元运算符的前后插入空格。
  - `remove` - 移除二元运算符周围的空格。
  - `ignore` - 不要更改二元运算符周围的空格。

赋值运算符的间距

- 名称：`cpp_space_around_assignment_operator`
- 值：
  - `insert` - 在赋值运算符周围插入空格。
  - `remove` - 移除赋值运算符周围的空格。
  - `ignore` - 不要更改赋值运算符周围的空格。

指针/引用对齐方式

- 名称：`cpp_space_pointer_reference_alignment`
- 值：
  - `left` - 左对齐。
  - `center` - 居中对齐。
  - `right` - 右对齐。
  - `ignore` - 保持不变。

条件运算符的间距

- 名称：`cpp_space_around_ternary_operator`
- 值：
  - `insert` - 在条件运算符周围插入空格。
  - `remove` - 移除条件运算符周围的空格。
  - `ignore` - 不要更改条件运算符周围的空格。

### <a name="wrapping-options"></a>换行选项

块的换行选项

- 名称：`cpp_wrap_preserve_blocks`
- 值：
  - `one_liners` - 不要对单行代码块换行。
  - `all_one_line_scopes` - 不要对左大括号和右大括号位于下一行上的代码块进行换行。
  - `never` - 始终为块应用新行设置。

## <a name="see-also"></a>请参阅

- [EditorConfig.org](https://editorconfig.org/)
- [支持语言服务的 EditorConfig](../extensibility/supporting-editorconfig.md)
- [代码编辑器功能](writing-code-in-the-code-and-text-editor.md)
