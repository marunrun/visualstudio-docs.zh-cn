---
title: CA1716：标识符不应与关键字 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
helpviewer_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
ms.assetid: 900cc8a1-1089-4069-a4ce-10b109ac4fab
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f81aec5973d1915ba646c20c3b84186443678754
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669103"
---
# <a name="ca1716-identifiers-should-not-match-keywords"></a>CA1716：标识符不应与关键字冲突
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldNotMatchKeywords|
|CheckId|CA1716|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 命名空间、类型或 viritual 或接口成员的名称与编程语言中的保留关键字匹配。

## <a name="rule-description"></a>规则说明
 命名空间、类型和虚拟和接口成员的标识符不应与面向公共语言运行时的语言所定义的关键字匹配。 根据所用的语言和关键字，编译器错误和歧义会使库难以使用。

 此规则检查以下语言中的关键字：

- Visual Basic

- C#

- C++/CLI

  不区分大小写的比较用于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 关键字，区分大小写比较用于其他语言。

## <a name="how-to-fix-violations"></a>如何解决冲突
 选择不在关键字列表中显示的名称。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果确信该标识符不会混淆 API 用户，并且库可用于 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 中的所有可用语言，则可以禁止显示此规则发出的警告。
