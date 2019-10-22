---
title: CA1044：属性不应为 write |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PropertiesShouldNotBeWriteOnly
- CA1044
helpviewer_keywords:
- CA1044
- PropertiesShouldNotBeWriteOnly
ms.assetid: 8386bf3a-b161-4841-bf8b-92591595aea9
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aa2d07337ec48e41a9d8ad82602a387159192f92
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668276"
---
# <a name="ca1044-properties-should-not-be-write-only"></a>CA1044：属性不应是只写的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PropertiesShouldNotBeWriteOnly|
|CheckId|CA1044|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护的属性具有 set 访问器，但没有 get 访问器。

## <a name="rule-description"></a>规则说明
 Get 访问器提供对属性的读取访问权限，而 set 访问器提供写入访问权限。 虽然可以接受且经常需要使用只读属性，但设计准则禁止使用只写属性。 这是因为允许用户设置一个值，然后阻止用户查看该值不提供任何安全性。 而且，如果没有读访问，将无法查看共享对象的状态，使其用处受到限制。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 get 访问器添加到属性。 或者，如果需要只写属性的行为，请考虑将该属性转换为方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 强烈建议您不要禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中，`BadClassWithWriteOnlyProperty` 是具有只写属性的类型。 `GoodClassWithReadWriteProperty` 包含更正后的代码。

 [!code-csharp[FxCop.Design.PropertiesNotWriteOnly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.PropertiesNotWriteOnly/cs/FxCop.Design.PropertiesNotWriteOnly.cs#1)]
 [!code-vb[FxCop.Design.PropertiesNotWriteOnly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.PropertiesNotWriteOnly/vb/PropertiesNotWriteOnly.vb#1)]
