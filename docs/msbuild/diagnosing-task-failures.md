---
title: 诊断任务故障 | Microsoft Docs
ms.date: 09/25/2019
ms.topic: troubleshooting
f1_keywords:
- MSBuild.ToolTask.ToolCommandFailed
dev_langs:
- VB
- CSharp
- C++
- jsharp
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89dcb8bddf2c92406ad5eff952d1f4050d7f9262
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593273"
---
# <a name="diagnosing-task-failures"></a>诊断任务故障

<xref:Microsoft.Build.Utilities.ToolTask> 派生类运行工具进程（如果任务未记录更具体的错误，则会返回非零退出代码）时，会发出 `MSB6006`。

## <a name="identifying-the-failing-task"></a>识别失败的任务

遇到任务错误时，应首先识别失败的任务。

错误文本会指明工具名称（<xref:Microsoft.Build.Utilities.ToolTask.ToolName> 的任务实现提供的易记名称或可执行文件的名称）和数字退出代码。 例如，在

```text
error MSB6006: "custom tool" exited with code 1.
```

工具名称为 `custom tool`，退出代码为 `1`。

### <a name="command-line-builds"></a>命令行生成

如果将生成配置为包含摘要（默认），则摘要将如下所示：

```text
Build FAILED.

"S:\MSB6006_demo\MSB6006_demo.csproj" (default target) (1) ->
(InvokeToolTask target) ->
  S:\MSB6006_demo\MSB6006_demo.csproj(19,5): error MSB6006: "custom tool" exited with code 1.
```

此结果表示错误发生在项目 `S:\MSB6006_demo\MSB6006_demo.csproj` 中名为 `InvokeToolTask` 的目标中文件 `S:\MSB6006_demo\MSB6006_demo.csproj` 第 19 行中定义的任务。

### <a name="in-visual-studio"></a>在 Visual Studio 中

Visual Studio 错误列表中的 `Project`、`File` 和 `Line` 列中提供了相同的信息。

## <a name="finding-more-failure-information"></a>查找更多故障信息

当任务未记录特定的错误时，将发出此错误。 无法记录错误通常是因为未将任务配置为理解它所调用的工具发出的错误格式。

正常情况下的工具通常会向其标准输出或错误流发出一些上下文或错误信息，任务默认捕获并记录此信息。 在出现错误之前，查看日志条目以获取其他信息。 重新运行具有较高日志级别的生成时，可能需要保留此信息。

## <a name="next-steps"></a>后续步骤

但愿日志记录中指出的其他上下文或错误显示了问题的根本原因。

否则，你可能需要通过检查作为失败任务输入的属性和项来缩小可能的原因范围。
