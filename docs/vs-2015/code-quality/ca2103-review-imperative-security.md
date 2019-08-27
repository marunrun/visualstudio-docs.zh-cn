---
title: CA2103:检查命令性安全 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2103
- ReviewImperativeSecurity
helpviewer_keywords:
- CA2103
- ReviewImperativeSecurity
ms.assetid: d24fde71-bdf6-46c0-8965-9a73dc33c1aa
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5b8b3067d5c8ab8204d6ad723315c400e7b27552
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694930"
---
# <a name="ca2103-review-imperative-security"></a>CA2103:检查命令性安全
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ReviewImperativeSecurity|
|CheckId|CA2103|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 某个方法使用命令性安全，并且可能正在使用在要求处于活动状态时可以更改的状态信息或返回值来构造权限。

## <a name="rule-description"></a>规则说明
 命令性安全使用的托管的对象来指定代码在执行期间，相比声明性安全，它使用属性来存储元数据中的权限和操作的权限和安全操作。 命令性安全是非常灵活，因为你可以将权限对象的状态设置并选择通过使用到运行时不可用的信息的安全操作。 合并到一起，灵活性得以实现，用于确定权限的状态不会保持运行时信息保持不变，只要该操作是有效的风险。

 应尽可能使用声明性安全。 声明性需求不易于理解。

## <a name="how-to-fix-violations"></a>如何解决冲突
 检查命令性安全请求，以确保该权限的状态不依赖于正在使用权限可以更改的信息。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果权限不依赖于变化的数据。 但是，它是更好的做法将强制性要求更改为其等效声明。

## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
