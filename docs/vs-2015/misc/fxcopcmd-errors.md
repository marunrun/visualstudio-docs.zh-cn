---
title: FxCopCmd 错误 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
caps.latest.revision: 12
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3e0770654f564c57cf576666dcd9575f47d9ce1c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432280"
---
# <a name="fxcopcmd-errors"></a>FxCopCmd 错误
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
  
 严重错误会返回分析错误。 它指示无法完成分析。 如果适用，错误代码还包含错误的根本原因。 以下情况下将生成错误：  
  
- 分析无法执行由输入不足所导致。  
  
- 分析引发不由 FxCopCmd 处理了异常。  
  
- 指定的项目文件未找到或已损坏。  
  
- 未指定输出选项，或无法写入该文件。  
  
    > [!NOTE]
    > FxCopCmd 返回代码"程序集引用错误"0x200 本身是一条警告，而不是错误。 此返回代码指示未找到缺少的间接引用，但 FxCopCmd 无法处理它们。 它是一条警告，存在一些分析结果可能已泄露的可能性。 与任何其他返回代码结合使用它时，请考虑"程序集引用错误"返回代码为错误。  
  
## <a name="see-also"></a>请参阅  
 [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)