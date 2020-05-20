---
title: Linting R 代码
description: 如何使用 Visual Studio 针对 R 的内置 Linting 支持，包括 Linter 选项。
ms.date: 07/02/2018
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.text_editor.r.lint
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: aecf9d95fb8a3b2cda659e2694bff145424e150b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62970728"
---
# <a name="lint-r-code-in-visual-studio"></a>在 Visual Studio 中 Lint R 代码

Linter 分析代码，旨在发现潜在错误、格式设置问题和其他代码干扰（如假性空白）。 使用 Linter 还支持某些编码约定，例如标识符的命名方式。 此类约定在团队和其他合作情况下很有帮助。

针对 Visual Studio 的 R 工具 (RTVS) 内置适用于 R 的 Linter，可通过本文介绍的各个选项控制检查行为。 可以在“工具” > “选项” > “文本编辑器” > “R” > “Lint”下找到这些选项。

默认情况下禁用 Lint。 若要启用 Lint，请将“所有” > “启用 Lint”选项设置为“True”。

启用时，Linter 在你键入时在编辑器中运行。 以绿色波浪线指示问题。 例如，在下图中，RTVS 已识别六个 Lint 问题，包括使用 `=` 而不是 `<-` 进行赋值、函数参数周围缺少空格、使用 Pascal 拼写法和大写标识符，以及使用分号。 将鼠标悬停在问题上可查看问题描述。

![R 代码 Linter 输出的示例](media/linting-01.png)

通常根据项目或文件的需求，更改 Linter 选项。 例如，在线课程中的示例代码可能将 `=`（而不是 `<-`）与 Pascal 命名法标识符结合使用。 此类代码会频繁显示 Linter 警告，因为默认 Linter 选项设为标志 Pascal 命名法标识符。 处理此类代码时，可以禁用默认语法检查选项，而不用更正每个实例。

## <a name="assignment-group"></a>赋值组

| 选项 | 默认值 | Lint 效果 |
| --- | --- | --- |
| 强制使用\<- | **True** | 标识 `<-` 何时未用于赋值。 |

## <a name="naming-group"></a>命名组

这些选项标记使用不同命名约定的标识符：

| 选项 | 默认值 | Lint 效果 |
| --- | --- | --- |
| **标记 camelCase** | **False** | 标记使用 camelCase 的标识符。 |
| **标记长名称** | **False** | 标记名称长度超过“最大名称长度”设置的标识符  。 |
| **标记多个点** | **True** | 标记使用多个点的标识符。 |
| **标记 PascalCase** | **True** | 标记使用 PascalCase 的标识符。 |
| **标记 snake_case** | **False** | 标记使用下划线的标识符。 |
| **标记大写** | **True** | 标记全部使用大写的标识符。 |
| **最大名称长度** | **32** | 应用“标记长名称”设置的长度  。 |

## <a name="spacing-group"></a>空格组

这些选项默认情况下均设置为 True，用于控制 Linter 识别空格问题的位置：函数名称后、逗号前后、运算符前后、左右大括号位置、( 前和 () 内  。

## <a name="statements-group"></a>语句组

| 选项 | 默认值 | Lint 效果 |
| --- | --- | --- |
| **多个** | **True** | 标识多个语句位于同一行的情况。 |
| **分号** | **True** | 标识使用分号。 |

## <a name="text-group"></a>文本组

| 选项 | 默认值 | Lint 效果 |
| --- | --- | --- |
| **行长度限制** | **False** | 设置 Linter 标记行是的长度是否大于“最大行长度”选项  。 |
| **最大行长度** | **80** | 设置“行长度限制”选项应用的行长度  。 |

## <a name="whitespace-group"></a>空白组

这些选项默认状态下均设置为 True，用于控制 Linter 识别空白问题的位置：使用制表符、使用双引号、尾随空行和尾随空白  。