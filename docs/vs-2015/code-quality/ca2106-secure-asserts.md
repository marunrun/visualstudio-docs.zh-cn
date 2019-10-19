---
title: CA2106：安全断言 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2106
- SecureAsserts
helpviewer_keywords:
- CA2106
- SecureAsserts
ms.assetid: 91feb36e-6e2c-436c-8272-5aee31f77e98
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1f333478c952db74fa6a9482cdad91ce6a858301
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666003"
---
# <a name="ca2106-secure-asserts"></a>CA2106：保护断言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecureAsserts|
|CheckId|CA2106|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 某个方法断言权限，但不对调用方执行任何安全检查。

## <a name="rule-description"></a>规则说明
 如果在不执行任何安全检查的情况下断言安全权限，则会在代码中留下可利用的安全漏洞。 安全堆栈审核在断言安全权限时停止。 如果在不对调用方执行任何检查的情况下断言权限，调用方可以使用您的权限间接执行代码。 仅当你确定断言无法以有害方式使用时，才允许不进行安全检查的断言。 如果调用的代码无害，或用户无法将任意信息传递给所调用的代码，则断言不会造成危害。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将安全要求添加到方法或其声明类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅在仔细检查安全检查后，禁止显示此规则发出的警告。

## <a name="see-also"></a>请参阅
 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>[安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)
