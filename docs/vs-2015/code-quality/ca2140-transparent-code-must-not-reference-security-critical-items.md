---
title: CA2140:透明代码不得引用安全关键项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2129
- SecurityTransparentCodeShouldNotReferenceNonpublicSecurityCriticalCode
- CA2140
helpviewer_keywords:
- CA2140
- SecurityTransparentCodeShouldNotReferenceNonpublicSecurityCriticalCode
- CA2129
ms.assetid: 251a12da-0557-47f5-a4f7-0229d590ae7b
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1990e781b5793b05166c6ff5b6e9c14141ffdd69
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154255"
---
# <a name="ca2140-transparent-code-must-not-reference-security-critical-items"></a>CA2140:透明代码不得引用安全关键项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsMustNotReferenceCriticalCode|
|CheckId|CA2140|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明的方法：

- 处理安全关键的安全异常类型

- 包含标记为安全关键类型的参数

- 已使用安全关键约束泛型参数

- 具有的安全关键类型的局部变量

- 引用被标记为安全关键的类型

- 调用标记为安全关键的方法

- 引用被标记为安全关键的字段

- 返回标记为安全关键类型

## <a name="rule-description"></a>规则说明
 将标有一个代码元素<xref:System.Security.SecurityCriticalAttribute>是安全关键的属性。 透明方法不能使用安全关键元素。 如果透明类型尝试使用安全关键类型<xref:System.TypeAccessException>， <xref:System.MethodAccessException> ，或<xref:System.FieldAccessException>引发。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请执行以下操作：

- 标记使用与安全关键代码的代码元素<xref:System.Security.SecurityCriticalAttribute>属性

     \- 或 -

- 删除<xref:System.Security.SecurityCriticalAttribute>从被标记为安全关键，而是将它们标记的代码元素的特性<xref:System.Security.SecuritySafeCriticalAttribute>或<xref:System.Security.SecurityTransparentAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在以下示例中，透明方法尝试引用安全关键泛型集合、 安全关键字段和安全关键方法。

 [!code-csharp[FxCop.Security.CA2140.TransparentMethodsMustNotReferenceCriticalCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2140.transparentmethodsmustnotreferencecriticalcode/cs/ca2140 - transparentmethodsmustnotreferencecriticalcode.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Security.SecurityTransparentAttribute> <xref:System.Security.SecurityCriticalAttribute>
 <xref:System.Security.SecurityTransparentAttribute>
 <xref:System.Security.SecurityTreatAsSafeAttribute>
 <xref:System.Security?displayProperty=fullName>
