---
title: CA2201:不要引发保留的异常类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseReservedExceptionTypes
- CA2201
helpviewer_keywords:
- CA2201
- DoNotRaiseReservedExceptionTypes
ms.assetid: dd14ef5c-80e6-41a5-834e-eba8e2eae75e
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 580a021a85d1211932c248ddc925a49e95e1cf13
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142562"
---
# <a name="ca2201-do-not-raise-reserved-exception-types"></a>CA2201:不要引发保留的异常类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotRaiseReservedExceptionTypes|
|CheckId|CA2201|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因
 某方法引发的异常类型过于一般或者保留的运行时。

## <a name="rule-description"></a>规则说明
 下面的异常类型是太通用，向用户提供足够的信息：

- <xref:System.Exception?displayProperty=fullName>

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.SystemException?displayProperty=fullName>

  下面的异常类型被保留，应仅由公共语言运行时引发：

- <xref:System.ExecutionEngineException?displayProperty=fullName>

- <xref:System.IndexOutOfRangeException?displayProperty=fullName>

- <xref:System.NullReferenceException?displayProperty=fullName>

- <xref:System.OutOfMemoryException?displayProperty=fullName>

  **不会引发一般异常**

  如果您引发一般异常类型，如<xref:System.Exception>或<xref:System.SystemException>中的库或框架，它会强制使用者能够捕捉所有异常，包括未知他们不知道如何处理的异常。

  相反，引发在 framework 中，已存在的派生程度更大的类型，或创建您自己的派生类型<xref:System.Exception>。

  **引发特定异常**

  下表显示了参数和验证属性的 set 访问器中包含值参数的参数时引发的异常：

|参数说明|例外|
|---------------------------|---------------|
|`null` 引用|<xref:System.ArgumentNullException?displayProperty=fullName>|
|超出允许的范围的值 （如集合或列表的索引）|<xref:System.ArgumentOutOfRangeException?displayProperty=fullName>|
|无效`enum`值|<xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=fullName>|
|包含不符合一种方法的参数规范的格式 (例如的格式字符串`ToString(String)`)|<xref:System.FormatException?displayProperty=fullName>|
|否则为无效|<xref:System.ArgumentException?displayProperty=fullName>|

 当操作对象引发的当前状态无效 <xref:System.InvalidOperationException?displayProperty=fullName>

 当对已释放的对象执行操作时引发 <xref:System.ObjectDisposedException?displayProperty=fullName>

 不支持操作时 (如在被重写**Stream.Write**中打开进行读操作 Stream) 引发 <xref:System.NotSupportedException?displayProperty=fullName>

 当转换会导致溢出 （例如在显式强制转换运算符重载） 时引发 <xref:System.OverflowException?displayProperty=fullName>

 对于所有其他情况下，请考虑创建自己的派生类型<xref:System.Exception>并引发该异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改为不是保留的类型之一的特定类型引发的异常的类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关的规则
 [CA1031:不要捕捉一般异常类型](../code-quality/ca1031-do-not-catch-general-exception-types.md)
