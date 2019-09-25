---
title: CA1063:正确实现 IDisposable
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- ImplementIDisposableCorrectly
- CA1063
helpviewer_keywords:
- CA1063
- ImplementIDisposableCorrectly
ms.assetid: 12afb1ea-3a17-4a3f-a1f0-fcdb853e2359
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 8b29c9ed644c223488261333e79f17229bd4b7a3
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235304"
---
# <a name="ca1063-implement-idisposable-correctly"></a>CA1063:正确实现 IDisposable

|||
|-|-|
|TypeName|ImplementIDisposableCorrectly|
|CheckId|CA1063|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因

<xref:System.IDisposable?displayProperty=nameWithType>接口未正确实现。 此情况的可能原因包括：

- <xref:System.IDisposable>在类中是重新实现。

- `Finalize`再次重写。

- `Dispose()`被重写。

- 方法不是公共、[密封](/dotnet/csharp/language-reference/keywords/sealed)或名为**Dispose。** `Dispose()`

- `Dispose(bool)`不受保护、虚拟或未密封。

- 在未密封的`Dispose()`类型中`Dispose(true)`，必须调用。

- 对于未密封类型， `Finalize`实现不会调用或同时`Dispose(bool)`调用或基类终结器。

违反其中任何一种模式都会触发警告 CA1063。

声明和实现接口的<xref:System.IDisposable>每个未密封类型都必须提供其自己`protected virtual void Dispose(bool)`的方法。 `Dispose()`应调用`Dispose(true)`，并且终结器应调用`Dispose(false)`。 如果创建声明和实现<xref:System.IDisposable>接口的非密封类型，则必须定义`Dispose(bool)`并调用它。 有关详细信息，请参阅[清理非托管资源（.net 指南）](/dotnet/standard/garbage-collection/unmanaged)和[Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)。

默认情况下，此规则仅查看外部可见类型，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

所有<xref:System.IDisposable>类型都应正确实现[Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)。

## <a name="how-to-fix-violations"></a>如何解决冲突

检查你的代码并确定以下哪种解决方法会修复此冲突：

- 从<xref:System.IDisposable>类型实现的接口列表中删除，而改为重写基类释放实现。

- 从类型中删除终结器，重写 Dispose （bool 释放），并在 "释放" 为 false 的代码路径中放置终止逻辑。

- 重写 Dispose （bool 释放），并将 dispose 逻辑放在 "释放" 为 true 的代码路径中。

- 请确保 Dispose （）被声明为 public 和[sealed](/dotnet/csharp/language-reference/keywords/sealed)。

- 重命名 dispose 方法以**释放**，并确保将其声明为 public 和[sealed](/dotnet/csharp/language-reference/keywords/sealed)。

- 请确保 Dispose （bool）声明为 protected、virtual 和未密封。

- 修改 dispose （），使其调用 dispose （true），然后调用<xref:System.GC.SuppressFinalize%2A>当前对象实例（`this`或`Me` Visual Basic），然后返回。

- 修改终结器，使其调用 Dispose （false），然后返回。

- 如果你创建了一个声明并实现<xref:System.IDisposable>接口的非密封类型，请确保的<xref:System.IDisposable>实现遵循本部分前面所述的模式。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1063.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（设计）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="pseudo-code-example"></a>伪代码示例

下面的伪代码提供了一个示例，说明如何在使用托管资源和本机资源的类中实现 Dispose （bool）。

```csharp
public class Resource : IDisposable
{
    private IntPtr nativeResource = Marshal.AllocHGlobal(100);
    private AnotherResource managedResource = new AnotherResource();

    // Dispose() calls Dispose(true)
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    // NOTE: Leave out the finalizer altogether if this class doesn't
    // own unmanaged resources, but leave the other methods
    // exactly as they are.
    ~Resource()
    {
        // Finalizer calls Dispose(false)
        Dispose(false);
    }

    // The bulk of the clean-up code is implemented in Dispose(bool)
    protected virtual void Dispose(bool disposing)
    {
        if (disposing)
        {
            // free managed resources
            if (managedResource != null)
            {
                managedResource.Dispose();
                managedResource = null;
            }
        }
        // free native resources if there are any.
        if (nativeResource != IntPtr.Zero)
        {
            Marshal.FreeHGlobal(nativeResource);
            nativeResource = IntPtr.Zero;
        }
    }
}
```

## <a name="see-also"></a>请参阅

- [Dispose 模式（框架设计准则）](/dotnet/standard/design-guidelines/dispose-pattern)
- [清理非托管资源（.NET 指南）](/dotnet/standard/garbage-collection/unmanaged)