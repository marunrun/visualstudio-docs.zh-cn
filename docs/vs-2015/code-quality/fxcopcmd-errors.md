---
title: FxCopCmd 错误
ms.date: 10/19/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.author: gewarren
author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d723065e224058b7e269299aad2900f97a1425d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936642"
---
# <a name="fxcopcmd-tool-errors"></a>FxCopCmd 工具错误

FxCopCmd 不考虑所有错误是致命的。 如果 FxCopCmd 具有足够的信息来执行分部分析，它将执行分析和报告发生的错误。 错误代码，它是一个 32 位整数，包含与错误对应的数字值的按位组合。

下表介绍 FxCopCmd 返回的错误代码：

|Error|数字值|
|-----------|-------------------|
|没有错误|0x0|
|分析错误|0x1|
|规则例外|0x2|
|项目加载错误|0x4|
|程序集加载错误|0x8|
|规则库加载错误|0x10|
|导入报表加载错误|0x20|
|输出错误|0x40|
|命令行开关错误|0x80|
|初始化错误|0x100|
|程序集引用错误|0x200|
|BuildBreakingMessage|0x400|
|未知的错误|0x1000000|

**分析错误**返回为致命错误。 它指示无法完成分析。 如果适用，错误代码还包含错误的根本原因。 以下情况下将生成错误：

- 由于输入不足，无法执行分析。

- 分析引发不由 FxCopCmd 处理了异常。

- 指定的项目文件未找到或已损坏。

- 未指定输出选项，或无法写入该文件。

> [!NOTE]
> FxCopCmd 返回代码**程序集引用错误**0x200 本身是一条警告，而不是错误。 此返回代码指示缺少间接引用，但该 FxCopCmd 无法处理它们。 此警告意味着某些分析结果可能已泄露的可能性。 将视为**程序集引用错误**为错误与任何其他返回代码结合使用它时。

## <a name="see-also"></a>请参阅

- [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)