---
title: 代码分析规则 CA2153 损坏状态异常
ms.date: 02/19/2019
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4b75e45b8a199265eaefe3a2b3c37ed62039e0eb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62542152"
---
# <a name="ca2153-avoid-handling-corrupted-state-exceptions"></a>CA2153:避免处理损坏状态异常

|||
|-|-|
|TypeName|AvoidHandlingCorruptedStateExceptions|
|CheckId|CA2153|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

[损坏状态异常 (Cse)](https://msdn.microsoft.com/magazine/dd419661.aspx)指示该内存损坏进程中存在。 如果攻击者可以将攻击放置到损坏的内存区域，则捕获它们（而非允许进程崩溃）可能导致安全漏洞。

## <a name="rule-description"></a>规则说明

CSE 指示进程状态已损坏且未被系统捕获。 损坏的状态的情况，在常规处理程序仅捕获异常如果将方法标记<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=fullName>属性。 默认情况下[公共语言运行时 (CLR)](/dotnet/standard/clr)不会为 Cse 调用 catch 处理程序。

最安全的选择是允许进程崩溃而不捕获这些类型的异常。 甚至日志记录代码可以允许攻击者利用内存损坏错误。

此警告时使用的常规处理程序捕获所有异常，例如，捕获 cse 时会触发`catch (System.Exception e)`或`catch`不使用任何异常参数。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此警告，请执行以下操作：

- 删除 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> 特性。 这将恢复为默认运行时行为，其中 CSE 不会传递到 catch 处理程序。

- 删除常规 catch 处理程序，而不是捕获特定异常类型的处理程序。 这可能包括 Cse，假定处理程序代码可以安全地处理它们 （少见）。

- 在 catch 处理程序，也不能将异常传递给调用方应导致结束正在运行的进程中重新引发该 CSE。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="pseudo-code-example"></a>伪代码示例

### <a name="violation"></a>冲突

下面伪代码说明此规则检测到的模式。

```csharp
[HandleProcessCorruptedStateExceptions]
// Method that handles CSE exceptions.
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle exception.
    }
}
```

### <a name="solution-1---remove-the-attribute"></a>解决方案 1-删除属性

删除<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性可确保您的方法未处理损坏状态异常。

```csharp
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle exception.
    }
}
```

### <a name="solution-2---catch-specific-exceptions"></a>解决方案 2-捕获特定异常

删除常规的 catch 处理程序并只捕获特定异常类型。

```csharp
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle IOException.
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle UnauthorizedAccessException.
    }
}
```

### <a name="solution-3---rethrow"></a>解决方案 3-再次引发

重新引发异常。

```csharp
[HandleProcessCorruptedStateExceptions]
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Rethrow the exception.
        throw;
    }
}
```