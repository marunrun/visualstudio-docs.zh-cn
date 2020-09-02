---
title: 使用 DebuggerTypeProxy 属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- attributes [C#], debugger
- DebuggerTypeProxyAttribute class
- DebuggerTypeProxy attribute
ms.assetid: 943f3bb1-993e-4800-a47e-0af78b063014
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f6e349dd5bea4e0d89c31864960a5438d1e2b13f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684076"
---
# <a name="using-debuggertypeproxy-attribute"></a>使用 DebuggerTypeProxy 特性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DebuggerTypeProxyAttribute] (assetId:///T:System.Diagnostics.DebuggerTypeProxyAttribute?qualifyHint=False&自动升级 = True) 指定类型的代理或，并更改类型在调试器窗口中的显示方式。 查看具有代理的变量时，代理将代替“显示”中的原始类型。 调试器变量窗口仅显示代理类型的公共成员。 不会显示私有成员。  
  
 此特性可应用于：  
  
- 结构  
  
- 类  
  
- 程序集  
  
  类型代理类必须具有一个构造函数，该函数采用代理将替换的类型的参数。 在每次需要显示目标类型的变量时，调试器都会创建类型代理类的一个新实例。 这会对性能产生一定影响。 因此，不应在构造函数中执行非必需的工作。  
  
  若要最大程度地减小性能损失，表达式计算器将不检查类型的显示代理上的特性，除非用户在调试器窗口中单击 + 符号或使用 <xref:System.Diagnostics.DebuggerBrowsableAttribute> 扩展该类型。 因此，不应将特性置于显示类型自身中。 特性可以且应该用于显示类型的正文中。  
  
  类型代理最好是作为特性目标类中的私有嵌套类。 这样，它便能轻松访问内部成员。  
  
  如果在程序集级别使用 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>，则 `Target` 参数将指定代理要替换的类型。  
  
  有关如何将此特性与 <xref:System.Diagnostics.DebuggerDisplayAttribute> 和 <xref:System.Diagnostics.DebuggerTypeProxyAttribute> 一起使用的示例，请参阅[使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)。  
  
## <a name="using-generics-with-debuggertypeproxy"></a>将泛型与 DebuggerTypeProxy 一起使用  
 对泛型的支持是有限的。 对于 C#，`DebuggerTypeProxy` 只支持开放类型。 开放类型（也称作“非构造类型”）是一种还未使用其类型参数的自变量实例化的泛型类型。 不支持封闭类型（也称作“构造类型”）。  
  
 开放类型的语法类似于：  
  
 `Namespace.TypeName<,>`  
  
 如果使用泛型类型作为 `DebuggerTypeProxy` 中的目标，则必须使用该语法。 `DebuggerTypeProxy` 机制将为你推理类型参数。  
  
 有关 C# 中的开放类型和封闭类型的详细信息，请参阅 [C# 语言规范](https://msdn.microsoft.com/library/e5d5a5cc-636b-4bff-b9c8-a8edc6207c22)中的第 20.5.2 节“开放类型和封闭类型”。  
  
 Visual Basic 没有开放类型语法，因此您无法在 Visual Basic 中执行同样的操作。 而必须使用开放类型名称的字符串表示形式。  
  
 `"Namespace.TypeName'2"`  
  
## <a name="see-also"></a>另请参阅  
 [使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)   
  [使用调试器显示特性增强调试](https://msdn.microsoft.com/library/72bb7aa9-459b-42c4-9163-9312fab4c410)
