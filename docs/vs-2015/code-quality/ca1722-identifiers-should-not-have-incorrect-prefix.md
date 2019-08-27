---
title: CA1722:标识符应采用正确的前缀 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotHaveIncorrectPrefix
- CA1722
helpviewer_keywords:
- CA1722
- IdentifiersShouldNotHaveIncorrectPrefix
ms.assetid: c3313c51-d004-4f9a-a0d1-6c4c4a1fb1e6
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0c9aa6600578da0d9868df2ecff9992bff9e818c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191246"
---
# <a name="ca1722-identifiers-should-not-have-incorrect-prefix"></a>CA1722:标识符应采用正确的前缀
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectPrefix|
|CheckId|CA1722|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标识符具有不正确的前缀。

## <a name="rule-description"></a>规则说明
 按照约定，只有某些编程元素具有以特定前缀开头的名称。

 类型名称不具有特定前缀，并且不应使用 C 作为前缀。 此规则报告的类型名称，例如 CMyClass 冲突，并不会报告的类型名称，例如缓存冲突。

 命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。

## <a name="how-to-fix-violations"></a>如何解决冲突
 删除从标识符的前缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关的规则
 [CA1715:标识符应具有正确的前缀](../code-quality/ca1715-identifiers-should-have-correct-prefix.md)
