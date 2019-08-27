---
title: CA2211:非常量字段不应是可见 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2211
- NonConstantFieldsShouldNotBeVisible
helpviewer_keywords:
- NonConstantFieldsShouldNotBeVisible
- CA2211
ms.assetid: e1e42c40-0acd-4312-af29-70133739a304
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 48d1a449301c422aa457346d1eb3d48d2f395f2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142494"
---
# <a name="ca2211-non-constant-fields-should-not-be-visible"></a>CA2211:非常量字段不应是可见的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|NonConstantFieldsShouldNotBeVisible|
|CheckId|CA2211|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护的静态字段不是常量也不是只读的。

## <a name="rule-description"></a>规则说明
 不是常数也不是只读字段的静态字段不是线程安全的。 对此类字段的访问必须严格控制，并需要高级编程技术来同步对类对象的访问。 这些是技巧难以学习和母版和测试此类对象会带来独特挑战，因为静态字段最适合用于存储不会更改的数据。 此规则适用于库;应用程序不应公开任何字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请将静态字段常数或只读的。 如果无法做到这一点，重新设计要使用替代机制，例如管理的基础字段对线程安全的访问的线程安全属性的类型。 意识到问题，如锁争用和死锁可能影响性能和行为的库。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果你正在开发的应用的因此有权访问包含静态字段的类型的完全控制。 库设计器不应取消与该规则; 警告使用非常量静态字段可使用库开发人员难以正确使用。

## <a name="example"></a>示例
 下面的示例显示了与此规则冲突的类型。

 [!code-csharp[FxCop.Usage.AvoidStaticNonConstants#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AvoidStaticNonConstants/cs/FxCop.Usage.AvoidStaticNonConstants.cs#1)]
 [!code-vb[FxCop.Usage.AvoidStaticNonConstants#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.AvoidStaticNonConstants/vb/FxCop.Usage.AvoidStaticNonConstants.vb#1)]
