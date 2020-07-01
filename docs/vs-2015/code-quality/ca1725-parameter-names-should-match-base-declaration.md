---
title: CA1725：参数名应与基声明匹配 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ParameterNamesShouldMatchBaseDeclaration
- CA1725
helpviewer_keywords:
- CA1725
- ParameterNamesShouldMatchBaseDeclaration
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f1fb30cd37ebffcee7619190cef83560813b25db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547363"
---
# <a name="ca1725-parameter-names-should-match-base-declaration"></a>CA1725:参数名应与基方法中的声明保持一致
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ParameterNamesShouldMatchBaseDeclaration|
|CheckId|CA1725|
|Category|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见方法重写中的参数名称与方法的基声明中的参数名称或该方法的接口声明中的参数名称不匹配。

## <a name="rule-description"></a>规则描述
 以一致的方式命名重写层次结构中的参数可以提高方法重写的可用性。 如果派生方法中的参数名与基声明中的名称不同，可能会导致无法区分出该方法是基方法的重写还是该方法的新重载。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请重命名参数以匹配基声明。 此修补程序是对 COM 可见方法的重大更改。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，但之前已发布的库中的 COM visible 方法除外。
