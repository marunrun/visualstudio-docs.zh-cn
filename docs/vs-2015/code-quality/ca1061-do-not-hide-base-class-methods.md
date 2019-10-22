---
title: CA1061：不要隐藏基类方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1061
- DoNotHideBaseClassMethods
helpviewer_keywords:
- DoNotHideBaseClassMethods
- CA1061
ms.assetid: 0bda9dc8-87b4-4038-ab9d-563298387466
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 24579e6aa3ba1bf70ed6f195091152b60f3232a3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72604013"
---
# <a name="ca1061-do-not-hide-base-class-methods"></a>CA1061：不要隐藏基类方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotHideBaseClassMethods|
|CheckId|CA1061|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 派生类型声明一个方法，该方法具有相同的名称，并且参数的参数数目与它的一个基方法相同;一个或多个参数是基方法中的相应参数的基类型;所有剩余参数的类型都与基方法中的相应参数的类型相同。

## <a name="rule-description"></a>规则说明
 当派生方法的参数签名只是与基方法的参数签名中的相应类型的派生程度更弱的类型不同时，基类型中的同名方法会隐藏基类型中的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除或重命名该方法，或者更改参数签名，使该方法不会隐藏基方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了违反规则的方法。

 [!code-csharp[FxCop.Design.HideBaseMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.HideBaseMethod/cs/FxCop.Design.HideBaseMethod.cs#1)]
