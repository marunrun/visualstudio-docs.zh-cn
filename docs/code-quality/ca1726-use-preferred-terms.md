---
title: CA1726:使用首选词条
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UsePreferredTerms
- CA1726
helpviewer_keywords:
- UsePreferredTerms
ms.assetid: 642b2acd-3a33-4d1f-b0a7-67073ae73be2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f359f7aa24ada0edf2c98a7d527ed715df85086
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233920"
---
# <a name="ca1726-use-preferred-terms"></a>CA1726:使用首选词条

|||
|-|-|
|TypeName|UsePreferredTerms|
|CheckId|CA1726|
|类别|Microsoft.Naming|
|重大更改|正在进行-对程序集引发时<br /><br /> 非中断-在类型参数上触发时|

## <a name="cause"></a>原因

在外部可见的标识符的名称中，包括一个存在首选备用词条的词条。 或名称包含字词标志或标志。

## <a name="rule-description"></a>规则说明

此规则将标识符分析为标记。 每个单独的标记和每个连续的双重标记组合将与规则中和任何自定义字典中不推荐使用的部分中的字词进行比较。 下表显示了规则中内置的术语及其首选替代项。

|过时术语|首选术语|
|-------------------|--------------------|
|`Arent`|`AreNot`|
|`Cancelled`|`Canceled`|
|`Cant`|`Cannot`|
|`ComPlus`|`EnterpriseServices`|
|`Couldnt`|`CouldNot`|
|`Didnt`|`DidNot`|
|`Doesnt`|`DoesNot`|
|`Dont`|`DoNot`|
|`Flag` 或 `Flags`|无替换字词。 请勿使用。|
|`Hadnt`|`HadNot`|
|`Hasnt`|`HasNot`|
|`Havent`|`HaveNot`|
|`Indices`|`Indexes`|
|`Isnt`|`IsNot`|
|`LogIn`|`LogOn`|
|`LogOut`|`LogOff`|
|`Shouldnt`|`ShouldNot`|
|`SignOn`|`SignIn`|
|`SignOff`|`SignOut`|
|`Wasnt`|`WasNot`|
|`Werent`|`WereNot`|
|`Wont`|`WillNot`|
|`Wouldnt`|`WouldNot`|
|`Writeable`|`Writable`|

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将此术语替换为首选替代项。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅当标识符的名称是有意的并且特别与原始字词相关，而不是首选字词时，才禁止显示此规则的警告。

## <a name="related-rules"></a>相关规则
[命名警告](../code-quality/naming-warnings.md)