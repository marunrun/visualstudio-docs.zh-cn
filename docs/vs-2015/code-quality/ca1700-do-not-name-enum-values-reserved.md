---
title: CA1700：不 &#39;保留&#39; 命名枚举值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1700
- DoNotNameEnumValuesReserved
helpviewer_keywords:
- DoNotNameEnumValuesReserved
- CA1700
ms.assetid: 7a7e01c3-ae7d-4c82-a646-91b58864a749
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 57f2a2e5959860a99a921101ff5782f9bce9ace3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545647"
---
# <a name="ca1700-do-not-name-enum-values-39reserved39"></a>CA1700：不 &#39;保留&#39; 命名枚举值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DoNotNameEnumValuesReserved|
|CheckId|CA1700|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 枚举成员的名称包含单词 "reserved"。

## <a name="rule-description"></a>规则描述
 此规则假定当前不使用名称中包含“reserved”的枚举成员，而是将其作为一个占位符，以在将来的版本中重命名或移除它。 重命名或移除成员是一项重大更改。 不应指望用户只是因为其名称包含 "保留" 而忽略成员，也不能依赖于用户阅读或遵守文档。 此外，由于保留成员显示在对象浏览器和智能集成开发环境中，因此它们可能会导致混淆实际使用的成员。

 在将来的版本中，将新成员添加到枚举，而不是使用保留成员。 在大多数情况下，添加新成员不是一项重大更改，只要添加不会导致原始成员的值发生变化。

 在有限的情况下，添加成员是一项重大更改，即使原始成员保留其原始值也是如此。 主要是，不能从现有代码路径返回新成员，而不会中断对 `switch` `Select` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 包含整个成员列表的返回值使用（in）语句并在默认情况下引发异常的调用方。 第二个问题是：客户端代码可能无法处理反射方法（如）的行为更改 <xref:System.Enum.IsDefined%2A?displayProperty=fullName> 。 相应地，如果新成员必须从现有方法返回，或者由于反射的使用不正确而发生已知的应用程序不兼容性，则唯一的不间断解决方案是：

1. 添加包含原始成员和新成员的新枚举。

2. 用特性标记原始枚举 <xref:System.ObsoleteAttribute?displayProperty=fullName> 。

   对于公开原始枚举的任何外部可见类型或成员，请遵循相同的过程。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除或重命名该成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 对于当前使用的成员或以前发布的库，可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA2217:不要使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

 [CA1712:不要将类型名用作枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

 [CA1028:枚举存储应为 Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

 [CA1008:枚举应具有零值](../code-quality/ca1008-enums-should-have-zero-value.md)

 [CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
