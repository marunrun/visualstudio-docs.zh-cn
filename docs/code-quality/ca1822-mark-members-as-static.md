---
title: CA1822:将成员标记为 static
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MarkMembersAsStatic
- CA1822
helpviewer_keywords:
- MarkMembersAsStatic
- CA1822
ms.assetid: 743f0af7-41d1-4852-8d97-af0688b31118
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f25b74949c734921c313ae2cf00a2d217029e52
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921389"
---
# <a name="ca1822-mark-members-as-static"></a>CA1822:将成员标记为 static

|||
|-|-|
|TypeName|MarkMembersAsStatic|
|CheckId|CA1822|
|类别|Microsoft.Performance|
|是否重大更改|无间断-如果该成员在程序集外部不可见, 不管你进行了何种更改。 不间断-如果只使用`this`关键字将成员更改为实例成员。<br /><br /> 如果将成员从实例成员更改为静态成员并且在程序集外部可见, 则为。|

## <a name="cause"></a>原因
不访问实例数据的成员未标记为静态的 (在中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]为共享)。

## <a name="rule-description"></a>规则说明
可以将不访问实例数据或不调用实例方法的成员标记为 static（在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中为 Shared）。 在将这些方法标记为 static 之后，编译器将向这些成员发出非虚拟调用站点。 发出非虚拟调用站点将阻止每个调用的运行时检查, 以确保当前对象指针为非 null。 这可以实现对性能敏感的代码的显著性能提升。 在某些情况下, 访问当前对象实例的失败表示正确性问题。

## <a name="how-to-fix-violations"></a>如何解决冲突
将成员标记为 static (在中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]为 Shared), 或在方法体中使用 "this"/"Me" (如果适用)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
对于以前发布的代码, 可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
[CA1811避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)

[CA1812避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1804删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)