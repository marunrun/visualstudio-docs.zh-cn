---
title: CA2207：以内联方式初始化值类型的静态字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InitializeValueTypeStaticFieldsInline
- CA2207
helpviewer_keywords:
- CA2207
- InitializeValueTypeStaticFieldsInline
ms.assetid: d1ea9d8b-ecc2-46ca-86e2-c41dd0e76658
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a2b3c1faf4ecf3ecf79a3c78d0ded106b88345ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72609365"
---
# <a name="ca2207-initialize-value-type-static-fields-inline"></a>CA2207：以内联方式初始化值类型的静态字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|InitializeValueTypeStaticFieldsInline|
|CheckId|CA2207|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 值类型声明显式静态构造函数。

## <a name="rule-description"></a>规则说明
 当声明值类型时，它会经历默认初始化，其中所有值类型字段均设置为零，所有引用类型字段都设置为 `null` （Visual Basic 中 `Nothing`）。 仅保证在调用类型的实例构造函数或静态成员之前运行显式静态构造函数。 因此，如果创建类型时未调用实例构造函数，则不保证静态构造函数运行。

 如果所有静态数据都以内联方式初始化并且未声明显式静态构造函数C# ，则和 Visual Basic 编译器会将 `beforefieldinit` 标志添加到 MSIL 类定义。 编译器还会添加包含静态初始化代码的私有静态构造函数。 此私有静态构造函数保证在访问类型的任何静态字段之前运行。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请在声明时初始化所有静态数据，并删除静态构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA1810：以内联方式初始化引用类型的静态字段](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md)
