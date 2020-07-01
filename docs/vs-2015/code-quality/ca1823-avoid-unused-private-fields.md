---
title: CA1823：避免未使用的私有字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedPrivateFields
- CA1823
helpviewer_keywords:
- AvoidUnusedPrivateFields
- CA1823
ms.assetid: 614f94f6-0dc7-430f-8124-cb889a4a720f
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 01f2ef59ceb6d10cc33276fdd3e5388f39175f8b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545296"
---
# <a name="ca1823-avoid-unused-private-fields"></a>CA1823:避免未使用的私有字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|AvoidUnusedPrivateFields|
|CheckId|CA1823|
|Category|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 当代码中的私有字段存在，但未被任何代码路径使用时，将报告此规则。

## <a name="rule-description"></a>规则描述
 检测到程序集内有似乎未访问过的私有字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除字段或添加使用该字段的代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA1812:避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801:检查未使用的参数](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804:移除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)

 [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)
