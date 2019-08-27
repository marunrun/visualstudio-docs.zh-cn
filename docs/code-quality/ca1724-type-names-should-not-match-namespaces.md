---
title: CA1724:类型名不应与命名空间冲突
ms.date: 09/28/2018
ms.topic: reference
f1_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
helpviewer_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
ms.assetid: 329af3b5-5600-4101-831d-531ab3eb7060
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f81327324de937df57edfb36cae34d613f6298a5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546015"
---
# <a name="ca1724-type-names-should-not-match-namespaces"></a>CA1724:类型名不应与命名空间

|||
|-|-|
|TypeName|TypeNamesShouldNotMatchNamespaces|
|CheckId|CA1724|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因

类型名称与一个或多个外部可见的类型的引用的命名空间名称相匹配。 名称比较不区分大小写。

## <a name="rule-description"></a>规则说明

用户创建的类型名不应与引用具有外部可见类型的命名空间的名称。 违反此规则会降低您的库的可用性。

## <a name="how-to-fix-violations"></a>如何解决冲突

重命名该类型，以便它与具有外部可见的类型的引用命名空间的名称不匹配。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

对于新开发，没有已知情况下，必须在此禁止显示此规则的警告。 禁止显示警告之前，请仔细考虑如何库用户可能会被搞糊涂了匹配的名称。 发布库，您可能需要禁止显示此规则的警告。