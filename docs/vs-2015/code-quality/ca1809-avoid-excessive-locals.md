---
title: CA1809:避免过多的局部变量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 64002b9b99d1b861fa3378710cb0bb8d9219c99d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158000"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809:避免过多的局部变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidExcessiveLocals|
|CheckId|CA1809|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 成员包含 64 个以上的本地变量，其中一些可能是编译器生成。

## <a name="rule-description"></a>规则说明
 优化性能的常见是将值存储于处理器寄存器，而不是在内存中，这被称为*注册*值。 公共语言运行时最多可考虑最多为 64 个局部变量。 放置在堆栈上的不是以内的变量，必须将移动到操作之前注册。 若要允许可能性，所有本地变量获取以内，限制为 64 的本地变量的数目。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请重构要使用局部变量不能超过 64 个的实现。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果性能不是一个问题，是若要禁止显示此规则的警告，或若要禁用规则，安全的。

## <a name="related-rules"></a>相关的规则
 [CA1804:删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)
