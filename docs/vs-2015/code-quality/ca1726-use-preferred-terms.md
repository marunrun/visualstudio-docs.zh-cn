---
title: CA1726：使用首选字词 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UsePreferredTerms
- CA1726
helpviewer_keywords:
- UsePreferredTerms
ms.assetid: 642b2acd-3a33-4d1f-b0a7-67073ae73be2
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 96e0614bc5c08c83008af4e67a2aa865f08f74f3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547805"
---
# <a name="ca1726-use-preferred-terms"></a>CA1726:使用首选词条
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅 [CA1726：使用首选字词](/visualstudio/code-quality/ca1726-use-preferred-terms)。

|项|值|
|-|-|
|TypeName|UsePreferredTerms|
|CheckId|CA1726|
|类别|Microsoft。命名|
|是否重大更改|正在进行-对程序集引发时<br /><br /> 非中断-在类型参数上触发时|

## <a name="cause"></a>原因
 在外部可见的标识符的名称中，包括一个存在首选备用词条的词条。 此外，名称还包括字词标志或标志。

## <a name="rule-description"></a>规则描述
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
