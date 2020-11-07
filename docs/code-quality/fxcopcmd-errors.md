---
title: FxCopCmd 错误
ms.date: 10/19/2016
description: 了解 FxCopCmd 命令返回的错误代码。 查看每个代码表示的错误类型，并了解如何识别错误。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
ms.author: mikejo
author: mikejo5000
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 88c900ec10ea13e7f9d7092769565703bf52fe8c
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94348927"
---
# <a name="fxcopcmd-tool-errors"></a>FxCopCmd 工具错误

FxCopCmd 不会将所有错误视为严重错误。 如果 FxCopCmd 具有足够的信息来执行部分分析，则会执行分析并报告发生的错误。 错误代码是一个32位整数，它包含与错误相对应的数字值的按位组合。

下表描述了 FxCopCmd 返回的错误代码：

|错误|数值|
|-----------|-------------------|
|无错误|0x0|
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
|未知错误|0x1000000|

对于严重错误，将返回 **分析错误** 。 它表示分析无法完成。 如果适用，错误代码还包含错误的根本原因。 以下条件会生成错误：

- 由于输入不足，无法执行分析。

- 分析引发了不由 FxCopCmd 处理的异常。

- 指定的项目文件找不到或已损坏。

- 未指定输出选项或无法写入文件。

> [!NOTE]
> FxCopCmd 返回代码 **程序集引用错误** 0x200 本身就是警告而不是错误。 此返回代码指示缺少间接引用，但 FxCopCmd 可以处理它们。 警告意味着某些分析结果可能已泄露。 将 **程序集引用错误** 视为与任何其他返回代码结合使用时的错误。

## <a name="see-also"></a>请参阅

- [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)
