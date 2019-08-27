---
title: CA2144:透明代码不应从字节数组加载程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2144
ms.assetid: 777b1310-6e16-4413-b4ee-5f3136304f82
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b54e74297ca44662f49b5842aae8e334a8f4045a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142658"
---
# <a name="ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays"></a>CA2144:透明代码不应从字节数组加载程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsShouldNotLoadAssembliesFromByteArrays|
|CheckId|CA2144|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明方法加载程序集从字节数组，使用以下方法之一：

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

## <a name="rule-description"></a>规则说明
 透明代码安全检查不像关键代码的安全检查一样全面，因为透明代码不能执行安全敏感的操作。 从字节数组中加载的程序集在不透明的代码中可能不会被注意到，并且该字节数组可能包含确实需要审核的关键或更重要的安全关键代码。 因此，透明代码不应从字节数组加载程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请将标记加载的程序集中的方法<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 因为透明的方法从字节数组加载程序集，则将触发规则上的以下代码。

 [!code-csharp[FxCop.Security.CA2144.TransparentMethodsShouldNotLoadAssembliesFromByteArrays#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2144.transparentmethodsshouldnotloadassembliesfrombytearrays/cs/ca2144 - transparentmethodsshouldnotloadassembliesfrombytearrays.cs#1)]
