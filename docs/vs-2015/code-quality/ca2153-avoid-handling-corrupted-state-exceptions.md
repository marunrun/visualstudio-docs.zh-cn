---
title: CA2153：避免处理损坏状态异常 |Microsoft Docs
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 418cc9cb-68ad-47e9-a6c8-a48b9c35db45
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 27d837c09e5f2f90796c149bf58d1114d7e6352d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546310"
---
# <a name="ca2153-avoid-handling-corrupted-state-exceptions"></a>CA2153:避免处理损坏状态异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|AvoidHandlingCorruptedStateExceptions|
|CheckId|CA2153|
|Category|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 [损坏状态异常 (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) 指示进程中存在内存损坏。 如果攻击者可以将攻击放置到损坏的内存区域，则捕获它们（而非允许进程崩溃）可能导致安全漏洞。

## <a name="rule-description"></a>规则描述
 CSE 指示进程状态已损坏且未被系统捕获。 在损坏状态的情况中，如果你将方法标记有适当的 `HandleProcessCorruptedStateExceptions` 特性，则常规的处理程序仅捕获异常。 默认情况下， [公共语言运行时 (CLR)](https://msdn.microsoft.com/library/8bs2ecf4.aspx) 将不会为 CSE 调用 catch 处理程序。

 允许进程崩溃而不捕获这些类型的异常是最安全的选择，因为甚至日志记录代码都可允许攻击者利用内存损坏错误。

 当使用捕获所有异常的常规处理程序（如 catch(exception) 或 catch(no exception specification)）捕获 CSE 时会触发此警告。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此警告，应执行以下任一操作：

 1. 请删除 `HandleProcessCorruptedStateExceptions` 属性。 这将恢复为默认运行时行为，其中 CSE 不会传递到 catch 处理程序。

 2. 删除常规 catch 处理程序，而不是捕获特定异常类型的处理程序。  这可能包括假定处理程序代码可以安全处理这些内容的 CSE（非常罕见）。

 3. 重新引发 catch 处理程序中的 CSE，确保异常传递给调用方并将导致结束正在运行的进程。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="pseudo-code-example"></a>伪代码示例

### <a name="violation"></a>冲突
 下面伪代码说明此规则检测到的模式。

```
[HandleProcessCorruptedStateExceptions]
//method to handle and log CSE exceptions
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
    }
}
```

### <a name="solution-1"></a>解决方法 1
 删除 HandleProcessCorruptedExceptions 特性确保将不会处理异常。

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-2"></a>解决方法 2
 删除常规的 catch 处理程序并只捕获特定异常类型。

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-3"></a>解决方法 3
 重新引发异常。

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
        throw;
    }
}
```
