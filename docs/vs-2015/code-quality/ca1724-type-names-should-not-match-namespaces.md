---
title: CA1724：类型名不应与命名空间匹配 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
helpviewer_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
ms.assetid: 329af3b5-5600-4101-831d-531ab3eb7060
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aa0b73b6608f0dfd5daa4b770b7d780e64704c99
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544425"
---
# <a name="ca1724-type-names-should-not-match-namespaces"></a>CA1724:类型名不应与命名空间冲突
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|TypeNamesShouldNotMatchNamespaces|
|CheckId|CA1724|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型名称匹配不区分 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 大小写的比较中的命名空间名称。

## <a name="rule-description"></a>规则描述
 类型名称不应该与 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类库中定义的命名空间的名称匹配。 与该规则冲突将使库的可用性下降。

## <a name="how-to-fix-violations"></a>如何解决冲突
 选择与类库命名空间的名称不匹配的类型名称 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 对于新开发，不会发生任何已知方案，你必须禁止显示此规则发出的警告。 在您禁止显示该警告之前，请仔细考虑您库的用户可能会如何与匹配名称混淆。 对于装运库，可能必须禁止显示此规则发出的警告。
