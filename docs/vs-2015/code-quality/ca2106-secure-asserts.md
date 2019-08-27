---
title: CA2106:安全断言 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1fb1968c6e2750f658f39f009c97fbab133cccab
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687398"
---
# <a name="ca2106-secure-asserts"></a>CA2106:保护断言
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
 如果在不执行任何安全检查的情况下断言安全权限，则会在代码中留下可利用的安全漏洞。 安全堆栈审核停止时断言安全权限。 如果在调用方执行任何检查的情况下断言权限，调用方可以通过使用你的权限间接执行代码。 断言无安全检查是允许仅当你确信，无法以有害方式使用断言。 断言不会造成损害，如果您调用的代码是无害的或用户不能将任意信息传递给调用的代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请添加对方法或其声明类型安全要求。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 禁止显示此规则在仔细检查安全性后，才的警告。

## <a name="see-also"></a>请参阅
 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)
