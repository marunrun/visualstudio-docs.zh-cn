---
title: CA2207:以内联方式初始化值类型的静态字段
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeValueTypeStaticFieldsInline
- CA2207
helpviewer_keywords:
- CA2207
- InitializeValueTypeStaticFieldsInline
ms.assetid: d1ea9d8b-ecc2-46ca-86e2-c41dd0e76658
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 46f579b6776ffab6d0ed3b2e216e29d36d2065ee
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231690"
---
# <a name="ca2207-initialize-value-type-static-fields-inline"></a>CA2207:以内联方式初始化值类型的静态字段

|||
|-|-|
|TypeName|InitializeValueTypeStaticFieldsInline|
|CheckId|CA2207|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因
值类型声明显式静态构造函数。

## <a name="rule-description"></a>规则说明
当声明值类型时，它会经历默认初始化，其中所有值类型字段均设置为零，所有引用类型字段都设置为`null` （`Nothing`在 Visual Basic 中）。 仅保证在调用类型的实例构造函数或静态成员之前运行显式静态构造函数。 因此，如果创建类型时未调用实例构造函数，则不保证静态构造函数运行。

如果所有静态数据都以内联方式初始化并且未声明显式静态构造函数C# ，则和 Visual Basic 编译器`beforefieldinit`会将标志添加到 MSIL 类定义。 编译器还会添加包含静态初始化代码的私有静态构造函数。 此私有静态构造函数保证在访问类型的任何静态字段之前运行。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请在声明时初始化所有静态数据，并删除静态构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
[CA1810以内联方式初始化引用类型的静态字段](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md)