---
title: CA2007：不直接等待任务
ms.date: 03/08/2019
ms.topic: reference
f1_keywords:
- CA2007
- DoNotDirectlyAwaitATaskAnalyzer
helpviewer_keywords:
- CA2007
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.openlocfilehash: cf07c997f933e6aacf3eff29ae204ecd0bedb036
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233077"
---
# <a name="ca2007-do-not-directly-await-a-task"></a>CA2007：不直接等待任务

|||
|-|-|
|TypeName|DoNotDirectlyAwaitATaskAnalyzer|
|CheckId|CA2007|
|类别|Microsoft.Reliability|
|重大更改|不间断|

## <a name="cause"></a>原因

异步方法会 直接[等待](/dotnet/csharp/language-reference/keywords/await) <xref:System.Threading.Tasks.Task>。

## <a name="rule-description"></a>规则说明

当异步方法<xref:System.Threading.Tasks.Task>直接等待时，延续将在创建任务的同一线程中发生。 此行为在性能方面可能会很大，并且可能会在 UI 线程上导致死锁。 请考虑<xref:System.Threading.Tasks.Task.ConfigureAwait(System.Boolean)?displayProperty=nameWithType>调用以通知你的继续符。

此规则是通过[FxCop 分析器](install-fxcop-analyzers.md)引入的，在传统的 FxCop 分析中不存在。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决冲突， <xref:System.Threading.Tasks.Task.ConfigureAwait%2A>请在等待<xref:System.Threading.Tasks.Task>的上调用。 可以为`true` `false` 参数`continueOnCapturedContext`传递或。

- 对`ConfigureAwait(true)`任务调用与未显式调用<xref:System.Threading.Tasks.Task.ConfigureAwait%2A>的行为相同。 通过显式调用此方法，您就会让读者知道您有意要对原始同步上下文执行继续。

- 对`ConfigureAwait(false)`任务调用以将延续任务计划给线程池，从而避免 UI 线程上出现死锁。 对于`false`与应用无关的库，传递是一个不错的选择。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果你知道使用者不是图形用户界面（GUI）应用，或者使用者<xref:System.Threading.SynchronizationContext>没有，则可以禁止显示此警告。

## <a name="example"></a>示例

下面的代码段生成警告：

```csharp
public async Task Execute()
{
    Task task = null;
    await task;
}
```

若要解决此冲突， <xref:System.Threading.Tasks.Task.ConfigureAwait%2A>请对等待<xref:System.Threading.Tasks.Task>的调用：

```csharp
public async Task Execute()
{
    Task task = null;
    await task.ConfigureAwait(false);
}
```

## <a name="configurability"></a>配置

你可以配置是否要排除不从此规则返回值的异步方法。 若要排除这些类型的方法，请将以下键/值对添加到项目中的 editorconfig 文件：

```ini
# Package version 2.9.0 and later
dotnet_code_quality.CA2007.exclude_async_void_methods = true

# Package version 2.6.3 and earlier
dotnet_code_quality.CA2007.skip_async_void_methods = true
```

你还可以配置要应用此规则的输出程序集类型。 例如，若要仅将此规则应用于生成控制台应用程序或动态链接库（即，不是 UI 应用）的代码，请将以下键-值对添加到项目中的 editorconfig 文件：

```ini
dotnet_code_quality.CA2007.output_kind = ConsoleApplication, DynamicallyLinkedLibrary
```

有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="see-also"></a>请参阅

- [是否应使用 ConfigureAwait （false）来等待任务？](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md#should-i-await-a-task-with-configureawaitfalse)
- [在 Visual Studio 中安装 FxCop 分析器](install-fxcop-analyzers.md)