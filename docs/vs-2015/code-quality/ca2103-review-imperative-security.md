---
title: CA2103：检查命令性安全 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b4abf0b15a4fbba1abc61572da8a2f6126c754f2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652163"
---
# <a name="ca2103-review-imperative-security"></a>CA2103：检查命令性安全
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
 与声明性安全（使用属性在元数据中存储权限和操作）相比，命令性安全在代码执行期间使用托管对象指定权限和安全操作。 命令性安全性非常灵活，因为你可以使用在运行时之前不可用的信息来设置权限对象的状态并选择安全操作。 这种灵活性带来的风险在于，只要操作有效，您用于确定权限状态的运行时信息就不会保持不变。

 应尽可能使用声明性安全。 声明性要求更易于理解。

## <a name="how-to-fix-violations"></a>如何解决冲突
 查看命令性安全要求，以确保权限的状态不依赖于在使用权限时可以更改的信息。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果权限不依赖于变化的数据，则可以安全地禁止显示此规则发出的警告。 但是，最好将命令性需求更改为其声明性等效项。

## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
