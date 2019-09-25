---
title: CA2211:非常量字段不应是可见的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2211
- NonConstantFieldsShouldNotBeVisible
helpviewer_keywords:
- NonConstantFieldsShouldNotBeVisible
- CA2211
ms.assetid: e1e42c40-0acd-4312-af29-70133739a304
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 11ff4ca3a3146c1080e26fd3ab50af7f7cf0e4e6
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231759"
---
# <a name="ca2211-non-constant-fields-should-not-be-visible"></a>CA2211:非常量字段不应是可见的

|||
|-|-|
|TypeName|NonConstantFieldsShouldNotBeVisible|
|CheckId|CA2211|
|类别|Microsoft.Usage|
|重大更改|重大|

## <a name="cause"></a>原因
公共或受保护的静态字段不是常量，也不是只读的。

## <a name="rule-description"></a>规则说明
不是常数也不是只读字段的静态字段不是线程安全的。 必须严格控制对此类字段的访问，并且需要使用高级编程技术来同步对类对象的访问。 由于这些都是很难学习和掌握的技能，并且测试此类对象会带来自己的挑战，因此最好将静态字段用于存储不会更改的数据。 此规则适用于库;应用程序不应公开任何字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将静态字段设置为常量或只读。 如果这是不可能的，请重新设计该类型以使用替代机制（如线程安全属性）来管理对基础字段的线程安全访问。 请注意，锁争用和死锁之类的问题可能会影响库的性能和行为。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果你正在开发应用程序，因此可以安全地禁止显示此规则发出的警告，从而可以完全控制对包含静态字段的类型的访问。 库设计器不应禁止显示此规则发出的警告;使用非常量静态字段可以使开发人员难以正确使用库。

## <a name="example"></a>示例
下面的示例演示违反此规则的类型。

[!code-vb[FxCop.Usage.AvoidStaticNonConstants#1](../code-quality/codesnippet/VisualBasic/ca2211-non-constant-fields-should-not-be-visible_1.vb)]
[!code-csharp[FxCop.Usage.AvoidStaticNonConstants#1](../code-quality/codesnippet/CSharp/ca2211-non-constant-fields-should-not-be-visible_1.cs)]