---
title: CA1504：查看误导性字段名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewMisleadingFieldNames
- CA1504
helpviewer_keywords:
- CA1504
- ReviewMisleadingFieldNames
ms.assetid: 94136ff1-4aaf-4dc2-9170-48c171ab7499
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d375b64bbc877cb377157f13b3e4cfa7c7cf1592
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547870"
---
# <a name="ca1504-review-misleading-field-names"></a>CA1504:检查令人误解的字段名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|ReviewMisleadingFieldNames|
|CheckId|CA1504|
|类别|Microsoft 可维护性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 实例字段的名称以 "s_" 开头或 `static` （in）字段的名称以 `Shared` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] "m_" 开头。

## <a name="rule-description"></a>规则描述
 以 "s_" 开头的字段名称与多个用户的静态数据相关联。 同样，以 "m_" 开头的字段名称与实例（成员）数据相关联。 为了更轻松地维护代码，名称应遵循一般使用的约定。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用相应的前缀重命名该字段。 或者，通过添加或删除修饰符，使字段与当前后缀一致 `static` 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。
