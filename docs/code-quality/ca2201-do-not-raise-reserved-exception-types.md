---
title: CA2201:不要引发保留的异常类型
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotRaiseReservedExceptionTypes
- CA2201
helpviewer_keywords:
- CA2201
- DoNotRaiseReservedExceptionTypes
ms.assetid: dd14ef5c-80e6-41a5-834e-eba8e2eae75e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3d9b787a4e50f43867b5d9b4ec7a11aba03f8599
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231672"
---
# <a name="ca2201-do-not-raise-reserved-exception-types"></a>CA2201:不要引发保留的异常类型

|||
|-|-|
|TypeName|DoNotRaiseReservedExceptionTypes|
|CheckId|CA2201|
|类别|Microsoft.Usage|
|重大更改|重大|

## <a name="cause"></a>原因

方法引发的异常类型太笼统或由运行时保留。

## <a name="rule-description"></a>规则说明

以下异常类型太一般，无法为用户提供足够的信息：

- <xref:System.Exception?displayProperty=fullName>

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.SystemException?displayProperty=fullName>

以下异常类型已保留，只应由公共语言运行时引发：

- <xref:System.AccessViolationException?displayProperty=fullName>

- <xref:System.ExecutionEngineException?displayProperty=fullName>

- <xref:System.IndexOutOfRangeException?displayProperty=fullName>

- <xref:System.NullReferenceException?displayProperty=fullName>

- <xref:System.OutOfMemoryException?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.COMException?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.ExternalException?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SEHException?displayProperty=fullName>

- <xref:System.StackOverflowException?displayProperty=fullName>

**不引发一般异常**

如果在库或框架中引发一般异常类型<xref:System.Exception> （ <xref:System.SystemException>如或），则它会强制使用者捕获所有异常，包括不知道如何处理的未知异常。

相反，引发框架中已存在的派生程度更高的类型，或者创建您自己的派生自<xref:System.Exception>的类型。

**引发特定异常**

下表显示了参数以及在验证参数时要引发的异常，包括属性的 set 访问器中的 value 参数：

|参数说明|例外|
|---------------------------|---------------|
|`null`对|<xref:System.ArgumentNullException?displayProperty=fullName>|
|超出允许的值范围（如集合或列表的索引）|<xref:System.ArgumentOutOfRangeException?displayProperty=fullName>|
|值`enum`无效|<xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=fullName>|
|包含的格式不符合方法的参数规范（如的格式字符串`ToString(String)`）|<xref:System.FormatException?displayProperty=fullName>|
|否则无效|<xref:System.ArgumentException?displayProperty=fullName>|

当操作对对象引发的当前状态无效时<xref:System.InvalidOperationException?displayProperty=fullName>

对已释放的引发的对象执行操作时<xref:System.ObjectDisposedException?displayProperty=fullName>

不支持操作时（例如在重写的流中**写入**）<xref:System.NotSupportedException?displayProperty=fullName>

当转换导致溢出时（如在显式强制转换运算符重载中）引发<xref:System.OverflowException?displayProperty=fullName>

对于所有其他情况，可考虑创建自己的派生自<xref:System.Exception>的类型并引发该。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请将引发的异常的类型更改为非保留类型之一的特定类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则

- [CA1031不要捕获一般异常类型](../code-quality/ca1031-do-not-catch-general-exception-types.md)
