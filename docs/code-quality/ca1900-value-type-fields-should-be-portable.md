---
title: CA1900:值类型字段应为可移植字段
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1900
- ValueTypeFieldsShouldBePortable
helpviewer_keywords:
- ValueTypeFieldsShouldBePortable
- CA1900
ms.assetid: 1787d371-389f-4d39-b305-12b53bc0dfb9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f734d0cf28a5aec28ebbf635dd384efe176b1774
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921320"
---
# <a name="ca1900-value-type-fields-should-be-portable"></a>CA1900:值类型字段应为可移植字段

|||
|-|-|
|TypeName|ValueTypeFieldsShouldBePortable|
|CheckId|CA1900|
|类别|Microsoft.Portability|
|是否重大更改|如果该字段可以在程序集外查看, 则为。<br /><br /> 无间断-如果该字段在程序集外部不可见, 则为。|

## <a name="cause"></a>原因
此规则检查在被封送到64位操作系统上的非托管代码时, 通过显式布局声明的结构是否会正确对齐。 IA-64 不允许未对齐的内存访问, 如果不解决此冲突, 进程将崩溃。

## <a name="rule-description"></a>规则说明
具有包含未对齐字段的显式布局的结构会导致在64位操作系统上发生崩溃。

## <a name="how-to-fix-violations"></a>如何解决冲突
小于8个字节的所有字段的偏移量必须是其大小的倍数, 而大于8个字节或更大的字段的偏移量必须是8的倍数。 另一种解决方案是`LayoutKind.Sequential`使用`LayoutKind.Explicit`而不是, 前提是合理。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
只有出现错误时才应禁止显示此警告。