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
ms.openlocfilehash: 3f35e450f17a671b800d003b94ceb5ebc2321c90
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841395"
---
# <a name="ca2007-do-not-directly-await-a-task"></a>CA2007：不直接等待任务

|||
|-|-|
|TypeName|DoNotDirectlyAwaitATaskAnalyzer|
|CheckId|CA2007|
|类别|Microsoft.Reliability|
|是否重大更改|非换行|

## <a name="cause"></a>原因

异步方法[等待](/dotnet/csharp/language-reference/keywords/await)<xref:System.Threading.Tasks.Task>直接。

## <a name="rule-description"></a>规则说明

当异步方法等待<xref:System.Threading.Tasks.Task>延续直接创建了任务的同一线程中发生。 此行为可以极大地降低性能，并且可能会导致在 UI 线程上发生死锁。 请考虑调用<xref:System.Threading.Tasks.Task.ConfigureAwait(System.Boolean)?displayProperty=nameWithType>以指示您的继续符的意图。

此规则随[FxCop 分析器](install-fxcop-analyzers.md)"旧"（静态代码分析） 中不存在和 FxCop。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决冲突，请调用<xref:System.Threading.Tasks.Task.ConfigureAwait%2A>上等待<xref:System.Threading.Tasks.Task>。 您可以传递`true`或`false`为`continueOnCapturedContext`参数。

- 调用`ConfigureAwait(true)`任务上具有相同的行为不显式调用<xref:System.Threading.Tasks.Task.ConfigureAwait%2A>。 通过显式调用此方法，即让读者了解有意想要在原始的同步上下文上执行延续任务。

- 调用`ConfigureAwait(false)`来计划到线程池的延续任务，从而避免在 UI 线程上的发生死锁。 传递`false`是独立于应用程序的库的一个不错的选择。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果您知道，使用者不是一个图形用户界面 (GUI) 应用，或使用者没有可以取消显示此警告<xref:System.Threading.SynchronizationContext>。

## <a name="example"></a>示例

下面的代码段将生成警告：

```csharp
public async Task Execute()
{
    Task task = null;
    await task;
}
```

若要解决冲突，请调用<xref:System.Threading.Tasks.Task.ConfigureAwait%2A>上等待<xref:System.Threading.Tasks.Task>:

```csharp
public async Task Execute()
{
    Task task = null;
    await task.ConfigureAwait(false);
}
```

## <a name="configurability"></a>可配置性

你可以配置你想要排除不与该规则返回值的异步方法。 若要排除这些类型的方法，请将以下键-值对添加到你的项目中的.editorconfig 文件：

```ini
# Package version 2.9.0 and later
dotnet_code_quality.CA2007.exclude_async_void_methods = true

# Package version 2.6.3 and earlier
dotnet_code_quality.CA2007.skip_async_void_methods = true
```

此外可以配置哪个输出程序集类型应用此规则。 例如，若要仅将此规则应用于生成控制台应用程序或动态链接的库 （即，不 UI 应用） 的代码，到你的项目中的.editorconfig 文件添加以下键-值对：

```ini
dotnet_code_quality.CA2007.output_kind = ConsoleApplication, DynamicallyLinkedLibrary
```

有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="see-also"></a>请参阅

- [应等待的任务使用 configureawait （false）？](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md#should-i-await-a-task-with-configureawaitfalse)
- [在 Visual Studio 中安装 FxCop 分析器](install-fxcop-analyzers.md)