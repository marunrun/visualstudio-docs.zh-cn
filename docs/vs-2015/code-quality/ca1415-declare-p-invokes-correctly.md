---
title: CA1415：正确声明 P 调用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1415
- DeclarePInvokesCorrectly
helpviewer_keywords:
- CA1415
- DeclarePInvokesCorrectly
ms.assetid: 42a90796-0264-4460-bf97-2fb4a093dfdc
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b9931d29c818d95785146558637c32237e2c5276
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547844"
---
# <a name="ca1415-declare-pinvokes-correctly"></a>CA1415：正确声明 P/Invoke
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DeclarePInvokesCorrectly|
|CheckId|CA1415|
|Category|Microsoft. 互操作性|
|是否重大更改|无间断-如果在程序集外部不能出现声明参数的 P/Invoke。 如果在程序集外部显示声明参数的 P/Invoke，则为。|

## <a name="cause"></a>原因
 平台调用方法的声明不正确。

## <a name="rule-description"></a>规则描述
 平台调用方法访问非托管代码，并通过使用 `Declare` 或中的关键字定义 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 。 目前，此规则查找目标 Win32 函数的平台调用方法声明，这些函数具有指向重叠结构参数的指针，并且相应的托管参数不是指向结构的指针 <xref:System.Threading.NativeOverlapped?displayProperty=fullName> 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请正确声明平台调用方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则并满足规则的平台调用方法。

 [!code-csharp[FxCop.Interoperability.DeclarePInvokes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DeclarePInvokes/cs/FxCop.Interoperability.DeclarePInvokes.cs#1)]

## <a name="see-also"></a>另请参阅
 [与非托管代码交互操作](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
